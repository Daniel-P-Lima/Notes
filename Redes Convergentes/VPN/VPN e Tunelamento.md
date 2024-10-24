![[Redes Convergentes]]
Proteger o tráfego de empresa para empresa, como ligações telefônicas pelo VoiP. Conectando duas entidades formando um canal de comunicação pela internet ou um link que não passa pela internet
- Só existe um link físico mas definindo se os pacotes são criptografados ou não
- Este link onde é configurado o VPN pode estar criptografado e é autenticado a origem dos pacotes 
- O VPN Camada 3, faz parte da camada de S.O na pilha, criptografando rede, transporte e aplicação
## Primeira Alternativa
Provedor cria VPN entre matriz e filial, desviando da internet.
## Segunda Alternativa
A própria empresa implementa um VPN
## Criptografia e Tunelamento
Um pacote dentro do outro
Quando uma máquina pinga outra por uma rede de VPN, o pacote IP de ping é inserido dentro de outro pacote e é criptografado. Seguindo criptografado dentro do outro pacote até chegar no seu destino. Quando entregue no gateway de entrada da rede é descriptografado e retirado do pacote 