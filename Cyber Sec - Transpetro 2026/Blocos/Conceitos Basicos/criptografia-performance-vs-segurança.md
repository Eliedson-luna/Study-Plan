# Sobre

Aqui busco resumir os conceitos de alguns métodos de criptografia.

## Criptografia Simétrica

Mesma chave para cifrar e decifrar. Algoritmos: AES, ChaCha20, 3DES (legado).

### Segurança
Forte contra ataques de força bruta com chaves de 256 bits (AES-256 é considerado seguro até contra computação quântica, reduzindo efetivamente para ~128 bits de segurança via algoritmo de Grover). O ponto fraco não é o algoritmo, é a distribuição da chave — como duas partes combinam a mesma chave sem um canal seguro prévio é o problema central que ela não resolve sozinha.

### Performance
Extremamente rápida, geralmente com aceleração via hardware (AES-NI em CPUs modernas). Usada para cifrar grandes volumes de dados — é o que roda por baixo do TLS depois do handshake, discos criptografados, VPNs.

## Criptografia Assimétrica

Par de chaves matematicamente relacionadas: pública (compartilhável) e privada (secreta). Algoritmos: RSA, ECC (Elliptic Curve), Ed25519.

### Segurança
Resolve o problema de distribuição de chave da simétrica — você nunca precisa transmitir a chave privada. Baseada em problemas matemáticos difíceis de reverter (fatoração de números grandes no RSA, logaritmo discreto em curvas elípticas no ECC). RSA está com os dias contados quando computação quântica amadurecer (algoritmo de Shor quebra fatoração); ECC também é vulnerável, mas exige curvas maiores para o mesmo nível de segurança comparado a RSA, o que já é uma vantagem de eficiência hoje.

### Performance
Ordens de magnitude mais lenta que simétrica (pense 100-1000x) devido às operações matemáticas envolvidas (exponenciação modular, operações em curvas). Por isso, na prática, é usada só para trocar uma chave simétrica ou assinar digitalmente — nunca para cifrar o payload inteiro. É exatamente o papel dela no handshake TLS: assimétrica estabelece confiança e negocia uma chave de sessão simétrica, que assume o trabalho pesado depois.

## Criptografia Homomórfica

Permite realizar operações matemáticas diretamente sobre dados cifrados, produzindo um resultado que, ao ser decifrado, é igual ao resultado da mesma operação nos dados originais em texto claro. Ninguém — nem quem processa — precisa ver o dado em claro.

### Segurança
Teoricamente é o santo graal para computação em nuvem com dados sensíveis (ex: hospital manda dados de pacientes cifrados para um provedor de nuvem processar sem nunca decifrar). Ainda é área de pesquisa ativa em termos de maturidade de implementação e resistência a ataques de canal lateral.

### Performance
Esse é o calcanhar de Aquiles. FHE (Fully Homomorphic Encryption) pode ser 1.000 a 1.000.000 de vezes mais lenta que operações equivalentes em texto claro, dependendo da operação e do esquema (CKKS, BFV, TFHE). Isso a torna, hoje, praticamente inviável para uso em tempo real de propósito geral — está restrita a nichos específicos (agregações estatísticas simples, machine learning federado em escala limitada) onde o ganho de privacidade justifica o custo computacional brutal.

## Hashing (função de hash criptográfica)

Não é criptografia reversível — não existe "decifrar" um hash. Transforma dado de qualquer tamanho em saída de tamanho fixo, de forma unidirecional. Algoritmos: SHA-256, SHA-3, BLAKE3.

### Segurança
Computacionalmente inviável encontrar duas entradas com o mesmo hash (resistência a colisão) ou reverter o hash para achar a entrada original. Usado para verificação de integridade e armazenamento de senhas (nunca a senha em si, o hash dela). Vulnerável a *rainbow tables* quando usado sem salt, especialmente para senhas.

### Performance
Muito rápida por design (SHA-256 processa gigabytes por segundo em hardware comum) — o que é bom para checksums, mas ruim para senhas, já que facilita ataques de força bruta em massa. Por isso senhas usam funções de hash propositalmente lentas (bcrypt, Argon2, scrypt), não hash genérico.

## HMAC (Hash-based Message Authentication Code)

Combina hash com uma chave secreta para gerar um código que garante integridade + autenticidade (prova que a mensagem não foi alterada e veio de quem tem a chave).

### Segurança
Diferente de um hash simples, que qualquer um pode recalcular, HMAC exige a chave secreta para gerar ou validar, protegendo contra adulteração por quem não tem a chave. Uso comum: tokens de API, webhooks (GitHub e Stripe assinam payloads com HMAC), JWT no modo `HS256`.

### Performance
Praticamente tão rápido quanto o hash subjacente — o overhead da chave é desprezível. Viável para validar cada requisição de API em tempo real sem impacto perceptível.

## Assinatura Digital

Cifra o hash da mensagem com a chave privada do emissor (não a mensagem inteira, seria lento). Qualquer um com a chave pública valida que só o emissor poderia ter gerado aquilo.

### Segurança
Garante autenticidade e não-repúdio — diferente da criptografia assimétrica "normal", onde se cifra com a pública do destinatário para confidencialidade, aqui se cifra com a privada do emissor para provar autoria. Mesma matemática, propósito invertido. Depende da segurança do algoritmo assimétrico subjacente (RSA, ECDSA, Ed25519) e da integridade da chave privada.

