<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Soluções Aproximadas de Equações
 Algumas equações algébricas não são simples de se resolver analiticamente, e, por isso, faz-se necessário discutir mecanismos numéricos para obter soluções aproximadas desse tipo de equação. Apesar desses mecanismos muitas vezes não retornarem soluções exatas, eles podem fornecer aproximações muito boas e úteis para resolução de problemas.

<details><summary><h2><b> Método de Bissecção</h2></b></summary>
Um dos métodos para se alcançar raízes aproximadas de equações é o da bisecção. Nele, definimos um intervalo inicial $[a, b]$ da função e vamos diminuindo em outros menores até encontrar o valor $p$, próximo da resposta. Para tanto, calculamos o ponto médio do intervalo, dado por $p = \frac{a+b}{2}$. 

Se $f(p)=0$, encontramos o nosso resultado! 

No entanto, se $f(p)$ tiver o mesmo valor de $f(a)$, consideramos $a= p$ e $b= b$. 

Se $f(p)$ tiver o mesmo valor de $f(b)$, ou, ainda, se $f(a)$ e $f(b)$ tiverem o mesmo sinal consideramos $a= a$ e $b= p$.

Repetimos esse processo até que a diferença entre p e a raíz real da função seja menor que a precisão que queremos (também chamada, no código, de critério de parada).

