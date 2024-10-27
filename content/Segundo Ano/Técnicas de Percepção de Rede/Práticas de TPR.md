## <mark style="background: #FFF3A3A6;">Prática 1 - Data Acquisition</mark>

### Wireshark

- Wireshark filters: https://wiki.wireshark.org/DisplayFilters

Print do wireshark:

![[Pasted image 20241005190741.png]]

Pelo I/O Graph dá para ver bastante informação útil:

Número total de pacotes:

![[Pasted image 20241005191437.png]]

Número de pacotes TCP:

![[Pasted image 20241005191453.png]]

Número de pacotes UDP:

![[Pasted image 20241005191508.png]]

Número de pacotes *uploaded*:

![[Pasted image 20241005191520.png]]

Número de pacotes *downloaded*:

![[Pasted image 20241005191531.png]]

### tshark (Terminal shark)

É a versão CLI do wireshark

Para ter uma listagem das interfaces:

```bash
$ tshark -d
```

Para capturar pacotes:

```bash
$ tshark -i <interface>
```

Para capturar pacotes e guardar num ficheiro a captura:

```bash
$ tshark -i <interface> -w ficheiro.pcap
```

Para ler os pacotes capturados:

```bash
$ tshark -r ficheiro.pcap
```

>[!important]
>**PCAP** significa *Packet Capture* e é o formato de ficheiro de capturas do Wireshark

Para capturar pacotes com filtros:

```bash
$ tshark -i <interface> "tcp and host <ip_addr>"
```

Para obter estatísticas de conversas entre dispositivos, identificando quais dispositivos comunicaram entre eles mesmos:

```bash
$ tshark -r ficheiro.pcap -z conv,ip -q
```

Podemos também extrair o seu conteúdo para outro ficheiro (e.g. binário) com uma estrutura específica de modo a depois poder fazer uma análise detalhada:

```bash
$ tshark -r test.pcap -z conv,ip -q \ | sed 's/ kB/000/g' | sed 's/ MB/000000/g' | \ | grep "^[0-9]" | tr -d "[:alpha:],<>-" | sed "s/ \+/ /g" \ | awk '{print $9, $1, $2, $3, $4, $5, $6, $10}' | sort -n > conversas.dat
```

### NFStream

Pode também ser usado a esta *framework* do Python para extrair a informação dos fluxos de uma captura de pacotes feita:

```python
import argparse
from nfstream import NFStreamer

def main():

    parser=argparse.ArgumentParser()
    parser.add_argument('-r', '--readfile', nargs='?',required=True, help='input file')
    parser.add_argument('-w', '--writefile', nargs='?', help='output file')

    args=parser.parse_args()

    readfile=args.readfile

    if args.writefile is None:
        writefile=readfile.split('.')[0]+".csv"
    else:
        writefile=args.writefile
    print(writefile)

    my_streamer = NFStreamer(source=readfile,
                         decode_tunnels=True,
                         bpf_filter=None,
                         promiscuous_mode=True,
                         snapshot_length=1536,
                         idle_timeout=120,
                         active_timeout=1800,
                         accounting_mode=0,
                         udps=None,
                         n_dissections=20,
                         statistical_analysis=False,
                         splt_analysis=0,
                         n_meters=0,
                         performance_report=0)

    my_streamer.to_csv(path=writefile)

if __name__ == '__main__':
    main()
```

```bash
$ python baseNFStream.py -r ficheiro.pcap -w conversasNF.dat
```

## <mark style="background: #FFF3A3A6;">Prática 2: Data Processing</mark>

No *script* `basePktSampling.py`:
- `-i`: é para o ficheiro de entrada
- `-out`: é para o ficheiro de saída
- `-f`: é para o formato do ficheiro
	- `1` para ficheiro **com o mesmo formato que o fornecido**
	- `2` para ficheiro formato **tshark**
	- `3` para ficheiro formato **pcap**
- `-d`: intervalo de amostras em segundos
- `-c`: rede do cliente
- `-s`: rede do servidor

No *script* `basePktFeaturesExt.py`:
- w = janela de observação
- m = metodo
	- sequential
	- slide (com uma janela apenas)
	- slide (com várias janelas ao mesmo tempo)
- é feita mediana média desvio padrão para 4 colunas
	- upload de bytes
	- upload de pacotes
	- download de bytes
	- download de pacotes