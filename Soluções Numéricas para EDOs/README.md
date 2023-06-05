<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Soluções Numéricas para Equações Diferenciais Ordinárias
Ano passado, na disciplina de Equações Diferenciais do segundo semestre da Ilum, fomos apresentados aos PVIs (Problemas de Valor Inicial), que se tratam basicamente de uma equação diferencial associada a uma condição inicial. Como exemplo, podemos descrever o crescimento de uma população que segue à lei de de uma população que  Malthus (equação diferencial é  $x'(t)= \lambda x(t)$ ) e que começa com 2 indivíduos (condição inicial é $x(0)= 2$). Encontrar a solução exata para esse tipo de equação, muitas vezes, é uma tarefa muito difícil e, por isso, faz-se necessário o uso de aproximações numéricas. Para obter essas aproximações, podemos utilizar um dos dois métodos descritos abaixo!


<details><summary><h2><b> Método de Euler</h2></b></summary>
 
 O método de Euler é considerado um dos mais simples e fáceis de ser implementado computacionalmente, com um custo computacional relativamente baixo (quando comparado aos outros métodos). Sua expressão pode ser obtida através da expansão de Taylor da definição de derivada no ponto $t_p$:
 $$x'(t_p)= lim(t \rightarrow t_p) \frac{x(t) - x(t_p)}{t - t_p}$$
A partir dessa definição de derivada e considerando que, no método de Euler, o passo ($h= t-t_p$) é sempre constante, podemos chegar à expressão deral do método:
 $$x_{n+1}= x_n + hf(t_n,x_n)$$.
 E seu erro pode ser calculado por $O(h^2)$. Ou seja, quando menor o passo $h$, melhor a aproximação! 
 Entretanto, isso significa que, para obtermos um bom resultado, precisamos de um número muito grande de passos e, por consequência, o custo computacional é muito alto. Isso é ua desvantagem do método de Euler, que, apesar de ser mais simples que os outros métodos, também pode ser muito mais custoso computacionalmente.
 

Em python, o Método de Euler pode ser implementado pelo código abaixo, presente no jupyter notebook [Metodo de Euler](https://github.com/benetao/Analise_numerica/blob/main/Solu%C3%A7%C3%B5es%20Num%C3%A9ricas%20para%20EDOs/Metodo_de_Euler.ipynb) dessa pasta:

```python
def metodo_euler(f, x0, h, crit_parada, lamb):
    """
    Implementa método de Euler para resolver a equação f.

    Args:
        f : função que define a equação diferencial.
        x0 : valor inicial da população.
        h : tamanho do passo de integração.
        crit_parada : número de iterações do código.
        lambda : taxa de crescimento populacional.

    Returns:
        listas do eixo x e do eixo y para plotar o gráfico
    """
    y_euler = [y0]  # Lista para armazenar as soluções do eixo y
    x_euler = [0]  # Lista para armazenar valores do eixo x
    y = y0  # Valor inicial

    for i in range(crit_parada):
        y += h * f(y, x_euler[-1], lamb)  # Atualiza y usando o método de Euler
        t = (i + 1) * h  # Atualiza t
        x_euler.append(t)
        y_euler.append(y)

    return x_euler, y_euler
 ```
 ### Representação Geométrica
 
 <p align="center"><img heigth= 240 width= 1000 src= "https://github.com/benetao/Analise_numerica/assets/106626661/75ba96bc-a24e-4b14-8dda-6535acd9e25e">
  Figura 1: Aproximação da solução analítica pelo método de Euler do PVI citado no texto acima ($x′(t) = \lambda x(t)$, considerando condição inicial $x(0) = 2$).
</details>

<details><summary><h2><b> Método de Runge-Kutta</h2></b></summary>
 
 A expressão do método de Runge-Kutta é deduzida de forma muito semelhante à do método de Eules. Para o método de Runge-Kutta, no entanto, a expansão de taylor da definição de derivada é realizada até a quarta ordem, e não só até a segunda. Dessa forma, obtemos a seguinte expressão:
 $$x_n+1 = x_n + \frac{h}{6}(k_1+2k_2+2k_3+k_4)$$
 sendo que $k_1,k_2,k_3$ e $k_4$ são iguais a:
 $$k_1= f(t_n,x_n)$$
 $$k_2=  f(t_n,\frac{h}{2}x_n,\frac{h}{2}k_1)$$
 $$k_3= f(t_n,\frac{h}{2}x_n), \frac{h}{2}k_2)$$
 $$k_4=  f(t_n+h,x_n),hk_3)$$
 Como consequência, temos agora um método bem mais preciso que o Método de Euler. Afinal, com um mesmo valor de passo $h$, o método de Runge-Kutte retorna um erro muito menor, visto que o erro desse método é dado por $O(h^4)$. Isso pode ser percebido na Figura 4, na seção de Representação Geométrica.
 
Em python, o Método de Runge-Kutta pode ser implementado pelo código abaixo, presente no jupyter notebook [Metodo de Runge Kutta](https://github.com/benetao/Analise_numerica/blob/main/Solu%C3%A7%C3%B5es%20Num%C3%A9ricas%20para%20EDOs/Metodo_de_Runge_Kutta.ipynb) dessa pasta:

```python
def runge_kutta_4(f, y0, t0, tf, dt):
    """
    Resolve uma equação diferencial ordinária pelo método de Runge-Kutta de ordem 4.
​
    Parâmetros:
    f: função que descreve a equação diferencial (deve ter a assinatura f(t, y)).
    y0: valor inicial da solução.
    t0: tempo inicial.
    tf: tempo final.
    dt: tamanho do passo de tempo.
​
    Retorno:
    Um array com a solução da equação diferencial nos tempos especificados.
    """
​
    # Inicializa o vetor de tempo e de solução
    t = np.arange(t0, tf + dt, dt)
    y = np.zeros(len(t))
    y[0] = y0
​
    # Implementa o método de Runge-Kutta de ordem 4
    for i in range(len(t) - 1):
        k1 = dt * f(t[i], y[i])
        k2 = dt * f(t[i] + dt/2, y[i] + k1/2)
        k3 = dt * f(t[i] + dt/2, y[i] + k2/2)
        k4 = dt * f(t[i] + dt, y[i] + k3)
        y[i+1] = y[i] + 1/6 * (k1 + 2*k2 + 2*k3 + k4)
​
    return y
 ```
  ### Representação Geométrica
  <p align="center"><img heigth= 240 width= 800 src= "https://github.com/benetao/Analise_numerica/assets/106626661/b45a0730-5146-4a4e-a871-29c08873777c">
   
  Figura 2: Comparação das soluções do método de Runge-Kutta e de Euler para o PVI $x′(t) = \lambda x(t)$, condição inicial $x(0) = 2$.
 
 
</details>

 
## Referências
Burden, R.L. and Faires, J.D., 2003. Análise numérica. Thomson. <br />
Conte, S., 1965. Elementary numerical analysis. McGraw Hill. <br />
Ruggiero, M.A.G. and Lopes, V.L.R., 2000. Cálculo numérico: Aspectos teóricos e computacionais. Pearson Universidades.

</p>


