#2
a. Qual é o endereço IP da interface ativa do seu computador? 
	
	O endereço IP é 192.168.100.216 (campo source)

---

b. Qual é o valor do campo protocolo? O que identifica?

	O campo protocolo tem o valor "ICMP (1)". ICMP significa _Internet Control Message Protocol_ e é utilizado para comunicar ao nível da rede, tanto eventuais erros que possam acontecer, como por exemplo, _unreachable host, network, port, protocol_, out então _echo request/reply_. Como as mensagens ICMP encontram-se ao nível de rede, estas são também elas encapsuladas em datagramas IP que, consequentemente, usam o protocolo IP.
	Assim sendo, significa que a primeira mensagem ICMP transporta um _erro_ ou _echo_.

---

c. Quantos bytes tem o cabeçalho IP(v4)? Quantos bytes tem o campo de dados (payload) do datagrama? Como se calcula o tamanho do payload?  
	
	+ O **cabeçalho** IPv4 tem **20 bytes**.
	+ O **campo de dados** (payload) do datagrama tem **40 bytes**
	+ O cálculo do payload é feito retirando o tamanho do cabeçalho ao tamanho total do datagrama. Assim, basta fazer _60 - 20 = 40 bytes_.

---

d. O datagrama IP foi fragmentado? Justifique.

	QUANDO É QUE ACONTECE FRAGMENTAÇÃO?????
	Quando IP total length (por defeito o traceroute usa 60 bytes) > MTU disponível (1500 bytes)
	
	A verificação se um datagrama foi ou não fragmentado é feita com base em dois valores, o _fragment offset_ e a _flag more fragments_. Neste _PDU_ em específico _fragment offset_ = 0 e a _flag more fragments_ = 0. Desta forma, tendo em conta o _fragment offset_, sabe-se que se o datagrama foi fragmentado então ele é necessariamente o primeiro. Além disso, se analisarmos a _flag more fragments_ concluímos que para além do datagrama atual não existe mais nenhum associado a este. Assim sendo, conjugando a informação dos dois parâmetros percebe-se que se o datagrama é o primeiro e não existe mais nenhum associado, então este é único e não foi fragmentado.

---

e. Ordene os pacotes capturados de acordo com o endereço IP fonte (e.g., selecionando o cabeçalho da coluna Source), e analise a sequência de tráfego ICMP gerado a partir do endereço IP atribuído à sua máquina. Para a sequência de mensagens ICMP enviadas pelo seu computador, indique que campos do cabeçalho IP variam de pacote para pacote.  

	Os campos que vêm os seus valores alterados correspondem à _identification_, _header checksum_ e _time to live (TTL)_. 

---

f. Observa algum padrão nos valores do campo de Identificação do datagrama IP e TTL? 

	+ O campo da indentificação corresponde a um valor que é incrementado e que identifica unicamente o datagrama em questão. Por exemplo, se o primeiro datagrama tiver _Identification_ 0xb224 (45604), então o datagrama seguinte terá o valor 0xb225 (45605). 
	+ O TTL corresponde a uma variável que vai sendo decrementada sempre que é intersetada por um _router_. Visto que na primeira mensagem o TTL é 1, o datagrama é descartado imediatamente no primeiro _router_. Deste modo, é enviado, de seguida, um novo datagrama com TTL a 2 com a esperança de que este chegue desta vez ao destino. Caso não chegue, então no próximo PDU o TTL será aumentado, e assim sucessivamente, até chegar ao destino.

---

g. Ordene o tráfego capturado por endereço destino e encontre a série de respostas ICMP TTL exceeded enviadas ao seu computador. Qual é o valor do campo TTL? Esse valor permanece constante para todas as mensagens de resposta ICMP TTL exceeded enviados ao seu host? Porquê? 

	A source 192.168.100.254 referencia o primeiro router de acesso (visto ter o três primeiros campos iguais ao da máquina em que os testes estão a ser feitos e o último utiliza um número convencionado para ser utilizado para identificar a interface IP do router dentro da rede 192.168.100, na qual a máquina de testes se encontra).

	Desta forma, quando analisamos os datagramas da _source_ 192.168.100.254 percebemos que estes têm todos o TTL = 64. O TTL toma um valor exageradamente grande, devido ao desconhecimento que este tem da distância a que o _host_ de destino se encontra. Por defeito, este _source_ quando não tem informação da distância a que o _host_ de destino se encontra manda datagramas com TTL = 64 e por isso todas os seus DPU's tem TTL igual.

	Além disso, é possível concluir que as três mensagens recebidas deste _source_ com _ICMP TTL exceeded_ são a resposta ao envio feito pela máquina de testes de três datagramas de _echo (ping) request_ com TTL apenas de 1. Estes datagramas chegaram ao _router_ e ficaram com o TTL a 0 e o erro veio enviado de volta no datagrama _ICMP TTL exceeded_.

	Após estes datagramas é possível identificar um segundo conjunto de datagramas desta vez do _source_ 193.136.19.254. Pelo mesmo raciocínio podemos assumir que o IP desta interface identifica um _router_. Este novo _router_ envia datagramas com TTL = 254 (constante). Este valor é considerável pela mesma razão explicitada anteriormente. Estes datagramas são a resposta a 3 datagramas enviados pela máquina de testes com TTL = 2.
