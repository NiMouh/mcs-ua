## Questões Aula 5

**1. Considere a arquitetura PAM (Pluggable Authentication Modules) e a autenticação multimétodo (multi-factor). Explique de que forma é que a primeira facilita a concretização da segunda**

R: A arquitetura PAM permite a independencia de mecanismos de autenticação, o que facilita a implementação de MFA, uma vez que é possível utilizar vários métodos de autenticação em simultâneo.

**2. Considere a arquitetura PAM (Pluggable Authentication Modules). Explique de que forma é que a mesma dá total liberdade ao administrador de uma máquina para definir os métodos de autenticação de uma aplicação em particular.**

R: É dada a liberdade ao administrador para definir os métodos de autenticação de uma aplicação através da configuração dos ficheiros de *orchestration*.

**3. A infraestrutura PAM (Pluggable Authentication Modules) permite configurar de forma flexível e rápida a forma como se realizam diversas operações de autenticação que podem ser realizadas num sistema operativo Linux. Explique:**

  **a. Como se pode modificar apenas o processo de autenticação relativo a uma aplicação?**

R: É possível modificar apenas o processo de autenticação relativo a uma aplicação através da configuração de um ficheiro de *orchestration* específico para essa aplicação, /etc/pam.d/nome_da_aplicação.

  **b. De que forma é possível adicionar e parametrizar a execução de um novo mecanismo de autenticação?**

R: É possível adicionar e parametrizar a execução de um novo mecanismo de autenticação através da configuração de um novo módulo no ficheiro de *orchestration*, adicionando uma nova ação auth.