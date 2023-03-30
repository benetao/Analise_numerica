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

* `Erro Relativo`: $e(n)=$ $\frac{|n - n^*|}{n}$

Em python, podemos calcular erro absoluto definindo a seguinte função, presentes no jupyter notebook da pasta:
```python
def erro_absoluto(valor_real, valor_aproximado):
    """
    Calcula o erro absoluto de uma aproximação em relação ao valor real.
    """
    return abs(valor_real - valor_aproximado)
```

Já para calcular o erro relativo de uma aproximação, pode-se utilizar o código:

```python
def erro_relativo(valor_real, valor_aproximado):
    """
    Calcula o erro relativo de uma aproximação em relação ao valor real.
    """
    return abs((valor_real - valor_aproximado) / valor_real)

```
## Tipos de Erro

*`Algoritmo estável`: tipo de método numérico mais confiável, pois não propaga erro dos dados iniciais

*`Algoritmo instável`: menos confiável, pois propaga o erro dos dados iniciais

Algoritimos instáveis podem, muitas vezes, resultar num `Erro exponencial`, isto é, um erro para que,a pós $n$ operações sucessivas, pode ser calculado por $E_n = C^nE_0$, sendo C > 1. Normalmente, os resultados mais aceitáveis possuem `Erro Linerar`, geralmente resultantes de algoritmos estáveis. 

## Referências
<p>
Burden, R.L. and Faires, J.D., 2003. Análise numérica. Thomson. <br />
Conte, S., 1965. Elementary numerical analysis. McGraw Hill. <br />
Ruggiero, M.A.G. and Lopes, V.L.R., 2000. Cálculo numérico: Aspectos teóricos e computacionais. Pearson Universidades.

</p>
