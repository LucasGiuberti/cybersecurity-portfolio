# Cybersecurity & Threat Intelligence Portfolio

Bem-vindo ao meu portfólio de Cibersegurança. Este repositório documenta minha jornada e desenvolvimento técnico em operações de **Blue Team**, **Threat Intelligence** e **Análise de Vulnerabilidades**.

Aqui você encontrará relatórios técnicos, estudos de caso de reconhecimento (OSINT) e soluções de desafios práticos (CTF), todos mapeados com frameworks de mercado como **MITRE ATT&CK**.

## Estrutura do Projeto

- **`/real-world-analysis`**: Relatórios de reconhecimento passivo em alvos reais (anonimizados para conformidade ética).
- **`/ctf-writeups`**: Soluções detalhadas de laboratórios (TryHackMe, HackTheBox).

---

## Destaque Recente: Mapeamento de Superfície de Ataque (Target: Academic Sector)

Realizei um exercício completo de **Reconhecimento Passivo (Passive Recon)** contra uma infraestrutura real, focando na identificação de vetores de ataque sem interação direta com o alvo.

**Ferramentas Utilizadas:**
- `Amass` (Mapeamento de ASN e Subdomínios)
- `Shodan` (Banner Grabbing e CVEs)
- `Searchsploit` (Correlação de Exploits)

**Resultados Chave:**
- Identificação de **Shadow IT**: Servidores legados esquecidos na infraestrutura.
- Detecção de **Vulnerabilidade Crítica**: Apache 2.4.18 vulnerável a Privilege Escalation (CVE-2019-0211).
- Mapeamento via **MITRE ATT&CK**: T1596, T1590, T1190.

[Clique aqui para ler o relatório completo](./real-world-analysis/recon-target-academic.md)

---

## Disclaimer Ético
Todas as análises de alvos reais neste repositório foram realizadas utilizando métodos estritamente **passivos** (OSINT) ou em conformidade com programas de divulgação de vulnerabilidades (VDP/Bug Bounty). Nenhum teste de intrusão ativo ou ilegal foi realizado.
