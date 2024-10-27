# Prática 2 - Segurança nos Sistemas Operativos

To check the UID and GID of the files in the current directory, use the command `ls` with the option `-n`.
```bash
ls -n
```

Create a C program that prints the effective and real UID of the current process, as well as its effective and
real GIDs. After its compilation, run the program and check the result.

```c
#include <stdio.h>
#include <unistd.h> // Unix Standard Library

int main() {
    printf("Real UID: %d\n", getuid());
    printf("Effective UID: %d\n", geteuid());
    printf("Real GID: %d\n", getgid());
    printf("Effective GID: %d\n", getegid());
    return 0;
}
```

Compile the program with the command gcc. Run the program and check the results.

```bash
gcc -o uid uid.c
./uid
```

Note: Hereafter, some of the commands have to be executed by a super-user. Use a preceding sudo command in
those cases.

Change the ownership of the executable just created (UID of the owner) with the command chown; change also
the owner group GID of the executable (with the chgrp command). Use the UID of any other user and the
GID of any other group. Run the program again and check the results.

```bash
sudo chown 1001 uid
sudo chgrp 1001 uid
./uid
```

Activate the Set-UID flag of the executable with the command chmod. Run the program again and check the
results.

```bash
sudo chmod u+s uid
./uid
```

Activate the Set-GID flag of the executable with the command chmod. Run the program again and check the
results.

```bash
sudo chmod g+s uid
./uid
```

Change again the ownership of the executable, or its owner group GID. Run the program again and check
the results.

```bash
sudo chown 1000 uid
sudo chgrp 1000 uid
./uid
```

This is the goal of the chroot system call, and Linux command; check how it works with the commands:

```bash
man 8 chroot # for linux commands
man 2 chroot # for system calls
```

For the system call:
 - it receives a `const char *path` that contains the path directory in the system
 - on success the zero is returned. On error, -1 is returned 

For the linux commands:
 - `--groups=G_LIST`specify supplementary groups
 - `--userspec=USER` specify user to use
 - `--skip-chdir` do not change working directory to `/`

Is this experiment we will create a confined environment where only 4 commands exist: bash, ls, mkdir, and vi. 

To find the path of the commands, use the command `which`:
```bash
which bash
which ls
which mkdir
which vi
```

Create a directory, and copy the executables of the commands to the directory:
```bash
cd /new_root_aes
mkdir lib bin
cp /bin/bash /new_root_aes/bin
cp /bin/ls /new_root_aes/bin
cp /bin/mkdir /new_root_aes/bin
cp /bin/vi /new_root_aes/bin
```

Copy the shared libraries of the commands to the directory:
```bash
ldd /bin/bash
ldd /bin/ls
ldd /bin/mkdir
ldd /bin/vi
```

Copy the shared libraries to the directory:
```bash
cp /lib/x86_64-linux-gnu/libtinfo.so.5 /new_root_aes/lib
cp /lib/x86_64-linux-gnu/libdl.so.2 /new_root_aes/lib
cp /lib/x86_64-linux-gnu/libc.so.6 /new_root_aes/lib
cp /lib/x86_64-linux-gnu/libtinfo.so.5 /new_root_aes/lib
cp /lib/x86_64-linux-gnu/libdl.so.2 /new_root_aes/lib
cp /lib/x86_64-linux-gnu/libc.so.6 /new_root_aes/lib
cp /lib/x86_64-linux-gnu/libtinfo.so.5 /new_root_aes/lib
cp /lib/x86_64-linux-gnu/libdl.so.2 /new_root_aes/lib
```

Change the root directory of the process with the command chroot. Check the result with the command ls.

```bash
sudo chroot /new_root_aes /bin/bash
ls
```

# Prática 3 - SGX e Enclaves

Dentro da pasta `HelloEnclaveV1` temos o código fonte com a seguinte estrutura:

- `App`: Contém o código responsável por criar o enclave e executar as funções do mesmo;
  - `App.cpp`: Código principal da aplicação;
  - `App.h`: Cabeçalho da aplicação;
