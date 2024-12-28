
## <mark style="background: #BBFABBA6;">Objetivos da Cadeira</mark>

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

- **Direto**: observação apenas (interações com os sistemas, ambiente ou dados)
	- Isto pode ser feito analisando logs, visualizando a atividade na rede, ou observando eventos.
- **Indireta**: por análise de reações a eventos
	- Avaliando o impacto do que foi gerado de um evento ou incidente, como mudanças de comportamento, e desempenho do sistema.

### Modos de *Awareness*

- **Correlação**: Análise conjunta de múltiplas fontes de dados para detetar padrões escondidos e relações 
	- **Problema**: *Big Data Problem*, é preciso abundância de dados para ter uma análise precisa
- **Previsão**: Deteção de padrões ao longo de um tempo
	- **Problema**: *Black Swan Problem*, um evento que nunca foi observado não consegue ser previsto

> [!warning]
> Ambas as abordagens entram num ciclo de **dedução** da solução, **validação** dos resultados e **correção** de problemas.

Todas as fontes de dados são aceitáveis e **nunca deve ser assumido a irrelevância dos dados**. Para o contexto de análise, o **tempo é de extrema importância**, podendo ser relativo ou absoluto, por definir a sua ocorrência num instante específico e é parte de uma sequência de eventos.
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

### Ameaças Persistentes Avançadas (*APTs*)

- Tem como foco organizações especifica
- Explorar novas vulnerabilidades com novas ferramentas
- O objetivo é obter grande impacto (roubo, disrupção ou ambos)
- Usa métodos *stealth*
	- Aprende comportamentos normais
	- Executa ataques de mímica
	- Ajusta a tática com base nas defesas

### Tipos de Ataques Comportamentais

Alguns dos ataques feitos, são difíceis de serem classificados corretamente e exigem algum tipo de análise da forma como o utilizador interage com o sistema:

| **Ataque**                  | **Descrição**                                                                                                 | Ter atenção a                                                                                                                                                                                                                                                                                                                                       |
| --------------------------- | ------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ataque de Disrupção (DoS)   | Disrupção de serviço via tráfego gerado em abundância por múltiplos dispositivos, afetando a disponibilidade. | - Picos de tráfego destino em comparação com padrões normais <br><br>- Alterações súbitas na periodicidade e duração de conversações mais curtas<br><br>- Múltiplos pedidos simultâneos para o mesmo serviço de várias origens<br><br>- Distribuição homogênia de ASNs                                                                              |
| Exfiltração de dados        | Exportação intencional e não autorizada de dados de um dispositivo para um destino externo                    | - Variação no volume de tráfego enviado para endereços externos  <br><br>- Conexões com destinos anômalos ou desconhecidos<br><br>- Presença de pseudoperiodicidade no envio de informação para o exterior.<br><br>- Inspecionar os dados para padrões ou conteúdos suspeitos (e.g., transferências de grandes ficheiros)                           |
| _Ransomware_                | Negação de acesso a dados de um utilizador ou organização via encriptação                                     | - Monitorizar logs em busca de múltiplas modificações ou exclusões de ficheiros num curto espaço de tempo  <br><br>- Verificar a criação de ficheiros com extensões incomuns ou encriptadas  <br><br>- Identificar tentativas de acesso a backups                                                                                                   |
| Command & Control (C2)      | Comunicação de dispositivos comprometidos com um servidor de controlo                                         | - Monitorizar processos em execução na máquina por longos períodos  <br><br>- Identificar conexões regulares ou anómalas para IPs externos  <br><br>- Presença de pseudoperiodicidade no envio de informação para o exterior.<br><br>- Analisar padrões de tráfego fora do horário habitual                                                         |
| Mineração de cripto-moedas  | Utilização não autorizada de recursos computacionais para minerar cripto-moedas                               | - Desempenho da máquina (CPU, GPU, temperatura)  <br><br>- Processos que consomem recursos elevados de forma contínua<br><br>-Aumentos súbitos no consumo de energia ou desempenho                                                                                                                                                                  |
| Ataque homem no meio (MITM) | Interceção da comunicação e dados trocados entre máquinas                                                     | - Alterações anómalas na latência das conexões <br> <br>- Inspecionar tráfego para identificar respostas duplicadas ou retransmissões incomuns  <br><br>- Detectar alterações em certificados SSL ou assinaturas de comunicação                                                                                                                     |
| Acesso Indevido             | Acesso externo à rede utilizando credenciais válidas comprometidas                                            | - Acessos de localizações geográficas incomuns (GeoIP)  <br><br>- Tentativas de acesso fora do horário laboral  <br><br>- Múltiplas autenticações de locais diferentes para a mesma conta (impossible travel)  <br><br>- Tentativas de *brute force* ou *password-spraying*  <br><br>- Correlacionar tentativas de acessos suspeitos entre serviços |

