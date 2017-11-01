#3

a. Localize a primeira mensagem ICMP. Porque é que houve necessidade de fragmentar o pacote inicial?  
	
	O pacote inicial tem um _total length_ de 3033 bytes. O _MTU_ disponível é de apenas 1500 bytes e como tal o pacote inicial tem de ser fragmentado para que este possa ser transmitido na rede.

---

b. Imprima o primeiro fragmento do datagrama IP segmentado. Que informação no cabeçalho indica que o datagrama foi fragmentado? Que informação no cabeçalho IP indica que se trata do primeiro fragmento? Qual é o tamanho deste datagrama IP? 

	A informação de que o datagrama foi fragmentado é dada através da _flag more fragments_ que se encontra a 1 em conjugação com o campo _fragment offset_, que neste caso se encontra a 0. Desta forma, podemos concluir que este datagrama é efetivamente o primeiro (_fragment offset_ = 0) de um PDU fragmentado (_flag more fragments_ = 1).

---

c. Imprima o segundo fragmento do datagrama IP original. Que informação do cabeçalho IP indica que não se trata do 1º fragmento? Há mais fragmentos? O que nos permite afirmar isso? 

	Sabe-se que não é o primeiro segmento pois o datagrama em questão tem _fragment offset_ = 1480. Isto é, significa que no datagrama original este segmento começará a partir de 1480 bytes.
	Analisando a _flag more fragments_ percebe-se existe mais fragmentos.
	(...)

---

d. Quantos fragmentos foram criados a partir do datagrama original? Como se detecta o último fragmento correspondente ao datagrama original? 
	
	Analisando o parâmetro _identification_ dos datagramas capturados pelo _Wireshark_ percebe-se que existem três datagramas com o mesmo valor o que revela que pertencem ao mesmo PDU. Desta forma podemos concluir que o datagrama foi fragmentado duas vezes resultando em três fragmentos.
	
	A deteção do último fragmento é feita através da análise da _flag more fragments_. Se esta estiver a 1 então existe mais segmentos. Caso contrário, o segmento em questão é o último.

---

e. Indique, resumindo, os campos que mudam no cabeçalho IP entre os diferentes fragmentos, e explique a forma como essa informação permite reconstruir o datagrama original. 

	Os campos que mudam são os seguintes:

		+ Total length
		+ Flag more fragments
		+ Fragment offset
