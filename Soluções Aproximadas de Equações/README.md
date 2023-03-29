<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Soluções Aproximadas de Equações
 Algumas equações algébricas não são simples de se resolver analiticamente, e, por isso, faz-se necessário discutir mecanismos numéricos para obter soluções aproximadas desse tipo de equação. Apesar desses mecanismos muitas vezes não retornarem soluções exatas, eles podem fornecer aproximações muito boas e úteis para resolução de problemas.
## Método de Bissecção

Um dos métodos para se alcançar raízes aproximadas de equações é o da bisecção. Nele, definimos um intervalo inicial $[a, b]$ da função e vamos diminuindo em outros menores até encontrar o valor $p$, próximo da resposta. Para tanto, calculamos o ponto médio do intervalo, dado por $\frac{a+b}{2}$. Se $f(p)=0$, encontramos o nosso resultado! 

No entanto, se $f(p)$ tiver o mesmo valor de $f(a)$, consideramos a= p e b= b. Se $f(p)$ tiver o mesmo valor de $f(b)$, ou, ainda, se $f(a)$ e $f(b)$ tiverem o mesmo sinal consideramos a= a e b= p.

Repetimos esse processo até que a diferença entre p e a raíz real da função seja menor que a precisão que queremos (também chamada, no código, de critério de parada).

Em python, o método da bissecção pode ser implementado pelo código abaixo, presente no jupyter notebook []() dessa pasta:
```python
current_feed = feedparser.parse(links[0])
```

A partir disso, é possível buscar algumas estruturas do site que são do interesse para o desenvolvimento do site, sendo, no caso, o título, o link e a data de publicação da matéria. Para tanto, podemos utilizar o seguinte formato:

```python
current_feed.feed.title,current_feed.feed.link,current_feed.feed.description
```
## Método de Newton

Em seguida, levando em consideração que o site é destinado a estudantes brasileiros, é interessante a tradução do texto em inglês para o português, e, para tanto, foi usada a biblioteca Google Translator. Passamos como parâmetro da função `translate` da biblioteca a string a ser traduzida, seguida do seu destino, isto é, para que língua o texto deve ser traduzido.

```python
trans.translate('Hello, world!',dest='pt').origin
trans.translate('Hello, world!',dest='pt').text
```

Note que no código acima podemos buscar o texto original com a extensão `.origin` e o texto em si traduzido com `.text`.

## Método da Secante

Com base no exposto, finalmente podemos realizar a coleta dos dados e realizar uma inserção em um arquivo `.csv`, com as colunas "name", "date" e "link". No código a seguir, o loop é destinado por passar por todos os elementos encontrados e inserir no arquivo de destino.

```python
for link in links:
    current_feed = feedparser.parse(link)
    for n in range(len(current_feed.entries)-1):
        text = trans.translate((current_feed.entries[n].title),dest='pt').text 
        print(text)
        print(current_feed.entries[n].published[5:16])
        print(current_feed.entries[n].link)
        print()
```

Uma vez que o arquivo estava pronto, foi possível realizar a atualização de um arquivo já existente neste repositório (`\dados\dados.csv`) para que os dados desejados pudessem ser usados.