### Fases de um Ataque

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

A solução consiste em:
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
>- `00:01:23.4566 – IP Packet [from A to B with 64 bytes]`
>- `21:04:23.4566 – Error [id 404]`
#### Quantitativos 

Qualquer informação que pode ser **medida**, em termos estatísticos:
- Número de pacotes;
- Número de fluxos;
- Duração de fluxos;
- etc.

>[!example]
>- **Packets sent:** 5467
>- **Bytes seen in the last 10 minutes:** 18471947

### Formato dos dados

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

### Modos de aquisição de dados

- **Aquisição Passiva:** Observação e análise do tráfego existente na rede, sem realização tráfego sintético na rede.
- **Aquisição Ativa**: Envio de tráfego de teste ou a realização de transações sintéticas na rede para obter métricas

| **Exemplos de aquisição**                                         | **Propósito**                                                                                                                                  | **Usado para Obter**                                                                                                                                                                                     | Usado para detetar                                                                                     |
| ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **SNMP**                                                          | Aquisição de conhecimento sobre estados atuais de _nodes_ / ligações / servidores, usando métricas operacionais e logs dos dispositivos (MIBs) | - Temperatura e utilização de recursos (e.g., CPU, memória, discos).<br><br>- Estado de interfaces de rede (e.g., ativo/inativo, perdas de pacotes).<br><br>- Contagem de processos ou sessões ativas.   | - Ataque de negação de serviço distribuído (DDoS)<br><br>- Mineração de cripto-moedas                  |
| **Fluxos (e.g., NetFlow, sFlow)**                                 | Caracterizar a quantidade de tráfego entre utilizadores / servidores                                                                           | - Número de sessões criadas com o correspondente tempo.<br><br>- Protocolos utilizados entre origem e destino.<br><br>- Métricas de fluxos (bytes e pacotes enviados e recebidos).                       | - Ataque de negação de serviço distribuído (DDoS)<br><br>- Command & Control (C2)                      |
| **Captura de pacotes (e.g., DPI)**                                | Caracterizar utilizadores e serviços em curtos intervalos                                                                                      | - Identificação de IPs de origem/destino e portas associadas.<br><br>- Protocolos e serviços em uso (e.g., HTTP, DNS).<br><br>- Conteúdo trocado (e.g., ficheiros, credenciais, *payloads* específicos). | - Exfiltração de dados<br><br>- Ataque homem no meio (MITM)                                            |
| **Logs de dispositivos ou serviços (e.g., Syslog, Event Viewer)** | Adquirir conhecimento sobre o estado passado e o atual                                                                                         | - Registo de autenticações bem-sucedidas ou falhadas.<br><br>- Alterações na configuração do sistema.<br><br>- Eventos de inicialização ou falhas críticas nos serviços.                                 | - _Ransomware_<br><br>- Command & Control (C2)<br><br>- Acesso Indevido (dos serviços de autenticação) |
| **Medições ativas (e.g., one-way delay, jitter)**                 | Permite monitorizar a performance, injettando tráfego sintético e introduzindo entropia na rede e requer sincronização de _clocks_             | - Tempo de latência entre origem e destino.<br><br>- Medição de variações no atraso (jitter).<br><br>- Taxa de perda de pacotes em conexões específicas.                                                 | - Ataque homem no meio (MITM)<br><br>- Ataque de negação de serviço distribuído (DDoS)                 |

