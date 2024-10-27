
## <mark style="background: #BBFABBA6;">Objetivos</mark>

- **Caracterização e identificação de perfis de uso de rede**:
	- Aquisição
	- Análise
	- Mineração de dados (*Data Mining*)
- **Prevenção de deteção de intrusões de rede**:
	- Vetores de ataque
	- Mecanismos de proteção
	- Deteção de anomalias conhecidas
	- Deteção de anomalias comportamentais

## <mark style="background: #FFF3A3A6;">Tópico 1: Conhecimento Situacional (Situational Awareness)</mark>

Conhecimento, perceção e antecipação de ameaças de segurança que afetam diretamente a rede, os riscos que introduzem e a mitigação de comportamento malicioso.

Isto é feito em **fases**:
1. **Aquisição de dados**
2. **Processamento de dados**
3. **Criação de perfis de comportamento**
4. **Classificação desses perfis**
### Tipos de *Awareness*

- **Direto**: observação apenas
- **Indireta**: por análise de reações a eventos

### Modos de *Awareness*

- **Correlação**: Análise conjunta de múltiplas fontes de dados para detetar padrões escondidos e relações 
	- **Problema**: *Big Data Problem*, é preciso abundância de dados para ter uma análise precisa
- **Previsão**: Deteção de padrões ao longo de um tempo
	- **Problema**: *Black Swan Problem*, um evento que nunca foi observado não consegue ser previsto

> [!warning]
> Ambas as abordagens entram num ciclo de **dedução** da solução, **validação** dos resultados e **correção** de problemas.

### Tendência (*Bias*) Observacional 

Os dados são capturados e analisados de modo a **confirmar observações anteriores** e **crenças**, **não considerando** o resto dos dados.

![[Survivorship-bias.svg.png|600]]

> [!example]
> Blindagem dos aviões feita com base nos lugares onde foram **por norma** acertados, **desconsiderando** os restantes lugares.

Tem impacto sobre como os dados são:
- Colecionados
- Analisados

>[!important]
> Isto impede a **descoberta de ameaças desconhecidas**.

### Ameaças persistentes (APTs)

- Tem como foco organizações especifica
- Explorar novas vulnerabilidades com novas ferramentas
- O objetivo é obter grande impacto (roubo, disrupção ou ambos)
- Usa métodos *stealth*
	- Aprende comportamentos normais
	- Executa ataques de mímica
	- Ajusta a tática com base nas defesas

### Ataques

Um ataque tem as seguintes fases:
1. Aquisição de conhecimento
2. Infiltração
3. Aprendizagem
4. Propagação
5. Agregação
6. Exfiltração

Os ataques são feitos de maneira **incremental**, via escalada de privilégios. Informação pública abre portas para informação privada e acesso a domínios protegidos (Infiltração).

> [!note]
> Para implementar as diferentes fases de ataque, **máquinas legitimas têm que estar comprometidas**.

A **infiltração** pode ser feita:
- Abusando remotamente de utilizadores lícitos (e.g. *phising*, *vishing*)
- Remotamente mediante ações do atacante (e.g. exploração de vulnerabilidades na rede/sistema).
- Interação física (e.g. *wire-tapping*, portas USB)

A **propagação** usa um conjunto de metodologias:
- Exploração de credenciais
- Falsificando utilizadores e sistemas
- Exploração de vulnerabilidades

A **agregação** e **exfiltração** envolve transferência de dados M2M (*machine-to-machine*), isto pode ser feito:
- Internamente (Agregação)
- Externamente (Exfiltração)
### Desafios

Defesas de rede/sistemas tradicionais **não conseguem** garantir a segurança total das máquinas, **nem a prevenção de infiltração**:
- Liberdade do utilizador vs Segurança vs Confidencialidade
- Novas ameaças aparecem a toda hora

Tendo como solução:
- Tentar detetar o ataque nas fases mais importantes
	- Propagação
	- Agregação e Exfiltração
- Monitorização da rede e dos sistemas
## <mark style="background: #FFF3A3A6;">Tópico 2: Aquisição de Dados (Data Acquisition)</mark>

### Dados

Para obter este conhecimento da condição da rede é necessário a **aquisição de dados**, **monitorizando** redes e sistemas de modo a otimizar os serviços e a contra-atacar eventos anómalos.

### Tipos de dados
#### Qualitativos

**Informação descritiva**, referindo-se a coisas que podem ser observadas:
- Mensagens de Erro;
- Endereços comunicados;
- Tipos de pacotes;
- etc.

>[!example]
>`00:01:23.4566 – IP Packet [from A to B with 64 bytes]`
>`21:04:23.4566 – Error [id 404]`
#### Quantitativos 

Qualquer informação que pode ser **medida**, em termos estatísticos:
- Número de pacotes;
- Número de fluxos;
- Duração de fluxos;
- etc.

>[!example]
>**Packets sent:** 5467
>**Bytes seen in the last 10 minutes:** 18471947

### Origem dos dados

