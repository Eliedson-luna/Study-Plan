# Footprinting

O footprinting (ou reconhecimento) é a primeira fase de um ataque cibernético ou teste de intrusão, focada em coletar o máximo de informações públicas e privadas sobre um alvo.
## O que é o Footprinting?
É o processo de mapear a "pegada digital" de uma organização ou sistema antes de realizar qualquer investida real. O objetivo é descobrir portas de entrada, tecnologias usadas, endereços de rede e até dados sobre funcionários.
## Tipos de Footprinting
- Passivo: Coleta dados sem interagir diretamente com o alvo. Usa redes sociais, buscas no Google (Google Hacking), registros DNS e consultas Whois. Não aciona alarmes de segurança.
- Ativo: Envolve contato direto com os sistemas do alvo. Usa comandos como traceroute, ping ou varreduras de portas. Pode ser detectado por sistemas de defesa

# Scanning (Varredura)

O Scanning (Varredura) é a segunda fase do ciclo de um ataque cibernético, ocorrendo logo após o reconhecimento inicial e antes da exploração da brecha.
Nesta etapa, o invasor usa ferramentas técnicas para examinar o alvo ativamente e mapear portas abertas, serviços ativos, sistemas operacionais e vulnerabilidades específicas na rede ou nos dispositivos da vítima.
## Como funciona o Scanning em um ataque
O processo de varredura busca transformar dados genéricos obtidos no reconhecimento em alvos reais e pontos de entrada utilizáveis. Ele costuma se dividir em três partes principais:
- Varredura de portas (Port Scanning): Descobre quais portas de comunicação estão abertas em um servidor ou IP (como portas 80 para web ou 22 para SSH), indicando quais serviços estão rodando.
- Varredura de rede (Network Scanning): Identifica quais endereços IP estão ativos em uma faixa de rede da empresa, mapeando a topologia dos computadores conectados.
- Identificação de vulnerabilidades (Vulnerability Scanning): Usa programas automatizados para cruzar os serviços encontrados com bases de dados de falhas conhecidas, revelando se o sistema está desatualizado ou mal configurado.
## Ferramentas comuns de varredura
• Nmap: O programa mais conhecido do mercado para mapeamento de redes e portas.
• Netcat: Utilizado para leitura e gravação de dados em conexões de rede.
• Scanners de vulnerabilidade: Ferramentas como Nessus ou OpenVAS que buscam falhas específicas nos softwares instalados.

# Gaining Access: 