## <mark style="background: #FFF3A3A6;">Tópico 3: Processamento de Dados (Data Processing)</mark>

Os dados vêm em diferentes **formatos** e **estruturas**, esses dados têm que ser **processados** para depois serem **tratados**.

Quanto **melhor** for feito este processo, **mais facilitado** será o propósito seguinte, envolvendo **menor custo** na sua leitura e extração de resultados.

>[!example]
>- Análise estatística
>- *Machine Learning*

### Estrutura dos dados

O resultado do processamento é crucial para a análise de ***features*** presentes nos dados.

> [!definition]
> ***Features* (características):** Propriedade de medida presente num *dataset*. Representa a informação que é dada como *input* para um modelo descritivo.

#### Filtragem de Dados e Agregação (*Data Filtering and Aggregation*).

A filtragem de dados acontece quando, os dados em bruto são selecionados com base num determinado critério.

>[!example]
>1. Download/Upload
>2. TCP port 443, 80 or 22
>3. Fonte e Destino
>4. etc.

O resultado de um conjunto de filtragens gera um fluxo de dados (*datastream*). Este processo é chamado **agregação de dados** (*data aggregation*) consistindo em juntar várias informações de uma rede para criar uma visão mais clara e organizada do que acontece.

Com isto, são extraídos diversos eventos de um serviço, também denominados **interações**.

#### Amostragem de dados (*Data Sampling*)

Ocorre quando a maioria dos dados monitorizados são **qualitativos** e **devem ser convertidos** para dados **quantitativos**.

Os eventos são contados em **intervalos de amostragem** ou ***timestamps*** (Δt).

>[!example]
>Invés de ter apenas uma lista de eventos, ter amostras agrupadas em cada 2 segundos ou em cada 4 segundos, e analisar esses grupos de eventos.

Idealmente, é um Tuplo bidimensional, onde **N** representa o **número de *features***, por **intervalo de tempo**.

>[!example]
> Consideremos um conjunto de dados com **3 *features*** e **4 intervalos de tempo**:
> - **T1**: (100 Mbps, 30 ms, 0.1%)
> - **T2**: (120 Mbps, 28 ms, 0.15%)
> - **T3**: (95 Mbps, 35 ms, 0.2%)
> - **T4**: (110 Mbps, 32 ms, 0.05%)

### Modelagem

Os modelos podem descrever:
- **Ações Únicas:** Representam situações isoladas em várias conversações na rede
	- pacote enviado
	- pacote recebido
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
### Estatísticas Descritivas

Alternativamente a analisar cada ponto de dado individualmente, as estatísticas descritivas dão-nos uma visão geral, destacando padrões e características principais dos dados. 

Têm grande utilidade para sumarizar abundância de informação e identificar características principais de um conjunto de dados.

- **Média**: A média é o valor central de um conjunto de dados. Permite identificar a tendência central de eventos ou padrões de tráfego numa rede.
- **Mediana**: O valor mediano divide os dados em duas metades. Ela permite detetar *outliers* (anomalias) e comportamentos atípicos em redes.
- **Variância**: Mede a dispersão dos dados em torno da média. Indica a volatilidade ou a diversidade de eventos na rede.
- **Desvio padrão**: É a raiz quadrada da variância e expressa a dispersão dos dados de forma mais compreensível. Mede o quao distantes os valores encontram-se entre si.
- **Quartis e Percentis**: Dividem os dados em partes iguais ou percentuais. Auxiliam na análise de distribuição de eventos e na identificação de *thresholds* (limites) críticos na rede.
- **Covariâncias**: Mede como duas variáveis se movem juntas. Ajuda a identificar relações entre eventos ou métricas de rede.
- **Correlação do coeficiente**: Mede a força e a direção do relacionamento linear entre duas variáveis. Permite detetar dependências fortes entre parâmetros de rede.
- **Matriz de correlação**: Apresenta as correlações entre várias variáveis ao mesmo tempo. Facilita a identificação de padrões globais de interdependência entre eventos de rede.

### Características (*Features*) Observacionais

São as particularidades que podem ser extraídos através dos dados adquiridos. Estes parâmetros são fornecidos ao modelo observacional.

