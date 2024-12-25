
## ==Acrónimos==

| Acrónimo    | Definição                                           |
| ----------- | --------------------------------------------------- |
| **APCER**   | Associação Portuguesa de Certificação               |
| **AoC**     | *Attestation of Compliance*                         |
| **B2B**     | *Business-To-Business*                              |
| **B2C**     | *Business-To-Client*                                |
| **CNCS**    | Centro Nacional de Cibersegurança                   |
| **CTA**     | Comissão Técnica *Ad-hoc*                           |
| **DNP**     | Documento Normativo Português                       |
| **EMPD**    | Estrutura de Missão Portugal Digital                |
| **HSM**     | *Hardware Security Module*                          |
| **IPAC**    | Instituto Português de Acreditação                  |
| **IPG**     | Instituto Português da Qualidade                    |
| **INCM**    | Imprensa Nacional Casa da Moeda                     |
| **QNRCS**   | Quadro Nacional de Referência para a Cibersegurança |
| **PCI DSS** | *Payment Card Industry Data Security Standards*     |
| **PCI SSC** | *Payment Card Industry Security Standards Council*  |
| **POS**     | *Points of Sale*                                    |
| **PRR**     | Plano de Recuperação e Resiliência                  |
| **TS**      | *Technical Specification*                           |
| **ROC**     | *Report on Compliance*                              |
| **SAQ**     | *Self-Assessment Questionnaire*                     |
| **SMD**     | Selo de Maturidade Digital                          |

<div style="page-break-after: always;"></div>
## Agradecimentos

A conclusão desta dissertação, bem como da grande maioria deste período da minha vida académica, não seria possível sem a ajuda dos meus colegas de curso, aos quais sou imensamente grato.

Gostaria de expressar a minha gratidão a cada um(a) dos(as) senhores(as) pela colaboração, pelo apoio mútuo e pela troca de conhecimentos ao longo deste percurso. Juntos, enfrentamos desafios complexos, superamos obstáculos e compartilhamos experiências valiosas, enriquecendo a nossa jornada académica.

Além disso, gostaria de agradecer aos nossos professores e orientadores, que nos guiaram durante todo o processo. O seu conhecimento, dedicação e incentivo foram fundamentais para o sucesso deste projeto. A sua experiência e orientação ajudaram-nos a expandir os horizontes e a alcançar resultados de qualidade.

Também gostaria de agradecer às nossas famílias e amigos que nos apoiaram ao longo dessa jornada. O seu amor, paciência e encorajamento foram essenciais para enfrentarmos os desafios e mantermo-nos motivados durante os momentos mais difíceis.

Por fim, gostaria de agradecer à instituição académica pela oportunidade de realizar este projeto e pela formação de excelência que recebemos ao longo do curso. Estou profundamente grato por todas as oportunidades de aprendizado e crescimento que me foram proporcionadas.

A todos que contribuíram direta ou indiretamente para o sucesso deste projeto, meu mais sincero agradecimento. Aprendi muito com cada um de vocês e sou privilegiado por compartilhar essa jornada com pessoas tão talentosas e dedicadas.

Que esta dissertação de mestrado seja apenas o começo de uma carreira repleta de realizações e contribuições para a área da Cibersegurança.

Obrigado a todos!


## ==Introdução==

### Enquadramento

Este documento funciona como relatório do estágio curricular do curso de Mestrado em Cibersegurança (MCS) na Universidade de Aveiro (UA). O estágio visa aplicar e consolidar os conhecimentos adquiridos ao longo do percurso académico, através da evolução da maturidade de segurança da PRIO e garantia da conformidade com a atual legislação portuguesa.

### Motivação

Atualmente, a cibersegurança representa um papel crucial para a evolução e continuidade de negócio de uma empresa, num cenário onde as ameaças cibernéticas estão em constante evolução, garantir a resiliência operacional e a proteção dos sistemas de informação tornou-se prioridade para líderes de organizações em qualquer setor de atividade.