### Performance
Rápida porque assina apenas o hash (tamanho fixo pequeno), não o documento inteiro — evita o custo de cifrar payloads grandes com assimétrica. Ed25519 é hoje a escolha padrão por combinar assinaturas rápidas com chaves pequenas.

## Criptografia Pós-Quântica (PQC)

Algoritmos desenhados para resistir a ataques de computadores quânticos, que quebram RSA/ECC via algoritmo de Shor. Baseados em problemas matemáticos diferentes: reticulados (lattices), códigos, hashes multivariados. Padrões NIST: CRYSTALS-Kyber (troca de chave) e CRYSTALS-Dilithium (assinatura).

### Segurança
Resolve uma ameaça futura, não atual: computadores quânticos capazes de quebrar RSA/ECC em escala ainda não existem, mas dados cifrados hoje podem ser capturados e decifrados depois ("harvest now, decrypt later"), o que já justifica adoção antecipada para dados de longa vida útil.

### Performance
Chaves e assinaturas geralmente maiores que ECC equivalente, mas operações comparáveis ou até mais rápidas que RSA em alguns casos. Já adotada de forma híbrida (PQC + clássico simultaneamente) em TLS 1.3 por navegadores como Chrome, como transição de segurança sem abrir mão da compatibilidade atual.

## Compartilhamento de Segredo (Secret Sharing)

Divide um segredo (ex: chave mestra) em N pedaços, onde é preciso um número mínimo K deles (K de N) para reconstruir o segredo original. Nenhum pedaço isolado revela nada. Esquema clássico: Shamir's Secret Sharing.

### Segurança
Elimina o ponto único de falha de guardar uma chave crítica com uma só pessoa ou em um só local — comprometer menos que K pedaços não vaza nenhuma informação sobre o segredo. Uso típico: gerenciamento de chaves de root CA, cold wallets de criptomoeda distribuídas entre executivos, HSMs corporativos.

### Performance
Overhead computacional baixo na reconstrução; o custo real está na logística de distribuir e proteger os pedaços fisicamente/organizacionalmente, não no processamento.

## Searchable Encryption e ABE (Attribute-Based Encryption)

Nichos derivados da mesma motivação da homomórfica — computar ou buscar sobre dado cifrado sem decifrar tudo. Searchable encryption permite buscar palavras-chave em dados cifrados; ABE só permite decifrar se o usuário possui certos atributos (ex: "cargo=médico E departamento=cardiologia").

### Segurança
Reduz exposição de dado em claro em cenários de terceiro não confiável processando ou armazenando informação sensível, com controle de acesso granular por atributo no caso de ABE, sem precisar gerenciar uma chave por usuário.

### Performance
Mais rápida que FHE genérica, porque as operações suportadas são limitadas e específicas (busca por palavra-chave, decifração condicional) em vez de computação arbitrária — mas ainda mais lenta que criptografia simétrica/assimétrica tradicional, e menos madura em bibliotecas de produção.

## Tokenização

Tecnicamente não é criptografia — substitui dado sensível por um token sem relação matemática reversível; o mapeamento fica numa tabela segura, não numa fórmula. Muito usado em PCI-DSS para não guardar número de cartão real.

### Segurança
Quebrar a "matemática" não adianta nada porque não existe matemática ali — reverter só é possível consultando o sistema (vault) que guarda o mapeamento original, o que centraliza a proteção nesse sistema.

### Performance
Rápida para lookup, mas depende de uma consulta ao vault de tokenização (rede/banco), diferente de cifrar/decifrar que é puramente computacional local — isso pode introduzir latência de rede que criptografia tradicional não tem.

## Trade-off resumido

| Tipo | Segurança | Performance | Uso típico |
| --- | --- | --- | --- |
| Simétrica | Alta, mas depende de troca segura de chave | Muito rápida | Cifrar volume grande de dados |
| Assimétrica | Alta, resolve troca de chave | Lenta | Handshake, assinatura, troca de chave |
| Homomórfica | Máxima privacidade (nunca decifra) | Extremamente lenta | Nichos de computação sensível em nuvem |
| Hashing | Irreversível, mas vulnerável sem salt (senhas) | Muito rápida (ruim p/ senhas sem ajuste) | Integridade, armazenamento de senha |
| HMAC | Alta, integridade + autenticidade com chave compartilhada | Rápida (≈ hash) | Assinar payloads de API, webhooks |
| Assinatura digital | Alta, autenticidade + não-repúdio | Rápida (assina só o hash) | Certificados, commits assinados, contratos |
| Pós-quântica (PQC) | Resistente a ataque quântico futuro | Chaves maiores, custo comparável a RSA | TLS híbrido, dados de longa vida útil |
| Secret sharing | Elimina ponto único de falha | Baixo custo computacional | Chaves mestras, root CA, cold wallets |
| Searchable / ABE | Reduz exposição a terceiro não confiável | Lenta, mas menos que FHE | Busca cifrada, acesso condicional por atributo |
| Tokenização | Não reversível matematicamente (depende do vault) | Rápida, mas com latência de rede | Dados de cartão (PCI-DSS) |