Existem várias fontes possíveis de dados:
- **SNMP**
	- Aquisição de conhecimento sobre estados atuais de *nodes*/ligações/servidores
	- Utilização da máquina (e.g. temperatura, utilização do CPU)
- **Fluxos** (conversações)
	- Usado para caracterizar a quantidade de tráfego entre utilizadores/servidores
- **Captura de pacotes / DPI vs SPI**
- **Logs dos dispositivos**
- **Medições ativas (e.g. pings)**
	- Introduz entropia na rede e requer sincronização de *clocks*

### Formato de dados

Como os dados são guardados são de extrema importância na hora de avaliar uma captura de rede.

Tem que se ter em consideração fatores como:
- **Desempenho**
- **Tamanho**

> [!example]
> **Um ficheiro em formato binário irá ser mais compacto que um ficheiro JSON** com a mesma informação, pois este inclui caracteres separadores, indentação, entre outros fatores que podem aumentar exponencialmente o seu tamanho.

### Estrutura de dados

A escolha na forma de como os dados estão estruturados irá ter influência na hora do tratamento dos mesmos e consequentemente na capacidade de deteção de ameaças.

Tem que se ter em consideração fatores como:
- **Tempo**
- **Procura**
- **Tamanho**

>[!example]
>Matriz N por M onde N representa os tipos de pacotes e o M representa o timestamp

O foco será a **análise de fluxos**, nisto temos:
- **Fluxos maliciosos**: não é necessário a análise do fluxo por inteiro para a sua deteção
- **Fluxos normais com atividades anormais**: é necessário analisar o fluxo todo, e caracterizar o seu comportável ao longo dele todo.

### *Nodes*

Corresponde a qualquer dispositivo ou sistema ligado a uma rede.

Tem várias coisas que podemos extrair de um *node*:
- Core
	- *OS version*
	- *CPU load*
	- *Memory Usage*
	- *OS processes*
	- *Configuration*
	- *Dynamic Operations*
- Interface/link
	- *Link Bandwidth* 
	- *Throughput* 
	- *Packet drop* 
		- *Queue drop* 
		- *Packet corruption* 
		- *Link failure* 
		- *TTL expiration* 
	- *Queue delay*

### MIB (*Management Information Base*)

O conjunto de objetos geridos, utilizados para definir informações de equipamentos, e criado pelo fabricante.

>[!example]
>*UDP Module*
>- **ObjectID**: 1.3.6.1.2.1.7.1
>- **Name**: UDPInDatagrams
>- **Type**: Counter32
>- **Comments**: Number of UDP datagrams delivered to users.

## <mark style="background: #FFF3A3A6;">Tópico 3: Processamento de Dados (Data Processing)</mark>

Os dados vêm em diferentes **formatos** e **estruturas**, esses dados têm que ser **processados** para depois serem **tratados**.

Quanto **melhor** for feito este processo, **mais facilitado** será o propósito seguinte, envolvendo **menor custo** na sua leitura e extração de resultados.

>[!example]
>- Análise estatística
>- *Machine Learning*

### Modo ideal de apresentação

O resultado do processamento é crucial para a análise de ***features*** presentes nos dados.

> [!definition]
> ***Features* (características):** Propriedade de medida presente num *dataset*. 

Maioria dos dados monitorizados são **qualitativos** e **devem ser convertidos** para dados **quantitativos**.

>[!important]
>Este processo é chamado processo de **amostragem** (*sampling*).

Os eventos são contados num **intervalo de amostragem** (Δt).

>[!example]
>Invés de ter apenas uma lista de eventos, ter amostras agrupadas em cada 2 segundos ou em cada 4 segundos, e analisar esses grupos de eventos.

Idealmente é um Tuplo bidimensional, onde **N** representa o número de *features*, por **intervalo de tempo**.

>[!example]
> Consideremos um conjunto de dados com 3 *features* e 4 intervalos de tempo:
> - **T1**: (100 Mbps, 30 ms, 0.1%)
> - **T2**: (120 Mbps, 28 ms, 0.15%)
> - **T3**: (95 Mbps, 35 ms, 0.2%)
> - **T4**: (110 Mbps, 32 ms, 0.05%)

### Modelagem

Os modelos podem descrever:
- **Ações Únicas:** Representam situações isoladas em várias conversações na rede (e.g. um pacote enviado/recebido).
- **Comportamentos:** Representam um conjunto de situações isoladas que ao longo de um tempo geram um padrão.

>[!warning]
>Estes modelos **devem** permitir testar novos dados e tomar decisões periodicamente.

### Modelar Ações Únicas

![[Pasted image 20241012204150.png|center]]
### Modelar Comportamentos


![[Pasted image 20241012204217.png|center]]


>[!definition]
>***Model Inference***: é quando é feito previsões num modelo usando novos dados de entrada.

### Janela temporal

Representa os eventos presentes naquele intervalo de amostragem (o que aconteceu naquela altura). 

Nesta janela temporal podemos obter as *features* extraídas dessa janela e juntar a muitas outras de modo a invés de obter uma “imagem”, obter um “vídeo” dos eventos — **chamada janela de observação**.
#### Janelas Sequenciais

