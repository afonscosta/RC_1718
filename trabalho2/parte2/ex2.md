#2. Endereçamento e Encaminhamento IP

1b. Tratam-se de endereços privados pois o primeiro octeto é 00001010, que representa em decimal 10. Sendo este o primeiro octeto podemos afirmar que é um endereço IP privado visto que pertence ao conjunto de prefixos que identificam um endereçamento privado, nomeadamente, 
	+ Class A:  Start address – 10.0.0.0  End Address – 10.255.255.255
Outros possíveis conjuntos de endereços privados são:
	+ Class B:  Start address – 172.16.0.0  End Address – 172.31.255.255
	+ Class C:  Start address – 192.168.0.0  End Address – 192.168.255.255

---

1c. Na topologia em questão se vier pacote com destino ao PC7, este vem com endereço de destino de 10.0.9.20/24. Para tal, o pacote vem do _router_ R e chega ao _router_ Rd. O _router_ Rd aplica a NetMask 255.255.255.0 ao endereço de destino e obtém 10.0.9.0. Consegue fazer match no endereço 10.0.9.1 e envia o pacote para o SW4. Ao chegar ao SW4, este avalia o endereço de destino e duas situações podem acontecer. Se este tiver nos seus registos o endereço 10.0.9.20, então envia diretamente ao host especificado. Caso não tenha ainda essa informação envia para todos os hosts a ele ligados.

Efetivamente, os _switcts_ não operam ao nível de rede e como tal a camada de rede, nomeadamente o IP, é completamente transparente para estes dispositivos.

Através do exemplo a cima podemos concluir que não é necessário que este tenha IP pois os pacotes são enviados para o _switch_ com base no IP da rede que existe entre o _router_ e o _switch_. Visto que o _router_ interliga diferentes redes.

---

1.d. Usando o comando ping certifique-se que existe conectividade IP entre os laptops dos vários departamentos e os servidores do departamento D (basta certificar-se da conectividade de um laptop por departamento).

	prints

---
1.e. Verifique se existe conectividade IP do router de acesso para os servidores S1 e S2.

	prints

---
---
---
---
---

2.a. Execute o comando netstat –rn por forma a poder consultar a tabela de encaminhamento unicast (IPv4). Inclua no seu relatório as tabelas de encaminhamento obtidas; interprete as várias entradas de cada tabela. Se necessário, consulte o manual respetivo ( man netstat ).

	+PC3

	A primeira linha na tabela de endereçamento do PC3 representa a rota por defeito, isto é, quando entre no PC3 um datagrama com um IP que não faz _match_ com nenhum IP da coluna _Destination_ então este é reencaminhado para o _router_ de acesso, ou seja, 10.0.7.1 ficando este responsável pelo seu encaminhamento. Denotando que a primeira linha, por ser um endereço estático, tem a menor prioridade. Esta linha faz _match_ com qualquer endereço pois tem uma _Genmask_ igual a 0.0.0.0. Efetivamente, quando chega à máquina PC3, por exemplo,  um datagrama com o IP 10.0.8.20, este é comparado com todas as linhas da tabela. Posteriormente é aplicada a máscara.
10. 0. 8.20
 0. 0. 0. 0
------------
 0. 0. 0. 0 == 0. 0. 0. 0 (Destination)
	O resultado é depois comparado com o campo _Destination_ e faz match. De seguida é enviado para o router de acesso explicitado pelo campo _Gateway_

	A segunda linha é responsável por encaminhar, através da própria máquina, o trânsito local, ou seja, o prórprio PC3 encaminha os datagramas para _hosts_ vizinhos. 
	Deste modo, todos os datagramas que tiverem como prefixo de rede 10.0.7 vão fazer match na segunda linha, isto porque, chegando por exemplo o datagrama com o IP 10.0.7.21, é aplicada a máscara 255.255.255.0 e resulta a _destination_ 10.0.7.0. Posteriormente é enviado para o endereço dito no _Gateway_, 0.0.0.0, ou seja, fica responsável por encaminhar este datagrama a própria máquina. 
	Este processo de encaminhamento resulta pois os _hosts_ tem conhecimento da topologia da rede local na qual estão inseridos e como tal, pode ser delegado o encaminhamento local aos _hosts_.

	+Rb
	
	A tabela de encaminhamento do _router_ Rb não incluí rotas por defeito pois todas as rotas existentes na rede encontram-se identificadas na tabela à partida.
	Através da análise da topologia na rede criada com o CORE percebemos que o _router_ Rb deverá ser responsável por encaminhar para a rede 10.0.0.0, 10.0.1.0, e 10.0.7.0. A tabela de encaminhamento confirma as nossas suspeitas, pois todas as linhas que têm os endereços IP atrás indicados têm como _Gateway_ 0.0.0.0, que significa que o próprio _router_ fica responsável por encaminhar esses datagramas.
	Todas as outras redes existentes encontram-se na tabela com o endereço de encaminhamento apropriado. Nomeadamente, caso os datagramas tenham como destino a rede 10.0.x.0 em que x={2,3,6,8,9,10} estes são reencaminhados para uma das duas redes a que este _router_ tem acesso, isto é, 10.0.0.1 ou 10.0.1.2. Estas entradas em espicífico na tabela têm a _flag_ G no campo _Flags_, visto não ser um encaminhamento direto.

---

2.b. Diga, justificando, se está a ser usado encaminhamento estático ou dinâmico (sugestão: analise que processos estão a correr em cada sistema).

---

#EXTRAS

IP dest | Next Hop | NetMask
-----------------------------
0.0.0.0 | 10.0.5.1 | 0.0.0.0 -> Netmask a 0 diz que indepentemente do destino faz match
-----------------------------
10.0.5.0 | 0.0.0.0 | 255.255.255.0
             |
		corresponde à própria máquina (10.0.5.20)

