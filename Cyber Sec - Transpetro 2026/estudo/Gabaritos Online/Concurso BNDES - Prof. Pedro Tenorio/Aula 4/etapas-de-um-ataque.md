# Footprinting

O footprinting (ou reconhecimento) é a primeira fase de um ataque cibernético ou teste de intrusão, focada em coletar o máximo de informações públicas e privadas sobre um alvo.
## O que é o Footprinting?
É o processo de mapear a "pegada digital" de uma organização ou sistema antes de realizar qualquer investida real. O objetivo é descobrir portas de entrada, tecnologias usadas, endereços de rede e até dados sobre funcionários.
## Tipos de Footprinting
- Passivo: Coleta dados sem interagir diretamente com o alvo. Usa redes sociais, buscas no Google (Google Hacking), registros DNS e consultas Whois. Não aciona alarmes de segurança.
- Ativo: Envolve contato direto com os sistemas do alvo. Usa comandos como traceroute, ping ou varreduras de portas. Pode ser detectado por sistemas de defesa

## Fingerprint
É uma parte do footprinting onde o objetivo principal é identificar o SO da vítima.

### Existem dois tipos principais de fingerprint

#### Passivo
Deduz o sistema operacional através da captura passiva de pacotes.

#### Ativo
Resposta direta do host


# Scanning (Varredura)

O Scanning (Varredura) é a segunda fase do ciclo de um ataque cibernético, ocorrendo logo após o reconhecimento inicial e antes da exploração da brecha.
Nesta etapa, o invasor usa ferramentas técnicas para examinar o alvo ativamente e mapear portas abertas, serviços ativos, sistemas operacionais e vulnerabilidades específicas na rede ou nos dispositivos da vítima.
## Como funciona o Scanning em um ataque
O processo de varredura busca transformar dados genéricos obtidos no reconhecimento em alvos reais e pontos de entrada utilizáveis. Ele costuma se dividir em três partes principais:
- Varredura de portas (Port Scanning): Descobre quais portas de comunicação estão abertas em um servidor ou IP (como portas 80 para web ou 22 para SSH), indicando quais serviços estão rodando.
- Varredura de rede (Network Scanning): Identifica quais endereços IP estão ativos em uma faixa de rede da empresa, mapeando a topologia dos computadores conectados.
- Identificação de vulnerabilidades (Vulnerability Scanning): Usa programas automatizados para cruzar os serviços encontrados com bases de dados de falhas conhecidas, revelando se o sistema está desatualizado ou mal configurado.
## Ferramentas comuns de varredura
- Nmap: O programa mais conhecido do mercado para mapeamento de redes e portas.
- Netcat: Utilizado para leitura e gravação de dados em conexões de rede.
- Scanners de vulnerabilidade: Ferramentas como Nessus ou OpenVAS que buscam falhas específicas nos softwares instalados.


# Enumeracao

A etapa de enumeração em segurança da informação e testes de invasão (pentest) é o processo de interagir ativamente com um sistema alvo para extrair informações detalhadas, como nomes de usuários, compartilhamentos de rede, grupos, portas ativas e versões de serviços.

Enquanto a varredura (scanning) descobre portas abertas e quais serviços rodam nelas, a enumeração vai além e aprofunda essa conexão para coletar dados úteis a futuras exploracoes.
## Principais Objetivos
- Mapear usuários: Identificar contas de usuários válidas no sistema ou domínio.
- Identificar recursos: Listar compartilhamentos de arquivos (SMB/NFS) e impressoras.
- Descobrir aplicações e diretórios: Achar caminhos ocultos em servidores web.
- Levantar versões de software: Ler banners e detalhes de serviços para cruzar com vulnerabilidades conhecidas.
## Ferramentas Comuns
- Nmap: Utilizado com scripts (NSE) para enumerar serviços específicos.
- Enum4linux: Focado em coletar informações de sistemas Windows e Samba/Linux.
- Gobuster / Dirb: Empregados na enumeração de diretórios e arquivos em servidores web.
- Netcat: Utilizado para conexões manuais e leitura de banners de serviços de rede.
## Como Evitar ou Mitigar
- Políticas de mensagens genéricas: Em telas de login, evite retornar se o usuário existe ou se a senha está errada; utilize respostas padronizadas (ex: "Usuário ou senha incorretos").
- Endurecimento (Hardening): Desativar banners informativos padrão em servidores e serviços de rede.
- Monitoramento: Utilizar IDS/IPS para detectar tráfego excessivo ou varreduras típicas de ferramentas de enumeração

