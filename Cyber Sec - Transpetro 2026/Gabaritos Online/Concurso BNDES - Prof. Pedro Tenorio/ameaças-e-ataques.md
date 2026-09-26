
## Vulnerabilidade

 falha ou fraqueza em um sistema (código, configuração, processo, ou até comportamento humano) que pode ser explorada. É uma propriedade estática do sistema — existe independente de alguém tentar explorá-la ou não. Ex: uma função que não sanitiza input antes de montar uma query SQL.

## Ameaça (threat)
 Agente ou evento com potencial de explorar uma vulnerabilidade e causar dano. Pode ser um atacante humano, malware, um evento natural (incêndio no datacenter) ou até erro humano acidental. Ameaça sem vulnerabilidade correspondente não gera problema prático.

## Risco 

Probabilidade de uma ameaça explorar uma vulnerabilidade, multiplicada pelo impacto que isso causaria. É a métrica que orienta decisão — normalmente calculado como algo como Risco = Probabilidade × Impacto. Risco é o que você prioriza e gerencia; vulnerabilidade e ameaça são os insumos desse cálculo.

## Brecha (breach)

O evento realizado — a exploração de fato acontecendo. É quando a ameaça consegue explorar a vulnerabilidade com sucesso e há comprometimento real (dados vazados, sistema comprometido, acesso não autorizado obtido). Diferente de "incidente" em alguns frameworks (incidente pode incluir tentativas sem sucesso), brecha geralmente implica que o dano ocorreu.

## Mitigação 

Ação tomada para reduzir o risco — seja reduzindo a probabilidade (corrigindo a vulnerabilidade, ex: patch, WAF, input validation), reduzindo o impacto (segmentação de rede, backups, criptografia em repouso), ou ambos. Mitigação nunca elimina risco a zero; ela reduz a superfície ou a severidade.