Estas podem ser:
- **Estatísticas Descritivas Independentes do Tempo**: Descrevem os dados sem considerar a sequência temporal.
    - Exemplos incluem a média, variância, desvio padrão, quartis, entre outros. Estas estatísticas fornecem uma visão geral dos valores médios e da dispersão dos dados.
- **Estatísticas Descritivas Dependentes do Tempo**: Consideram a sequência e a ordem dos dados ao longo do tempo.
    - **Relações temporais entre métricas**: Por exemplo, a média e o desvio padrão da duração de períodos de silêncio (momentos sem atividade) ou de atividade contínua. Estes períodos podem revelar comportamentos típicos ou incomuns.
    - **Componentes de Pseudoperiodicidade**: Permitem identificar padrões repetidos ao longo do tempo.
    - **Multifractalidade Temporal**: Deteta repetições de eventos similares em diferentes escalas de tempo, ajudando a identificar padrões de uso que se repetem irregularmente, mas com similaridades.

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
   - Mostra a energia do sinal ao longo das frequências. Picos em certas frequências indicam periodicidade, mas assume consistência nos dados (sinais quase estacionário, não variam).

![[Pasted image 20241013140630.png]]

4. **Escalogramas**:
   - Representa a análise de *wavelets*, capturando padrões em diferentes escalas. Útil para detetar pseudoperiodicidade, por revelar variações de periodicidade ao longo do tempo em dados não estacionários.

![[Pasted image 20241013140907.png]]


>[!definition]
>***Wavelets*** são funções matemáticas utilizadas para analisar sinais e dados. Permitem identificar padrões temporais e prever comportamentos futuros, como picos de uso durante horários específicos.


## <mark style="background: #FFF3A3A6;">Tópico 4: Perfis de rede (Network Profiling)</mark>

O uso de *machine learning* em deteção de redes é necessário em certos casos:
- Dados em abundância (muitos dados)
- Dados com múltiplas dimensões
### Processamento do Modelo

Estas são algumas coisas a tomar em conta para a implementação de soluções.
#### Complexidade do Modelo

Dados brutos são possíveis, mas aumenta a complexidade do algoritmo de *Machine Learning*.
#### Redução de Variáveis

Existem variáveis ao ser introduzidos no conjunto de dados geram ruído e podem pior a capacidade de decisão do modelo.

Possível solução para isto seria a implementação de PCA (*Principal Components Analysis*) para determinar quais as variáveis de maior importância. 

>[!important]
>Pode não ser recomendado para este caso onde as diferenças mínimas são as de maior relevância.
#### Normalização e Padronização

É importante ser os dados normalizados, para isso podemos usar métodos conhecidos:
- Min/Max
- Máximo do valor absoluto
- Z-Score (padronização)

| **Aspeto**                    | **Normalização**                                                                        | **Padronização**                                                             |
| ----------------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Objetivo**                  | Trazer os valores de uma variável para um intervalo específico, geralmente entre 0 e 1. | Transformar os valores de uma variável para terem média 0 e desvio padrão 1. |
| **Sensibilidade a anómalias** | Sensível a outliers e ao intervalo dos dados.                                           | Menos sensível a outliers devido ao uso da média e do desvio padrão.         |
| **Uso**                       | Útil quando é essencial manter o intervalo original dos dados.                          | Eficaz quando os algoritmos assumem uma distribuição normal padrão.          |

>[!objetive]
>Isto permite remover o *Bias* manter o foco na correlação de variáveis.
#### Classificação vs. Deteção de anomalias.

Na avaliação de resultados, a classificação envolve ter um histórico vasto de todos os padrões, o que é difícil em redes, pois muitas das vezes para detetar ataques é preciso passar por eles. No caso de deteção de atividades desconhecidas, é feita uma deteção de anomalias, que requer conhecimento de padrões considerados normais.
### Aprendizagem Supervisionada vs. Não Supervisionada

**Num contexto real**, os **modelos supervisionados não são tão frequentes** neste contexto de prevenção de comportamentos maliciosos a nível da rede, pois por norma, não temos uma visão concreta quais dados são maliciosos e quais dados são benignos.

