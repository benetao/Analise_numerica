<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Integração Numérica

Da mesma forma que equações diferenciais podem ter soluções muito difíceis de se obter, integrais também podem ser muito trabalhosas, e algumas sequer possuem solução explícita, como é o caso da integral elíptica de Kapalan. Nesses casos, faz-se necessária a obtenção de soluções numéricas, tais como as obtidas pelos métodos do Trapézio e de Simpson, citados abaixo.
Ambos esses métodos são quadraduras numéricas, isto é, variações do método de integração em que se utiliza uma soma, cuja constante é obtida através de um polinômio interpolador de Lagrange, para obter resultados aproximados de $\int_{a}^{b}f(x)dx$.

<details><summary><h2><b> Método do Trapézio</h2></b></summary>
Em python, o Método do Trapézio pode ser implementado pelo código abaixo, presente no jupyter notebook [Metodo do Trapézio](https://github.com/benetao/Analise_numerica/blob/main/Solu%C3%A7%C3%B5es%20Num%C3%A9ricas%20para%20EDOs/Metodo_do_Trapezio.ipynb) dessa pasta:

```python
def metodo_do_trapezio(f, a, b):
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
 ```
  ### Representação Geométrica
 </details>
 <details><summary><h2><b> Método de Simpson</h2></b></summary>
 Terço de Simpson: ponto inicial, ponto final e ponto intermediário
  $\frac{h}{3}[f(x_0) + 4f(x_1) + f(x_2)]$
 </details>
 
## Referências
Burden, R.L. and Faires, J.D., 2003. Análise numérica. Thomson. <br />
Conte, S., 1965. Elementary numerical analysis. McGraw Hill. <br />
Ruggiero, M.A.G. and Lopes, V.L.R., 2000. Cálculo numérico: Aspectos teóricos e computacionais. Pearson Universidades.

</p>