- `Enclave`: Contém o código do enclave;
  - `Enclave.cpp`: Código do enclave;
  - `Enclave.h`: Cabeçalho do enclave;
  - `Enclave.edl`: Ficheiro de definição do enclave (*Enclave Definition Language*);
  - `Enclave.lds`: Ficheiro de ligação do enclave;
  - `Enclave_private_key.pem`: Chave privada do enclave.
  - `Enclave.config.xml`: Configuração do enclave.

O ficheiro `Enclave.edl` contém a definição das funções que podem ser chamadas dentro do enclave e tem a seguinte estrutura:

```c
enclave {
    
    trusted { // ECALLS : funções chamadas dentro do enclave
        public void e1_printf_hello_world(void);
    };

    untrusted { // OCALLS : funções chamadas fora do enclave
        public void o1_print_string([in, size=len] char* str, size_t len);
    };
};
```

A inicialização do enclave é feita no ficheiro `App.cpp`:

```cpp
#include "App.h"
#include "Enclave_u.h"

#include <stdio.h>
#include <sgx_urts.h>

int App::run() {
    sgx_status_t enclave_status = SGX_ERROR_UNEXPECTED;
    sgx_enclave_id_t enclave_id = 0;

    enclave_status = sgx_create_enclave(ENCLAVE_FILENAME, SGX_DEBUG_FLAG, NULL, NULL, &enclave_id, NULL);
    if (enclave_status != SGX_SUCCESS) {
        fprintf(stderr, "Enclave creation failed: %#x\n", enclave_status);
        return -1;
    }

    if ((enclave_status = e1_printf_hello_world(enclave_id)) != SGX_SUCCESS) {
        fprintf(stderr, "Enclave e1_printf_hello_world failed: %#x\n", enclave_status);
        sgx_destroy_enclave(enclave_id);
        return -1;
    }

    sgx_destroy_enclave(enclave_id);

    return 0;
}
```

Para compilar o código, basta executar o makefile presente na pasta `HelloEnclaveV1`:

```bash
make
```

Após a compilação, quatro ficheiros irão ser criados pela ferramenta `edger8r`, que é responsável por gerar o código de ligação entre o código da aplicação e o código do enclave:
 - `App/Enclave_u.c`: Código de ligação entre a aplicação e o enclave;
 - `App/Enclave_u.h`: Cabeçalho do código de ligação;
 - `Enclave/Enclave_t.c`: Código de ligação entre o enclave e a aplicação;
 - `Enclave/Enclave_t.h`: Cabeçalho do código de ligação.

Nota: Onde o `t` significa *trusted* e o `u` significa *untrusted*.

Irá surgir uma versão do enclave assinada e uma versão não assinada. Caso seja alterado o código do enclave, é necessário recompilar o mesmo e assinar o mesmo, caso contrário, a aplicação irá devolver o erro `The enclave image is not correct`.

Este programa foi construído em *hardware-mode*, ou seja, é necessário ter um processador com suporte a SGX para executar o mesmo. Para trocar para *simulation-mode*, basta alterar a flag `SGX_MODE` presente no makefile para `SIM`.

Foram calculados os tempos de execução de um programa de soma de elementos de uma lista, tanto dentro do enclave como fora do enclave. Os resultados foram os seguintes:
```
App: n = 10000
sum = 499982552 times=[12950, 12852, 12879, 12838, 12846, 12889, 12810, 12872, 12787, 12777, ]
Enclave: n = 10000
sum = 49995000 times=[48918, 46643, 36184, 36360, 36132, 35979, 36435, 36060, 35983, 35908, ]
```

Como podemos ver, o tempo de execução dentro do enclave é muito superior ao tempo de execução fora do enclave. Isto deve-se ao facto de que o enclave é uma zona segura e isolada, o que implica que a comunicação entre o enclave e o mundo exterior é mais lenta.
