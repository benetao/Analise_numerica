<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Sistemas de Números e Estudo de Erro

No dia-a-dia de um cientista, é muito comum a utilização de simulações numéricas, a fim de obter aproximações de resultados teóricos ou experimentais. Ao criarmos modelos matemáticos para fenômenos físicos, químicos ou biológicos, presumimos que a solução para o problema terá que ser encontrada por meio do uso de computadores. Uma vez que o modelo tenha sido criado, é importante realizar uma análise numérica da solução, que inclui a verificação de erros que possam afetar o comportamento da solução, bem como sua precisão e convergência. Para isso, é necessário avaliar o tamanho adequado dos passos para cada método, o número necessário de iterações e assim por diante.

## Aritmética computacional

Em modelos matemáticos computacionais, é muito comum que nos deparemos com números que não são reais, como, por exemplo $\sqrt{2}$ , número irracional, que possui infinitas casas decimais, significando que para representar esse valor numérico no computador é preciso aproximá-lo, e portanto, comete-se um erro nesse cálculo.

Existem dois principais métodos de aproximação:
* `Arredondamento`: se o último dígito é maior ou igual a 5 então soma-se 1 ao dígito anterior; se o último dígito é menor que 5, então desconsidera-se o último dígito;
* `Truncamento`: simplesmente desconsidera o último dígito

Para calcular os erros gerado quando aproximamos um número $n$ para $n^*$, temos:

* `Erro Absoluto`: $e(n)=$ $|n - n^*|$

* `Erro Eelativo`: $e(n)=$ $\frac{|n - n^*|}{n}$

Em python, podemos calcular esses erros definindo as seguintes funções:
```python
current_feed = feedparser.parse(links[0])
```

A partir disso, é possível buscar algumas estruturas do site que são do interesse para o desenvolvimento do site, sendo, no caso, o título, o link e a data de publicação da matéria. Para tanto, podemos utilizar o seguinte formato:

```python
current_feed.feed.title,current_feed.feed.link,current_feed.feed.description
```
## Tipos de Erro

*`Algoritmo estável`: tipo de método numérico mais confiável, pois não propaga erro dos dados iniciais

*`Algoritmo estável`: menos confiável, pois propaga o erro dos dados iniciais

Em seguida, levando em consideração que o site é destinado a estudantes brasileiros, é interessante a tradução do texto em inglês para o português, e, para tanto, foi usada a biblioteca Google Translator. Passamos como parâmetro da função `translate` da biblioteca a string a ser traduzida, seguida do seu destino, isto é, para que língua o texto deve ser traduzido.

```python
trans.translate('Hello, world!',dest='pt').origin
trans.translate('Hello, world!',dest='pt').text
```

Note que no código acima podemos buscar o texto original com a extensão `.origin` e o texto em si traduzido com `.text`.

## Implementação do código

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

## Integração dos dados e site

Com o intuito de integrar os dados no site, foi utilizado o Liquid templating system, que é uma variável construída no próprio Jekyll. Como parte de perfumaria, os dados foram colocados dentro de um retângulo estilizado.

```md
{% for dado in site.data.dados %}

  <div style="margin-bottom:8px;border: 0.5px solid grey;border-radius: 5px;">
    <div style="padding:10px;">
      <strong>{{ dado.name }}</strong><br>
      {{ dado.date }} • <a href="{{ dado.link }}" target="_blank">Link</a>
    </div>
  </div>
{% endfor %}
```
