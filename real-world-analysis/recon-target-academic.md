# Relatório de Reconhecimento: Target Academic Sector

**Data:** 2026-01-21
**Alvo:** [INSTITUIÇÃO ACADÊMICA ALVO] (Anonimizado)
**Tipo:** Reconhecimento Passivo
**Ferramenta:** Amass, Shodan, Searchsploit
**Tags:** #recon #cybersecurity #amass #osint #cve #mitre

---

## 🔍 Metodologia (Passo a Passo)

1. **Resolução de DNS:** Utilize o comando `host target.edu` para identificar o IP do servidor web principal (`195.130.xx.xx`).
2. **Identificação de Infraestrutura (ASN):** Através do Shodan, identifiquei que o IP pertence ao **AS-XXXX** (Rede Acadêmica Educacional).
3. **Análise de Serviços:** O scan passivo revelou as portas **80 (HTTP)** e **443 (HTTPS)** abertas.
4. **Detecção de Versão:** O banner grabbing identificou o serviço **Apache httpd 2.4.18**.
5. **Análise de Vulnerabilidade:** Consultando o *CVEDetails* e o *ExploitDB*, confirmei que esta versão possui mais de 80 vulnerabilidades conhecidas devido à falta de atualizações.

---

## 🎯 Alvo Crítico Identificado: 195.130.xx.xx

**Fonte:** Shodan
**Status:** 🚨 Altamente Vulnerável
**Serviço:** Apache httpd 2.4.18 (Ubuntu)

### ⚠️ Análise de Risco
O servidor está rodando uma versão obsoleta do Apache (2.4.18), provavelmente em um sistema operacional legado (Ubuntu 16.04 EOL).

> [!CAUTION]
> **Vulnerabilidades Detectadas (CVEs)**
> O Shodan reportou **20 vulnerabilidades críticas**. Isso indica falta de patch management (gerenciamento de atualizações).
> * **Vetor provável:** Exploit público para Apache 2.4.18.
> * **Impacto:** RCE (Remote Code Execution) ou DoS (Denial of Service).

### Evidência Visual
*(Screenshot anonimizada do Banner Grabbing via Shodan)*
![Evidência Shodan Anonimizada](./images/evidence-shodan-blurred.png)
*(Nota: Certifique-se de borrar o IP real na imagem antes do upload)*

---

## 💣 Tabela de Exploits Potenciais (Searchsploit)

Abaixo estão os exploits disponíveis publicamente para a versão identificada, demonstrando o risco teórico.

| Título do Exploit (Vulnerabilidade) | Caminho (Path) | Tipo | Comando p/ Baixar |
| :--- | :--- | :--- | :--- |
| **Apache 2.4.17 < 2.4.38 - 'apache2ctl graceful' 'logrotate' LPE** | `linux/local/46676.php` | **Privilege Escalation** | `searchsploit -m 46676` |
| Apache + PHP < 5.3.12 / < 5.4.2 - cgi-bin Remote Code Execution | `php/remote/29290.c` | RCE | `searchsploit -m 29290` |
| Apache < 2.2.34 / < 2.4.27 - OPTIONS Memory Leak | `linux/webapps/42745.py` | Info Leak | `searchsploit -m 42745` |
| Apache mod_ssl < 2.8.7 OpenSSL - 'OpenFuck.c' Remote Buffer Overflow | `unix/remote/21671.c` | Overflow | `searchsploit -m 21671` |

---

## 🗺️ Mapeamento MITRE ATT&CK (Fase de Reconhecimento)

Abaixo estão as técnicas confirmadas durante a análise passiva do alvo:

| ID | Tática | Técnica | Contexto Prático |
| :--- | :--- | :--- | :--- |
| **T1596** | Reconnaissance | *Search Open Technical Databases* | Utilização do **Shodan** para consultar bases de dados públicas e identificar serviços sem interação direta. |
| **T1590.002** | Reconnaissance | *Gather Victim Network Info: DNS* | Utilização do **Amass** para enumerar subdomínios, registros de e-mail (MX) e Nameservers. |
| **T1590.005** | Reconnaissance | *Gather Victim Network Info: IP Addresses* | Identificação do IP público (`195.130.xx.xx`) e correlação com o ASN (Bloco de Rede). |

---

## 🛡️ Defesa Sugerida (Blue Team Perspective)

> [!TIP]
> **Estratégias de Mitigação e Detecção**
>
> **1. Contra Exploração (T1190):**
> * **Ação Crítica:** Implementar *Patch Management* urgente. O Apache deve ser atualizado da versão 2.4.18 para a mais recente estável.
> * **Contenção:** Se não for possível atualizar agora, isolar o servidor atrás de um WAF (Web Application Firewall) para bloquear tentativas de exploit conhecidas.
>
> **2. Contra Reconhecimento (T1590/T1596):**
> * **Desafio:** Detectar essa fase é extremamente difícil, pois o tráfego ocorre em bases de dados externas (Shodan, Whois) e não na rede da organização.
> * **Solução (EASM):** A única forma de "detectar" é fazer o mesmo que o atacante: monitorar continuamente sua própria superfície de ataque externa (External Attack Surface Management).