# Ganho de Acesso (Access Gaining)

O Ganho de Acesso (Access Gaining) é a fase de um ataque cibernético onde o invasor efetivamente consegue entrar no sistema, rede ou aplicação alvo, explorando as vulnerabilidades descobertas nas etapas anteriores (como a de reconhecimento e varredura).

Esta etapa faz parte do núcleo do Ethical Hacking e do Cyber Kill Chain, representando o momento em que a invasão se concretiza.

## Principais Vetores de Ganho de Acesso

Os atacantes utilizam diferentes técnicas para obter o primeiro ponto de apoio (acesso inicial) em um ambiente:
- Exploração de Vulnerabilidades de Software: Uso de exploits para atacar falhas de segurança não corrigidas (como buffer overflows ou execução remota de código) em sistemas operacionais ou aplicações.
- Engenharia Social: Ataques de phishing via e-mail ou mensagens falsas para induzir usuários legítimos a entregar suas credenciais ou executar arquivos maliciosos.
- Ataques de Autenticação: Uso de força bruta (brute force), credential stuffing (testar senhas vazadas em outros sites) ou adivinhação de senhas fracas.
- Malware: Inserção de Cavalos de Troia (Trojans), ransomware ou keyloggers que abrem portas de comunicação para o atacante.
- Configurações Incorretas (Misconfigurations): Exploração de serviços expostos à internet sem senha, ou que ainda utilizam as credenciais padrão de fábrica (ex: admin/admin).

## O que acontece após o Ganho de Acesso?

Uma vez dentro do sistema, o nível de acesso inicial pode ser limitado (um usuário comum). Por isso, o atacante geralmente executa ações imediatas para consolidar o controle:
1. Escalação de Privilégios (Privilege Escalation): Abuso de falhas internas para subir o nível de acesso de "usuário comum" para "administrador" ou "root".
2. Manutenção de Acesso (Maintaining Access): Instalação de backdoors ou rootkits para garantir que ele possa voltar ao sistema mesmo se o computador for reiniciado ou se a senha inicial for alterada.
3. Movimentação Lateral: Exploração da rede interna a partir da máquina invadida para alcançar alvos mais valiosos, como servidores de banco de dados.

# Encobrimento de Rastros

O encobrimento de rastros é a etapa final de um ataque cibernético, usada pelo invasor para apagar evidências e dificultar investigações.

## As Etapas de um Ataque Cibernético

Um ataque segue um caminho organizado. As fases comuns incluem:

- Reconhecimento: Coleta de dados e varredura do alvo.
- Invasão Inicial: Acesso por falhas de segurança ou phishing.
- Movimentação Lateral: Exploração da rede em busca de dados.
- Ação/Impacto: Roubo de dados, criptografia ou interrupção.
- Encobrimento de Rastros: Limpeza de evidências.

## Técnicas de Encobrimento de Rastros

Para sumir com as provas, o invasor usa métodos específicos:
- Apagamento de Logs: Limpeza de registros de segurança no Windows ou remoção de arquivos em Linux para esconder acessos.
- Histórico de Comandos: Exclusão de linhas de comando digitadas no terminal.
- Timestomping: Mudança nas marcas de tempo de arquivos para enganar analistas de segurança.
- Desativação de Ferramentas: Desligar softwares de monitoramento ou alertas de SIEM.