Janelas temporais que se sucedem sem sobreposição, onde a análise de uma janela só ocorre após o término da anterior.

>[!example]
>Assistir a um filme onde a cada 10 minutos é feita uma análise do bloco que vimos. Pode haver momentos em que não temos a perceção correta do que aconteceu até ver o próximo bloco de filme.


![[Pasted image 20241013125035.png|center]]

- **Vantagens**:
  - Simplicidade na implementação e análise.
  - Redução de sobrecarga computacional, já que há uma pausa entre as janelas.
  
- **Desvantagens**:
  - Perde-se a deteção de eventos que ocorrem entre janelas.
  - Maior latência para capturar mudanças rápidas.

#### Janelas em *Slides*

Janelas móveis que se sobrepõem, permitindo análises contínuas e atualizadas sem esperar o fim de uma janela para iniciar outra.

>[!example]
>Assistir a um filme onde a 5 minutos de filme, começamos a ver o próximo bloco de 10 minutos. Deste modo ficamos com uma ideia do que acontece e o que está para acontecer de modo a fazer uma previsão, não perdendo nenhum detalhe no momento da análise.

![[Pasted image 20241013125131.png|center]]

- **Vantagens**:
  - Captura eventos com maior precisão e rapidez.
  - Permite análise contínua e mais sensível a mudanças no padrão de eventos.

- **Desvantagens**:
  - Maior custo computacional, ao haver sobreposição de dados.
  - Pode gerar redundância de informações devido à repetição de dados entre janelas.

### Perfil de entidade

**Caracterização** da janela de observação **após múltiplas observações**.

![[Pasted image 20241013134608.png|center]]

Comparação entre perfis, permite ao modelo:
- **Classificar** entidades em grupos
- **Agrupar** entidades semelhantes
- **Detetar** comportamento anómalo
- **Prever** eventos futuros

Estes perfis são **definidos pelas *features* que cada entidade tem**, permitindo **classificar** e **discriminar** comportamentos e detetando comportamentos que por norma uma entidade com aquele perfil **não tem**.

![[Pasted image 20241013134912.png|center]]

### Métricas

- **Média**: A média é o valor central de um conjunto de dados. Permite identificar a tendência central de eventos ou padrões de tráfego numa rede.
- **Mediana**: O valor mediano divide os dados em duas metades. Ela permite detetar *outliers* (valores atípicos) e comportamentos atípicos em redes.
- **Variância**: Mede a dispersão dos dados em torno da média. Indica a volatilidade ou a diversidade de eventos na rede.
- **Desvio padrão**: É a raiz quadrada da variância e expressa a dispersão dos dados de forma mais compreensível. Ajuda a identificar variações significativas no comportamento da rede.
- **Quantis e Percentis**: Dividem os dados em partes iguais ou percentuais. Auxiliam na análise de distribuição de eventos e na identificação de *thresholds* (limites) críticos na rede.

### Estatísticas Descritivas

- **Covariâncias**: Mede como duas variáveis se movem juntas. Ajuda a identificar relações entre eventos ou métricas de rede.
- **Correlação do coeficiente**: Mede a força e a direção do relacionamento linear entre duas variáveis. Permite detetar dependências fortes entre parâmetros de rede.
- **Matriz de correlação**: Apresenta as correlações entre várias variáveis ao mesmo tempo. Facilita a identificação de padrões globais de interdependência entre eventos de rede.

### Análise de Periodicidade

A análise de periodicidade **identifica padrões** cíclicos **em séries temporais**. 

Em dados de comportamento humano, como acessos a sistemas, os padrões frequentemente mostram **pseudoperiodicidade**, onde os intervalos são irregulares, mas tendem a repetir.

#### Métodos para Análise de Periodicidade:

1. **Autocorrelação**:
   - Mede a semelhança entre um sinal e as suas versões atrasadas. Identifica picos regulares, indicando um período específico.

![[Pasted image 20241013141216.png]]

2. **Autocorreção de Máximos Locais**:
   - Foca em pontos altos da série temporal. A regularidade dos máximos locais ajuda a revelar a periodicidade, mesmo que seja irregular.

![[Pasted image 20241013140522.png]]

3. **Periodogramas**:
   - Mostra a energia do sinal ao longo das frequências. Picos em certas frequências indicam periodicidade, mas assume consistência nos dados.

![[Pasted image 20241013140630.png]]

4. **Escalogramas**:
   - Representa a análise de *wavelets*, capturando padrões em diferentes escalas. Útil para detetar pseudoperiodicidade, por revelar variações de periodicidade ao longo do tempo.

![[Pasted image 20241013140907.png]]


>[!definition]
>***Wavelets*** são funções matemáticas utilizadas para analisar sinais e dados. Permitem identificar padrões temporais e prever comportamentos futuros, como picos de uso durante horários específicos.

## <mark style="background: #FFF3A3A6;">Tópico 4: Perfis de rede (Network Profiling)</mark>

`Por lecionar...`