Em python, o método da bissecção pode ser implementado pelo código abaixo, presente no jupyter notebook [Método de Bissecção](https://github.com/benetao/Analise_numerica/blob/main/Solu%C3%A7%C3%B5es%20Aproximadas%20de%20Equa%C3%A7%C3%B5es/Metodo_de_Bisseccao.ipynb) dessa pasta:
```python
def bissecao(inicio, fim, parada, N): #inicio= começo do intervalo dado; fim= fim do intervalo dado; parada= critério de parada; N= número máx de repetições
    f_inicial = f(inicio) # primeriro f(x) a ser analizado é o do início do intervalo
    i=1
    while (i <= N):
        p = inicio + (fim-inicio)/2 # calculando ponto médio
        f_final = f(p) # calculando f(x) do ponto médio
        if ((f_final == 0) or ((fim-inicio)/2 < parada)): # para quando achar a raíz OU quando a diferença entre o nº encontrado e a raíz for menor que parada
            return p # retorna o valor aproximado da raíz
        # bissecta o intervalo
        i= i+1
        if (f_inicial * f_final > 0): # analisando se fa e fp tem sinais distintos. Se sim, significa que a raíz está entre esses valores
            inicio = p # portanto, devemos calcular o ponto médio entre esses valores
            f_inicial = f_final
        else: # se fa e fp tem mesmo sina, dignifica que a raíz NÃO está entre esses valores
            fim=p
```
### Representação Geométrica
<p align="center"><img heigth= 120 width= 550 src= "https://user-images.githubusercontent.com/106626661/228638909-4301ca3e-47f3-457b-8378-e78a37556308.png">

</details>


<details><summary><h2><b> Método de Newton</h2></b></summary>

O método de Newton, ou método das tangentes, utiliza uma aproximação inicial da raiz e aprimora essa aproximação através de sucessivas iterações. O método de Newton é baseado no conceito de que a raiz de uma equação é o ponto em que a curva da função cruza o eixo das abscissas.

A fórmula do método de Newton é dada por:
$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$
Onde $x_n$ é a aproximação atual da raiz, $x_{n+1}$ é a próxima aproximação, $f(x_n)$ é o valor da função na aproximação atual e $f'(x_n)$ é a derivada da função na aproximação atual.

O método de Newton começa com uma aproximação inicial $x_0$. A cada iteração, a equação acima é utilizada para encontrar uma nova aproximação $x_{n+1}$. Esse processo é repetido até que a diferença entre a aproximação atual e a anterior seja menor que um certo valor de tolerância.

O método de Newton pode convergir para a raiz da equação muito mais rapidamente do que outros métodos numéricos, como o método da bissecção. No entanto, ele também pode ser mais sensível a aproximações iniciais ruins e a funções com pontos de inflexão próximos à raiz.



Em python, o método de Newton pode ser implementado pelo código abaixo, presente no jupyter notebook [Método de Newton](https://github.com/benetao/Analise_numerica/blob/main/Solu%C3%A7%C3%B5es%20Aproximadas%20de%20Equa%C3%A7%C3%B5es/Metodo_de_Newton.ipynb) dessa pasta:

```python
def newton(f, df, p0, eps=1e-6):
    # Definimos uma variável para armazenar o valor atual de x
      """
    Encontra uma raiz de f(x) a partir de um chute inicial p0 com precisão eps pelo método de Newton
    
    Retorna a raiz e o número de iterações do código
    """
    p = p0
    i=0
    fp = f(p)
    # Fazemos um loop para iterar o método de Newton
    while abs(fp) > eps: # critério de parada (precisão)
        # Calculamos o valor de f(x) e df(x)
        i = i+1 # contador de iteração
        fp = f(p)
        dfp = df(p)

        # Calculamos a próxima aproximação de x usando o método de Newton
        
        p = p - fp / dfp
        
        """ Série de Taylor: pn= pn-1 - (f(pn-1)/ f'(pn-1)"""

        # Verificamos se o valor atual de x é uma aproximação suficientemente boa para uma raiz
    return p
```
### Representação Geométrica
<p align="center"><img heigth= 120 width= 550 src= "https://user-images.githubusercontent.com/106626661/228925639-212a05c1-e230-4474-b5d8-e525db3e8df5.png">

 </details>
 
<details><summary><h2><b> Método da Secante</h2></b></summary>
 
 O método da secante é uma variação do método de Newton para encontrar raízes de uma função. Contudo, o método da secante não requer o cálculo da derivada da função, o que o torna mais simples em algumas situações.

Para obter o método da secante a partir do método de Newton, basta substituir a a derivada $f'(x_n)$ pela aproximação de diferenças finita, que é dada por: 
 
 $f'(x_n) = \frac{f(x_n) - f(x_{n-1})}{x_n - x_{n-1}}$
 
 Logo, substindo isso na fórmula do método da bissecção, obtemos:
 
 $f'(x_{k+1}) = \frac {f(x_k)x_{k-1}- f(x_{k-1})x_k}{f(x_k) - f(x_{k-1})}$

Ou seja, ao invés de usar a derivada $f'(x_n)$, ela utiliza uma aproximação da derivada calculada a partir de dois pontos próximos da curva da função.
Apesar de não requerer a avaliação da derivada da função, o que é uma vantagem, o método da secante geralmente é mais lento que o de Newton, podendo levar mais iterações para chegar a um resultado.
 
Em python, o método de Newton pode ser implementado pelo código abaixo, presente no jupyter notebook [Método de Newton](https://github.com/benetao/Analise_numerica/blob/main/Solu%C3%A7%C3%B5es%20Aproximadas%20de%20Equa%C3%A7%C3%B5es/Metodo_de_Newton.ipynb) dessa pasta:

```python
def secante(f, x0, x1, eps):
    """
    Encontra uma raiz da função f usando o método da secante,
    com aproximações iniciais x0 e x1 e critério de parada eps.
    
    Retorna a raiz encontrada e o número de iterações.
    """
    fx0 = f(x0)
    fx1 = f(x1) # são necessários dois pontos iniciais ( e não apenas 1, como eno de Newton, para se obter a média)
    x2 = x1 - fx1 * (x1 - x0) / (fx1 - fx0) # Definição do método da secante, obtida no item enterior pela aproximação da derivada da função
    i = 1
    while abs(f(x2)) > eps: # critério de parada (precisão)
        x0, x1 = x1, x2
        fx0, fx1 = fx1, f(x2)
        x2 = x1 - fx1 * (x1 - x0) / (fx1  - fx0)
        i += 1 # contador de iteração
    return x2, i
```
### Representação Geométrica
 <p align="center"><img heigth= 120 width= 550 src= "https://user-images.githubusercontent.com/106626661/228674014-8905f095-afbc-4ad1-9fde-96ed34dac3c9.png">


 
Podemos observar, por meio da representação geométrica, que, ao aplicar essa fórmula, a estimativa da raiz $x_{n+1}$ é calculada como a intersecção entre a reta que passa pelos pontos $(x_n, f(x_n))$ e $(x_{n-1}, f(x_{n-1}))$ e o eixo $x$:
<p>
</details>
<details><summary><h2><b> Método da Secante</h2></b></summary>
Socoooorrroooooo
</details>
## Referências
Burden, R.L. and Faires, J.D., 2003. Análise numérica. Thomson. <br />
Conte, S., 1965. Elementary numerical analysis. McGraw Hill. <br />
Ruggiero, M.A.G. and Lopes, V.L.R., 2000. Cálculo numérico: Aspectos teóricos e computacionais. Pearson Universidades.

</p>

