![[Redes Convergentes]]

Faz parte de um conjunto de soluções para mitigar falhas e problemas dentro de uma empresa. O Firewall analisa a política de segurança implementada pelo administrador da rede, liberando ou não o pacote
Funciona de maneira bidirecional, o que pode passar pela interface com origem interna, e o que pode entrar pela interface com origem externa 
Verifica se o pacote que está entrando na rede é compatível com o que saiu da rede
![[Captura de Tela 2024-10-17 às 08.16.41.png]]
## Primeira Geração: Firewall sem estado
- Analisa pacotes individualmente
- Todo pacote que entra e sai da rede é um novo pacote
## Segunda Geração: Filtros com estado
- Retém dados dos pacotes para coletar informações sobre uma conexão ou sessão
- IPTable é um firewall open source do Linux, onde implementa o paradigma de filtro com estado
- Não filtram a camada de aplicação, como o HTTP
## Terceira Geração: NGFW
(new generation firewall)
- Analisa e compreende informações de camada de aplicação
- Em geral, traz funcionalidades integradas, com IPS/IDS, Web Security...
- Cisco, Fortinet, Huawei e entre outras disponibilizam o hardware para maior segurança, com features avançadas de segurança
## ML-NGFW
- Vistos como uma nova categoria, incorpora modelos de ML para aprimoramento de técnicas de bloqueio e identificação de tráfego malicioso

## Mapeamento de Regras 
![[Captura de Tela 2024-10-17 às 08.24.00.png]]
Mapeamento **In** na interface
- Melhor interface para escolher o mapeamento de regras, já que o pacote é analisado antes de sair da rede, evitando movimento desnecessário do firewall caso necessário o bloqueio
Mapeamento **Out** na interface
![[Captura de Tela 2024-10-17 às 08.26.59.png]]

### Mapeamento as regras em um firewall primeira geração
- Toda regra que implementa a saída, tem que implementar a volta
- Protocolos UDP não tem ACK no seu cabeçalho
- Rota Default bloqueia qualquer pacote que não estiver nas regras
- O firewall percorre a tabela de orientado de cima para baixo

|   |   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|---|
|filtro|regra|acao|sentido|protocolo|IPorigem|IPdestino|Porigem|Pdestino|ACK|
|Firewall 1|1.1|P|I1 - in|TCP|200.17.98.0/24|*|>1023|80,443|0,1|
|Firewall 1|1.2|P|I2 - in|TCP|*|200.17.98.0/24|80,433|>1023|1|
|Firewall 1|2.1|P|I2 - in|TCP|*|200.17.98.2/32|>1023|80,433|0,1|
|Firewall 1|2.2|P|I1 - in|TCP|200.17.98.2/32|*|80,433|>1023|1|
|Firewall 1|3.1|P|I2 - in|UDP|*|200.17.98.4/32|>1023|53|NA|
|Firewall 1|3.2|P|I1 - in|UDP|200.17.98.4/32|*|53|>1023|NA|
|Firewall 1|4.1|P|I1 - in|TCP|200.17.98.3/32|*|>1023|25|0,1|
|Firewall 1|4.2|P|I2 - in|TCP|*|200.17.98.3/32|25|>1023|1|
|Firewall 1|5.1 (D)|N|*|*|*|*|*|*|*|