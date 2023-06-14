<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Integração Numérica

Da mesma forma que equações diferenciais podem ter soluções muito difíceis de se obter, integrais também podem ser muito trabalhosas, e algumas sequer possuem solução explícita, como é o caso da integral elíptica de Kapalan, dada por $\int_{0}^{48}\sqrt{1+cos^2(x)}dx$. Nesses casos, faz-se necessária a obtenção de soluções numéricas, tais como as obtidas pelos métodos do Trapézio e de Simpson, citados abaixo.
Ambos esses métodos são quadraduras numéricas, isto é, variações do método de integração em que se utiliza uma soma, cuja constante é obtida através de um polinômio interpolador de Lagrange, para obter resultados aproximados de $\int_{a}^{b}f(x)dx$.

<details><summary><h2><b> Método do Trapézio</h2></b></summary>
    
O método de integração numérica do trapézio é uma técnica para aproximar o valor de uma integral definida usando uma abordagem geométrica simples. Ele divide a área sob uma curva em um (no caso do método do trapézio simples) ou mais trapézios (no caso do método do trapézio composto) e calcula a soma dessas áreas para obter uma estimativa da integral.

No caso do trapézio simples, a integral é aproximada usando apenas um trapézio, utilizando a seguinte expressão:

$$\int_{a}^{b} f(x) dx ≈ (b - a) * \frac{(f(a) + f(b)}{2}$$

Nessa fórmula, $(b - a)$ é a base do trapézio, e $\frac{(f(a) + f(b)}{2}$ é a média das alturas das extremidades do trapézio. Essa média é multiplicada pela base para obter a área do trapézio e, consequentemente, uma estimativa para a integral.

O método do trapézio composto, por sua vez, é uma extensão do trapézio simples e oferece uma maior precisão. Em vez de usar apenas um trapézio, o intervalo $[a, b]$ é dividido em vários subintervalos menores. Em cada subintervalo, um trapézio é formado e a soma das áreas desses trapézios é calculada para aproximar a integral.

Seja $h$ o tamanho de cada subintervalo, então o método do trapézio composto utiliza a seguinte expressão para estimar a integral:

$$\int_{a}^{b} f(x) dx ≈ \frac{h}{2} * [f(a) + f(a + h) + f(a + 2h) + ... + f(b - h) + f(b)]$$

Nessa fórmula, a  soma de todas essas contribuições resulta em uma estimativa mais precisa da integral.

Em resumo, o método de integração numérica do trapézio (simples e composto) é uma maneira de aproximar o valor de uma integral definida usando trapézios para representar a área sob a curva. O trapézio simples utiliza apenas um trapézio, enquanto o trapézio composto divide o intervalo em vários subintervalos e soma as áreas dos trapézios correspondentes.

Em python, os Métodos do Trapézio Simples e Composto podem ser implementados, respectivamente, pelas funções definidas abaixo, presentes no jupyter notebook [Metodo do Trapézio](https://github.com/benetao/Analise_numerica/blob/main/Integra%C3%A7%C3%A3o%20Num%C3%A9rica/Metodo_do_Trapezio.ipynb) dessa pasta:

```python
def metodo_do_trapezio_simples(f, a, b):
    """
    Argumentos: 
    f= função da qual a aproximação da integral será calculada
    a= limite inferior da integral
    b= limite superior da integral
    
    Retorna:
    
    Aproximação da integral pelo método do trapézio
    """
    h = abs(b - a)
    integral = (f(a) + f(b)) / 2 * h

    return integral
    
 def metodo_do_trapezio_composto(f, a, b, n):
    """
    Argumentos: 
    f= função da qual a aproximação da integral será calculada
    a= limite inferior da integral
    b= limite superior da integral
    n= número de trapézios
    
    Retorna:
    
    Aproximação da integral pelo método do trapézio composto
    """
    h = (b - a) / n
    integral = (f(a) + f(b)) / 2

    for i in range(1, n):
        x = a + i * h
        integral += f(x)

    integral *= h
    return integral
 ```
    
  ### Representação Geométrica
    
  <p align="center"><img heigth= 200 width= 700 src= "https://github.com/benetao/Analise_numerica/assets/106626661/1e4a93f1-8a0b-4553-9a3d-b48c69187d1a">
   
  <p align="center">Figura 1: Solução analítica da integral elíptica de Kapalan ($\int_{0}^{48}\sqrt{1+cos^2(x)}dx$) pelo método de Trapézio Simples .
    
  <p align="center"><img heigth= 200 width= 700 src= "https://github.com/benetao/Analise_numerica/assets/106626661/ca64b589-777a-4b6c-874d-29f2ed71e003">
   
  <p align="center">Figura 2: Solução analítica da integral elíptica de Kapalan ($\int_{0}^{48}\sqrt{1+cos^2(x)}dx$) pelo método de Trapézio Composto .
 
 </details>
 <details><summary><h2><b> Método de Simpson</h2></b></summary>
    
O método de Simpson é muito similar ao do Trapézio, mas, por utilizar o polinômio de Lagrange de ordem 2, não aproxima a função de trapézios, mas sim de curvas.
Para tanto, o método de Simpson simples divide a função não só em dois pontos, como fazia-se no método do Trapézio, mas em três pontos- o chamado terço de Simpson (ponto inicial, ponto final e ponto intermediário). Logo, para Simpson simples (apenas uma curva), temos a seguinte expressão:
  $$\int_{a}^{b} f(x) dx ≈ \frac{h}{3}[f(x_0) + 4f(x_1) + f(x_2)]$$
Mas, assim como o método do Trapézio também pode ser composto e dividir a função em mais de um trapézio, tembém existe o método de Simpson composto, que divide a função e a aproxima de mais de uma curva, como mostra a Figura 4. A expressão do Método de Simpson Composto é:
$$\int_{a}^{b} f(x) dx \approx \frac{h}{3} \left[ f(x_0) + 4f(x_1) + 2f(x_2) + 4f(x_3) + 2f(x_4) + \ldots + 2f(x_{n-2}) + 4f(x_{n-1}) + f(x_n) \right]$$

        
Em python, os Métodos de Simpson Simples e Composto podem ser implementados, respectivamente, pelas funções definidas abaixo, presentes no jupyter notebook [Metodo de Simpson](https://github.com/benetao/Analise_numerica/blob/main/Integra%C3%A7%C3%A3o%20Num%C3%A9rica/Metodo_de_Simpson.ipynb) dessa pasta:

```python
def metodo_de_simpson_simples(f, a, b):
    h = (b - a) / 2
    x = np.array([a, (a + b) / 2, b])
    y = f(x)

    integral = h/3 * np.sum(y[0] + 4*y[1] + y[2])

    return integral
    
 def metodo_de_simpson_composto(g, a, b, n):
    if n % 2 != 0:
        n += 1  # Garante um número par de partições

    h = (b - a) / n
    x = np.linspace(a, b, n+1)
    y = g(x)

    integral = h/3 * np.sum(y[0:-1:2] + 4*y[1:-1:2] + y[2::2])

    return integral
 ```
    
  ### Representação Geométrica
    
  <p align="center"><img heigth= 200 width= 700 src= "https://github.com/benetao/Analise_numerica/assets/106626661/fef5d83d-f38f-420c-b9eb-ad000bac6bf3">
   
  <p align="center">Figura 3: Solução analítica de uma função pelo método de Simpson Simples.
  <p align="center"><img heigth= 200 width= 700 src= "https://github.com/benetao/Analise_numerica/assets/106626661/c0fc1b1a-7357-4325-9aae-a185c450d166">
   
  <p align="center">Figura 4: Solução analítica de uma função pelo método de Simpson Composto.
 </details>
 
## Referências
Burden, R.L. and Faires, J.D., 2003. Análise numérica. Thomson. <br />
Conte, S., 1965. Elementary numerical analysis. McGraw Hill. <br />
Ruggiero, M.A.G. and Lopes, V.L.R., 2000. Cálculo numérico: Aspectos teóricos e computacionais. Pearson Universidades.

</p>


