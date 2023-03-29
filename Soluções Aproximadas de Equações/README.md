<img align="right" alt="ilum" height="40" width="150" src="https://github.com/pedrozanineli/pcd.github.io/blob/main/logo1.png">

# Soluções Aproximadas de Equações
 Algumas equações algébricas não são simples de se resolver analiticamente, e, por isso, faz-se necessário discutir mecanismos numéricos para obter soluções aproximadas desse tipo de equação. Apesar desses mecanismos muitas vezes não retornarem soluções exatas, eles podem fornecer aproximações muito boas e úteis para resolução de problemas.
## Método de Bissecção

Um dos métodos para se alcançar raízes aproximadas de equações é o da bisecção. Nele, definimos um intervalo inicial $[a, b]$ da função e vamos diminuindo em outros menores até encontrar o valor $p$, próximo da resposta. Para tanto, calculamos o ponto médio do intervalo, dado por $\frac{a+b}{2}$. Se $f(p)=0$, encontramos o nosso resultado! 

No entanto, se $f(p)$ tiver o mesmo valor de $f(a)$, consideramos a= p e b= b. Se $f(p)$ tiver o mesmo valor de $f(b)$, ou, ainda, se $f(a)$ e $f(b)$ tiverem o mesmo sinal consideramos a= a e b= p.

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

## Método de Newton


Em seguida, levando em consideração que o site é destinado a estudantes brasileiros, é interessante a tradução do texto em inglês para o português, e, para tanto, foi usada a biblioteca Google Translator. Passamos como parâmetro da função `translate` da biblioteca a string a ser traduzida, seguida do seu destino, isto é, para que língua o texto deve ser traduzido.

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

Note que no código acima podemos buscar o texto original com a extensão `.origin` e o texto em si traduzido com `.text`.

## Método da Secante

Com base no exposto, finalmente podemos realizar a coleta dos dados e realizar uma inserção em um arquivo `.csv`, com as colunas "name", "date" e "link". No código a seguir, o loop é destinado por passar por todos os elementos encontrados e inserir no arquivo de destino.

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

Uma vez que o arquivo estava pronto, foi possível realizar a atualização de um arquivo já existente neste repositório (`\dados\dados.csv`) para que os dados desejados pudessem ser usados.