Segundo a ITSecurity, foi registado o maior aumento de ciberataques nos últimos dois anos
no segundo trimestre de 2024, com um **aumento em cerca de 25%** relativamente ao trimestre anterior, indicando que os mesmos estão tornando-se de cada vez mais frequentes.

Conforme o relatório de riscos de conflitos de 2024 do CNCS, para **81% dos profissionais** inquiridos no inquérito do CNCS, o **risco de uma entidade sofrer um incidente** de cibersegurança no ciberespaço de interesse nacional **aumentou**, enfatizando mais a frequência em **ataques de *phishing*/*smishing*, *ransomware* e engenharia social**, respetivamente.

Perante um cenário de **ameaças crescentes e cada vez mais diversificadas**, e a tendência para o **crescente aumento da dependência das tecnologias da informação e de comunicação** nas entidades públicas e privadas, torna-se essencial que estas **integrem a cibersegurança na sua cultura organizacional** como uma componente intrínseca à sua atividade.

Estes ataques são muitas das vezes mitigáveis através da adoção das **boas práticas de cibersegurança na rotina da empresa**. E a melhor forma de selar o compromisso da adoção destas práticas, e através da obtenção do Selo de Maturidade Digital.

Portugal, enquanto nação, tem trabalho em prol da **evolução** nesta área de grande relevância, alcançando uma nova posição de destaque no **Global Cybersecurity Index 2024** e destacando-se entre os países com **maior desenvolvimento em cibersegurança (*Tier 1 – Role-modelling*)**. A Prio enquanto empresa que prega evolução, irá acompanhar o resto de Portugal e superar as expectativas propostas.

### Objetivos

O estágio curricular envolve duas fases de focos distintos, porém de grande relevância para evolução da maturidade da segurança da empresa.

A primeira fase, que se prevê ser de execução mais célere, envolverá a avaliação dos passos necessários para alcançar o nível Prata do Selo de Maturidade Digital em Cibersegurança, assim como a colaboração para a sua obtenção. 

Já a segunda fase, que será mais prolongada, focar-se-á na implementação da *framework* PCI DSS, conforme a versão mais atualizada da norma. Esta fase abrangerá tanto pagamentos físicos (como cartões de crédito, débito, MBWay e outros) quanto pagamentos digitais (abrangendo plataformas de *e-commerce* e aplicações similares). Para ambas as modalidades de pagamento, será necessário realizar uma avaliação conforme a avaliação do nível de conformidade da organização. Com base nessa avaliação, será elaborado e implementado um plano de ação que vise a obtenção da certificação.

<div style="page-break-after: always;"></div>


## ==Estado-de-Arte==

### Selo de Maturidade Digital

#### O que é o SMD?

O Selo de Maturidade Digital (SMD) é uma certificação contida no plano de ação Portugal Digital, resultante de uma resposta consertada, a nível europeu, aos impactos da pandemia causada pela COVID-19.

A certificação de maturidade digital está acessível a qualquer organização, do setor privado ou público, que se pode certificar nas dimensões que considerar mais relevantes e/ou prioritárias para o seu negócio.

Os SMD pretendem a criação de **quatro normas de serviços** nas áreas de Cibersegurança, Acessibilidade, Privacidade e Proteção de Dados Pessoais e Sustentabilidade, onde cada uma delas representa **uma parte do documento normativo** onde são definidos os requisitos necessários para a obtenção da acreditação, denominado de **DNS TS-4577** (Documento Normativo Português). 

A certificação possui três níveis de maturidade, o nível bronze é aplicado às organizações de menor dimensão e com menores recursos humanos e técnicos a enfrentar riscos. O nível prata destinado a organizações com capacidades humanas e técnicas além das elementares, com média dimensão ou maior risco. O nível ouro é remetido às organizações com capacidade humana e técnica mais robusta, com grande necessidade de proteção da sua informação e criticidade da sua atividade.

A obtenção dos níveis mais elevados implicam a conformidade com os níveis inferiores e a certificação nas quatro dimensões, através da obtenção de uma **pontuação mínima em cada uma delas** corresponde à obtenção do **Selo Digital Global**.

#### Referências Legais e Regulamentares 

- Regulamento de Execução (UE) 2018/151, da Comissão, de 30 de janeiro de 2018:
	- Estabelece normas de execução no respeitante à especificação pormenorizada dos elementos a ter em conta pelos prestadores de serviços digitais na gestão dos riscos que se colocam à segurança das redes e dos sistemas de informação, bem como à especificação pormenorizada dos parâmetros para determinar se o impacto de um incidente é substancial.
- Regulamento de Cibersegurança (UE) 2019/881, do Parlamento Europeu e do Conselho, de 17 de abril de 2019:
	- Este Regulamento é relativo à ENISA (Agência da União Europeia para a Cibersegurança) e à certificação da cibersegurança das tecnologias da informação e comunicação que revoga o Regulamento (UE) n. 526/2013 (Regulamento Cibersegurança). Estabelece o enquadramento europeu para a certificação da cibersegurança, os procedimentos para criação de esquemas europeus de certificação da cibersegurança e determina os elementos a constar em tais esquemas.
- Diretiva NIS 2 (UE) 2022/2555, do Parlamento Europeu e do Conselho, a ser transposta para legislação:
	- Estabelece um quadro regulamentar comum no domínio da cibersegurança visando aumentar o nível de cibersegurança na UE, exigindo que os Estados-Membros da UE reforcem as capacidades de cibersegurança e introduzindo medidas de gestão dos riscos de cibersegurança e de notificação de informações em setores críticos, com regras relativas à cooperação, à partilha de informações, à supervisão e à execução.

#### Referências Normativas

A norma ISO/IEC 27001 especifica os requisitos para estabelecer, implementar, operar, monitorizar, rever, manter e melhorar um sistema de gestão de segurança da informação, bem como os requisitos para os controlos de segurança a serem implementados, conforme as necessidades e realidade da organização.

A norma ISO/IEC 17065 especifica os requisitos que se destinam a assegurar que os organismos de certificação gerem os processos de certificação de forma competente, consistente e imparcial, facilitando o reconhecimento desses mesmos organismos. Esta norma pode ser utilizada como documento de critérios para acreditação, avaliação e indicação de organismos por autoridades governamentais, proprietários de esquemas e outros.

#### Modelos de maturidade de cibersegurança

- [Cybersecurity Capability Maturity Model (C2M2) | Department of Energy](https://www.energy.gov/ceser/cybersecurity-capability-maturity-model-c2m2)
- [Cybersecurity Maturity Model Certification 2.0 Program | CISA](https://www.cisa.gov/resources-tools/resources/cybersecurity-maturity-model-certification-20-program)

#### O porquê da certificação do SMD?

A certificação do Selo de Maturidade Digital (SMD) apresenta várias vantagens face às restantes normas técnicas atualmente disponíveis em Portugal. Uma das principais é a existência de **incentivos financeiros**. À data da publicação do presente relatório, as entidades certificadas podem beneficiar de um incentivo suportado pelo PRR, no valor de **1.686,00 €** (acrescido de IVA à taxa legal em vigor), aplicável igualmente às quatro dimensões dos Selos de Maturidade Digital e aos três níveis de maturidade.

Outro benefício significativo é o seu **âmbito nacional**. A norma DNS TS-4577 foi desenvolvida pela Comissão Técnica, coordenada pelo Centro Nacional de Cibersegurança (CNCS), com base em normas ajustadas às necessidades e especificidades do contexto português. Este processo está alinhado com regulamentações e legislações nacionais, como o Quadro Nacional de Referência em Cibersegurança (QNRCS), o Roteiro para as Capacidades Mínimas de Cibersegurança e as Recomendações Técnicas do CNCS.

Adicionalmente, o SMD apresenta um **custo reduzido** em comparação com normas internacionais, como a ISO/IEC 27001, tornando-o uma solução mais económica. Por fim, destaca-se a sua **maior escalabilidade**, permitindo que as organizações progridam na sua maturidade digital, passando de um nível de certificação bronze para prata, por exemplo, estando também alinhado com alguns aspetos das normas internacionais.

#### Entidades Envolventes

Esta iniciativa foi realizada em parceria com várias entidades-chave. O **Instituto Português de Acreditação (IPAC)** e o **Instituto Português da Qualidade (IPQ)** desempenharam o papel de entidades certificadoras, enquanto a **Imprensa Nacional Casa da Moeda (INCM)** participou no desenvolvimento do projeto, com o acompanhamento da **Estrutura de Missão Portugal Digital (EMPD)**.

Concretamente o **Selo de Cibersegurança**, contou com a contribuição do **Centro Nacional de Cibersegurança (CNCS)** para a definição dos requisitos técnicos a serem implementados pelos candidatos. Além disso, o CNCS teve uma participação crucial na elaboração do esquema de certificação, desenvolvido no âmbito da Comissão Técnica de Normalização CTA 041 «Selos digitais», sob a coordenação do IPQ, o que resultou na **publicação da norma** DNP TS 4475-1:2021.

Embora o Selo de Cibersegurança não faça parte do Quadro Nacional de Certificação da Cibersegurança, o CNCS mantém a responsabilidade pela adequação e atualização dos requisitos técnicos em conformidade visando cibersegurança. O CNCS também colabora com o IPAC nas atividades de acreditação dos organismos de certificação envolvidos no processo.

#### Selo de Cibersegurança

A certificação para obtenção do Selo Digital de Cibersegurança baseia-se no QNRCS e **específica os requisitos técnicos a ser implementados** em todos os locais e processos da organização **onde há recurso a tecnologias de informação e comunicação**.

O principal objetivo destes requisitos é **mitigar muitos dos riscos físicos e digitais a que as organizações estão expostas**, contribuindo para o aumento da segurança da informação e proteção das empresas.

Como riscos associados a cibersegurança podem comprometer **outros processos da empresa**, o âmbito de certificação deve abranger a totalidade das atividades da organização em **todos os locais**.

Empresas que possuam esta certificação têm vantagens em relação a empresas ainda não acreditadas, nomeadamente na confiança transmitida em relações B2B ou B2C, garantindo a integridade da marca e melhorando a sua imagem perante o mercado e sociedade.
#### Ciber Higiene

Os controlos presentes na certificação do Selo Digital de Cibersegurança, na sua maioria, são referentes aos hábitos e boas práticas de segurança por parte dos colaboradores da empresa, também denominado de ciber higiene. A responsabilidade pela cibersegurança é do encargo das pessoas e não da tecnologia, assim como para a prevenção de micro-organismos maliciosos entrarem no nosso sistema imunitário devem ser mantidos hábitos de higiene diários.

As práticas de ciber higiene envolvem coisas como o uso de palavras-passe fortes para proteger os sistemas, realização de cópias de segurança, realização de atualizações regulares de *software* e sistemas operativos e ter os devidos cuidados com a segurança física.

### PCI DSS (*Payment Card Industry Data Security Standard*)

#### O que é PCI DSS?

É uma norma de segurança, publicada em 2006, que visa a proteção dos métodos de pagamento. O PCI DSS aplica-se aos pagamentos físicos, referentes às transações realizadas em postos de venda (POS) via terminais de pagamento, e aos pagamentos _online_, referentes a sítios na _internet_ onde os dados de pagamento são inseridos digitalmente. O cumprimento desta norma contribui significativamente para a salvaguarda das informações de pagamento sensíveis e para o desenvolvimento de soluções de pagamento mais seguras.

#### Entidades envolventes

As diretrizes desta norma foram desenvolvidas por cinco empresas que fornecem soluções de pagamento, sendo estas a VISA, American Express, Mastercard, Discover e JCB formando o PCI SSC (*PCI Security Standards Counci*l). 

Estas empresas representam uma maioria quase absoluta no mercado. O facto de a sua presença ser tão forte e da necessidade de que todos os sistemas envolvidos nas soluções de métodos de pagamento sejam interoperáveis implica a criação de um único padrão a ser seguido, desenvolvido por um ecossistema unificado na indústria de pagamentos.

![[Pasted image 20241019115905.png]]

Além disso, os requisitos do PCI DSS referenciam recomendações e controlos de organizações externas fidedignas e com grande relevância no tema de segurança da informação como o NIST, ENISA, FIDO ALLIANCE, ISO e OWASP.
#### Conformidade

Encontra-se em conformidade quem seguir os controlos correspondentes ao seu nível de conformidade. Existem quatro níveis para as organizações comerciantes, definidos com base no volume anual de transações de crédito ou débito processadas. O nível quatro é o nível mais baixo correspondente a empresas que tratam abaixo de 20 mil transações e o nível um é o nível mais alto correspondente a empresas que tratam acima de seis milhões de transações ao ano.

Apenas o nível um necessita de uma auditoria feita por um QSA (_Qualified Security Assessor_) sendo este uma entidade qualificada para validar a adesão com o PCI DSS, e da elaboração de um ROC (_Report on Compliance_). Para os restantes níveis apenas é exigido o preenchimento de um SAQ (_Self-Assessment Questionnaire_). Este procedimento é feito anualmente cumprimento os requisitos presentes na versão mais atualizada da norma. Além disso, é efetuado de maneira trimestral um _scan_ de vulnerabilidades às aplicações internas entidades aprovadas (ASVs) verificando a conformidade de um dos requisitos. No momento da auditoria, deve ser apresentando o registo de evidências de pelo menos três meses previamente.

Apesar de não existir diretamente uma obrigatoriedade jurídica, não conformidade com o padrão de segurança de dados do setor de cartões de pagamento afeta clientes e comerciantes. Para os clientes, a não conformidade significa que os seus dados arriscam serem comprometidos, levando a roubo de identidade ou perda financeira. Para os comerciantes, apesar de não existir penalizações legais diretas, a não conformidade pode resultar no não cumprimento diligência exigida por diretivas europeias, em multas por parte das empresas de cartões de pagamento, ações legais e danos à reputação.

##### Princípios de conformidade

Existem **seis princípios** centrais no PCI DSS, estes sumarizam os obstáculos mais importantes na segurança da informação, sendo descritos de forma mais detalhada pelos 12 requisitos.

**Construção e manutenção uma rede segura** é um princípio essencial para a proteção das informações. Isso envolve a instalação de _firewall's_ para resguardar os dados dos titulares de cartões e a configuração segura dos sistemas operativos e programas. Essas medidas estabelecem uma infraestrutura que previne acessos não autorizados desde o início.

Outro aspeto crucial é a **proteção dos dados do titular do cartão**. Isso inclui o armazenamento seguro dessas informações por meio de criptografia e a proteção da sua transmissão, evitando que dados sensíveis sejam intercetados. Assegurando a confidencialidade e a integridade das informações.

Além disso, é importante **manter um programa de gestão de vulnerabilidades**. Isso abrange a implementação de proteção contra _malware_ e a manutenção de sistemas seguros por meio de atualizações regulares. Isto permite a mitigação de riscos e a correção de vulnerabilidades antes haver possibilidade de serem exploradas.

A **implementação de controlos de acesso rigorosos** também se destaca. Limitar o acesso a dados apenas a pessoas autorizadas, exigir autenticação forte e restringir o acesso físico aos sistemas que armazenam informações sensíveis são ações que garantem um controle cuidadoso e monitorado.

Regularmente, as organizações devem **monitorizar e testar as suas redes**. Isso envolve o rastreamento de acessos aos dados, permitindo a rápida identificação de atividades suspeitas, além da realização de testes de segurança para validar a eficácia das medidas implementadas.

Por fim, é fundamental **manter uma política de segurança da informação**. Uma política abrangente deve ser desenvolvida e implementada, incluindo práticas essenciais para proteger informações sensíveis. Essa política serve como um guia para as ações e decisões relacionadas à segurança na organização.
<div style="page-break-after: always;"></div>

### Requisitos do PCI DSS

![[Pasted image 20241021114503.png]]

Estes requisitos são mais aplicados à vertente da segurança em pagamentos, no entanto, estes têm semelhança com normas como a ISO 27001 e o Selo de Maturidade Digital e diretivas como o NIS2 e o RGPD, sendo mais aplicados a práticas que promovem a segurança de sistemas de informação. Isto permite além de alcançar conformidade com o PCI DSS, poder cumprir em paralelo outras regulamentações, pois as políticas, controlos e registos de formações são semelhantes.

Quem cumprir estes requisitos e submeter a documentação necessária, ROC para empresas nível um e SAQ para as restantes, poderá proceder ao preenchimento do AOC (*Attestation of Compliance*).

<div style="page-break-after: always;"></div>

## ==Referências==

### Motivação

- (ref: Conferência "A Cibersegurança e a Continuidade de Negócio: Proteger e Gerir" 11/09/2024)
- https://www.itsecurity.pt/news/analysis/segundo-trimestre-de-2024-registou-maior-aumento-de-ciberataques-nos-ultimos-dois-anos
- https://observador.pt/2023/02/22/portugal-foi-o-terceiro-pais-europeu-com-mais-ataques-informaticos-a-que-a-ibm-respondeu-em-2022/
- https://www.itu.int/en/ITU-D/Cybersecurity/Documents/GCIv5/2401416_1b_Global-Cybersecurity-Index-E.pdf
- https://www.cncs.gov.pt/pt/observatorio/#relatorios

### Selo de Maturidade Digital

- https://portugaldigital.gov.pt/
- https://selosmaturidadedigital.incm.pt/
- https://www.ipq.pt/loja/normas/norma/2e2e512a-7fe5-ec11-bb3c-000d3ad7c2a0/
- https://www.cncs.gov.pt/docs/anexo-2-lista-de-referncias-legais-normativas-e-regulamentares.pdf
- https://www.cncs.gov.pt/pt/glossario/#linhasobservacao
- https://www.ua.pt/pt/ciberseguranca/boas-praticas-de-ciber-higiene
- https://www.cncs.gov.pt/pt/outras-certificacoes-relevantes/
- https://incm.pt/site/incentivos-financeiros-para-selos-de-maturidade-digital/
- [Projeto de regulamento relativo à implementação do regime jurídico da segurança do ciberespaço nas entidades da Administração Pública (diariodarepublica.pt)](https://files.diariodarepublica.pt/2s/2024/01/015000000/0002900035.pdf)

### PCI-DSS

- https://www.mastercard.com/global/en/business/overview/safety-and-security/security-recommendations/site-data-protection-PCI.html
- https://usa.visa.com/partner-with-us/pci-dss-compliance-information.html
- https://www.pcisecuritystandards.org/
- [PCI Security Standards Council – Protect Payment Data with Industry-driven Security Standards, Training, and Programs](https://www.pcisecuritystandards.org/document_library/)

Mais referências:
- [What is PCI DSS? | NordLayer Learn](https://nordlayer.com/learn/pci-dss/what-is-pci-dss/)
- [PCI Security Standards Council – Protect Payment Data with Industry-driven Security Standards, Training, and Programs](https://www.pcisecuritystandards.org/)
- [What is PCI DSS? Requirements and Compliance | TechTarget](https://www.techtarget.com/searchsecurity/definition/PCI-DSS-Payment-Card-Industry-Data-Security-Standard)
- [What Is PCI DSS? | Compliance Levels and Requirements | Akamai](https://www.akamai.com/glossary/what-is-pci-dss)
- [Data Compliance for Regulations Around the World (netapp.com)](https://bluexp.netapp.com/blog/data-compliance-regulations-hipaa-gdpr-and-pci-dss)
- [PCI DSS vs. ISO 27001: Similarities, differences, implementation, and certification | Advisera](https://advisera.com/27001academy/knowledgebase/pci-dss/)
- [PCI-DSS: o que é e porque é importante para a sua empresa - easypay](https://www.easypay.pt/blog/pci-dss/)
- [What Is PCI Compliance? PCI DSS Explained | Fortinet](https://www.fortinet.com/lat/resources/cyberglossary/what-is-pci-compliance)
- [PCI DSS Compliance Levels and Requirements for Your Business | Carbide (carbidesecure.com)](https://carbidesecure.com/resources/what-are-the-4-pci-dss-compliance-levels/)