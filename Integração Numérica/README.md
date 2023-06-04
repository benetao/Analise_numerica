<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Integração Numérica
Ano passado, na disciplina de Equações Diferenciais do segundo semestre da Ilum, fomos apresentados aos PVIs (Problemas de Valores Iniciais), que se tratam basicamente de uma equação diferencial associada a uma condição inicial. Como exemplo, podemos descrever o crescimento de uma população que segue à lei de de uma população que  Verhulst (equação diferencial é  $x'(t)= \lambda x(t)$ ) e que começa com 2 indivíduos (condição inicial é $x(0)= 2$). Encontrar a solução exata para esse tipo de equação, muitas vezes, é uma tarefa muito difícil e, por isso, faz-se necessário o uso de aproximações numéricas. Para obter essas aproximações, podemos utilizar um dos dois métodos descritos abaixo!

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


