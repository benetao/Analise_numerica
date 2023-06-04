<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Soluções Numéricas para Equações Diferenciais Ordinárias
 Algumas equações algébricas não são simples de se resolver analiticamente, e, por isso, faz-se necessário discutir mecanismos numéricos para obter soluções aproximadas desse tipo de equação. Apesar desses mecanismos muitas vezes não retornarem soluções exatas, eles podem fornecer aproximações muito boas e úteis para resolução de problemas.
<details><summary><h2><b> Método de Euler</h2></b></summary>

Em python, o método iterativo do ponto fixo pode ser implementado pelo código abaixo, presente no jupyter notebook [Metodo de Euler](https://github.com/benetao/Analise_numerica/blob/main/Solu%C3%A7%C3%B5es%20Aproximadas%20de%20Equa%C3%A7%C3%B5es/Metodo_de_Euler.ipynb) dessa pasta:

```python
def metodo_euler(f, x0, h, crit_parada, lamb):
    """
    Implementa método de Euler para resolver a equação de Malthus.

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
</details>

<details><summary><h2><b> Método de Runge-Kutta</h2></b></summary>
aaa
</details>
<details><summary><h2><b> Método do Trapézio</h2></b></summary>
 socorro
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


