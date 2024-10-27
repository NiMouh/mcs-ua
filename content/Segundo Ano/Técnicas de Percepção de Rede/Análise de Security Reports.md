## Fortinet Security Report 2024

### Estatísticas

- 53% das organizações que responderam ao inquérito não possuem confiança na segurança das suas aplicações
- 50% das organizações relatam comprometimento das suas aplicações no último ano
- 45% indicam incerteza do conhecimento de todas as aplicações presentes na organização
- 42% indicam incerteza no conhecimento de todas as APIs usadas na organização
- 45% indicam incerteza de comportamento de bots na organização
- 40% não conseguem detetar e remediar vulnerabilidades a tempo de comprometer a organização
- 56% usam firewalls para proteger as aplicações da organização indicante uma forte confiança na proteção das mesmas contra acessos não autorizados
- Existe um aumento de 11% na importância de WAF na segurança de API workloads

### As maiores preocupações são

- Deteção de ameaças
- Aplicações em *cloud*
- *Malware*

### Os vetores de ataque mais comuns

- Disseminação de Malware
- Stolen Credentials
- DDoS
- Exploração de vulnerabilidades

### Estratégia para alojamento de aplicações

- Cloud Hibrida
- On-Premises
- Cloud Privada

### Ataques Bot mais comuns

- Credential stuffing
- DDoS
- Card Fraud
- Web Scraping
- Spambot

### Recomendações

- Integrar WAFs (Web Application Firewalls)
- Integrar CWPP (Cloud Workload Protection Platforms)
- Integrar Multi-Factor Authentication (MFA)
- Implementar rate limiting e chaves de APIs para cada aplicação
- Monitorizar o desempenho das aplicações
- Proteger dados sensíveis (armazenados e em movimento)
- Uso de ferramentas de descoberta de aplicações (revelando hidden apps)
- Uso de ferramentas de inventário de APIs (Shadow API Scan)
- Implementação de abordagens contra ameaças de bots como browser fingerprinting, threat intelligence, analise compreensiva
- No desenvolvimento de software, o uso de pipelines CI/CD com verificações de segurança integradas
- Definição de controlos de acesso a APIs
- Treino e sensibilização


## Cloudflare Web Applications Security Report 2024

==PAREI NA PÁGINA 15==
### Security Key findings

- 37.1% dos ataques mais comuns em aplicações web são ataques DDoS
- As WAF comuns são usados para proteger tráfego de APIs, no entanto, não são suficientes para proteger contra novas ameaças a APIs
- Cerca de 22 minutos de exploração de CVEs após a publicação do PoC
- Uso de, em média, 47,1 scripts de terceiros em aplicações web e fazemos 49,6 conexões de saída para recursos externos.
- Uso de, em média, 11,5 HTTP Cookies em aplicações web empresariais
- Um terço de todo o tráfego é feito por bots e, cerca de, 93% dos bots são maliciosos
- O número de CVEs descobertos aumentou em 15% de 2022 para 2023
- Aumento em 93% anual de ataques DDoS pela camada de aplicação HTTP


### Exemplos de ataques em aplicações WEB e APIs

- The Anonymous Sudan group launched politically motivated DDoS attacks against banks, universities, hospitals, airports, social media platforms, government agencies, and others worldwide. 
- Cloudflare observed a record-breaking DDoS attack exploiting a vulnerability in the HTTP/2 protocol, launched by a botnet of only 20.000 machines that rotated IPs to avoid mitigation. 
- T-Mobile disclosed in early 2023 that it experienced a data breach of 37 million customer accounts via an exploited API

### Casos de uso comuns para regras

- [Link](https://developers.cloudflare.com/waf/custom-rules/use-cases/)

### Tendências de Zero-day

![[Pasted image 20240924174620.png|500]]

### Ataques DDoS

- [HTTP/2 Rapid Reset Attack](https://blog.cloudflare.com/zero-day-rapid-reset-http2-record-breaking-ddos-attack/)

### Recomendações

-  Automatic absorbing of malicious traffic as close as possible to the attack origin, to reduce end-user latency and business downtime 
- Unmetered, unlimited DDoS attack mitigations, without charging penalties for spikes in attack traffic 
- Centralized autonomous protections against all DDoS attack types
- Integrate a bot management service that accurately identifies bots at scale by applying behavioral analysis, Machine Learning, and fingerprinting to a diverse and vast volume of data. Also, that allows good bots, such as those belonging to search engines, to keep reaching your site while preventing malicious traffic.
