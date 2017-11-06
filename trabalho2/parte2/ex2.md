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



IP dest | Next Hop | NetMask
-----------------------------
0.0.0.0 | 10.0.5.1 | 0.0.0.0 -> Netmask a 0 diz que indepentemente do destino faz match
-----------------------------
10.0.5.0 | 0.0.0.0 | 255.255.255.0
             |
		corresponde à própria máquina (10.0.5.20)