Além disso, mesmo que estejamos no contexto onde temos essa informação, um treino não supervisionado seria o mais adequado para deteção de atividades maliciosas desconhecidas (*anomaly based detection*).
### Perfilagem

Cada conjunto de N atributos em cada observação é visto como um ponto no Universo Euclidiano N-Dimensional.

Onde cada ponto:
- É classificado previamente para identificar comportamentos conhecidos.
- Quando chega um ponto novo, ele será classificado de duas maneiras
	- **Um ponto pertencente a um grupo**: consoante a distância euclidiana do ponto central de cada grupo definido.
	- **Um ponto anómalo:** distância euclidiana grande dos restantes grupos.
### *Ensemble*

Este método constrói múltiplos modelos de *Machine Learning* (normalmente com metodologias diferentes), utilizando o resultado de cada modelo na definição de um único resultado.

Isto permite:
- **Reduzir a probabilidade de erros individuais.**
- **Melhorar a identificação anomalias/comportamentos maliciosos subtis que poderiam passar despercebidos por modelos isolados.**
- **Adapta-se facilmente a novos dados, reconhecendo comportamentos maliciosos emergentes.**


**Exemplo:**
![[Captura de ecrã 2024-11-15 141603.png]]

### Avaliação de um Modelo

No processo de avaliação, o *dataset* é dividido em dois *subsets*:
- **Treino:** Criação de perfis de utilização
- **Teste:** Avalição de resultados

![[Pasted image 20241115141238.png]]

>[!important]
>Ao contrário de outros modelos de Machine Learning, a construção do *dataset* é feito numa **linha temporal** (*timestamps*), onde o conjunto de treino representa o passado e o conjunto de teste o passado-recente. 
>
>Logo a utilização de técnicas como *cross-validation* (e.g. K-Folds), **não são adequadas**.
### Métricas

Na avaliação do modelo, existem dois valores que definem a capacidade da sua previsão:
- **True Positives (TP):**
- **False Positives (FP):**

E dois valores que definem o nível de erro da sua previsão:
- **False Positives (FP)**
- **False Negatives (FN)**

>[!important]
>No momento de avaliação, os **falsos positivos** devem ser o **mais baixo possível**, pois assim não causa **ruído**.

>[!example]
>Métricas que se podem obter com este valores:
> - Accuracy=(TP+TN)/(TP+TN+FP+FN) 
> - Precision=TP/(TP+FP) 
> - Recall=TP/(TP+FN) 
> - F1-Score== 2*(Recall * Precision) / (Recall + Precision)


| **Data Type**                                                                               | **Recommended Enterprise Tools**                                                        | **Description**                                                                                                                |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Network Sessions and Connection Duration**                                                | **Darktrace**                                                                           | Monitors and analyzes the duration and frequency of network sessions, identifying anomalous patterns and suspicious behaviors. |
| **Ports and Protocols Used**                                                                | **Suricata**, **Palo Alto Networks Firewalls**                                          | Monitors ports and protocols in use, including WebSockets, to detect unusual or unauthorized traffic.                          |
| **Connection Attempts and Disconnections**                                                  | **Splunk**, **Elastic Stack (ELK)**, **QRadar** (SIEM)                                  | Logs established and closed connections, helping to identify the timing and frequency of activity on Discord.                  |
| **User Activity (Session Level)**                                                           | **SIEMs** (e.g., **Splunk**, **QRadar**), **Darktrace**                                 | Monitors session activity to provide an overview of user behavior over time.                                                   |
| **Identification of Shared Media Types**                                                    | **Next-Generation Firewalls** with **DPI** (e.g., **Palo Alto Networks**, **Fortinet**) | Uses deep packet inspection to identify media types (e.g., video, audio) shared, even in encrypted traffic.                    |
| **Daily and Weekly Activity Patterns**                                                      | **Splunk**, **Elastic Stack**, **Grafana**                                              | Analyzes temporal activity patterns to identify peak times and consistent behaviors.                                           |
| **Presence in Voice Channels**                                                              | **Next-Generation Firewalls** with continuous WebSocket monitoring support              | Monitors activity in voice channels via WebSocket session analysis, providing insights on user presence and engagement.        |
