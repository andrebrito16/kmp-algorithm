[Desafios de Programação](https://ensino.hashi.pro.br/desprog/)

Algoritmo de Knuth-Morris-Pratt (KMP) 
======

++++++++++++++++++++++++++++++++++++++++++
Desafios de Programação

**Aula 22: Knuth-Morris-Pratt (KMP)**
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ História KMP
- +^É uma das soluções mais eficientes para o problema de correspondência de padrões em uma string.

- +^Desenvolvido em 1977 pelos pesquisadores Donald Knuth, James Morris e Vaughan Pratt

- +^Processamento de Linguagem Neural, Ánalise de Dados e Bioinformática

++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
- +^O algoritmo KMP compara o primeiro caractere do padrão (frase ou palavra) com o primeiro caractere do texto.
- +^Se os demais caracteres tiverem correspondência, a comparação ocorre caractere por caractere até encontrar uma diferença.
- +^Quando uma diferença é encontrada, o algoritmo utiliza uma tabela para determinar o salto necessário para o próximo caractere.

++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento00.png)
++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento01.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento02.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento03.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento04.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento05.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento06.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento07.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento08.png)
++++++++++++++++++++++++++++++++++++++++++ 

++++++++++++++++++++++++++++++++++++++++++ =
![](Funcionamento/Funcionamento09.png)
++++++++++++++++++++++++++++++++++++++++++

++++++++++++++++++++++++++++++++++++++++++ Vantagens do Algoritmo
- +Eficiência: Evita comparações desnecessárias, resultando em um processo de busca mais rápido.

- +Utilização da tabela: A tabela auxilia no cálculo dos saltos, otimizando a localização dos padrões.
++++++++++++++++++++++++++++++++++++++++++

++++++++++++++++++++++++++++++++++++++++++
**Handout**

- ^Agora podem tanto fazer individualmente quanto em grupo…

- ^…e discussões em grupo podem de fato fazer diferença…

- ^…mas, em algum momento, é importante fazer individualmente.

- ^Se há gabarito, veja só em último caso.
++++++++++++++++++++++++++++++++++++++++++

++++++++++++++++++++++++++++++++++++++++++
**Observações**

- ^Aprendizado ativo é fazer, não ler.

- ^Exceto em um ou outro caso excepcional, uma atividade é possível sem consulta além do material de aula dado até o momento.

- ^Além disso, muitas vezes a resposta da atividade é necessária para a compreensão do restante.

- ^Ou seja, “deixar para entender depois” não faz sentido. “Depois” depende de “entender”.
++++++++++++++++++++++++++++++++++++++++++

1.O Problema da Busca de Substrings
-------
A busca de substrings é um problema comum em ciência da computação. A questão é: dado um texto e um padrão, podemos encontrar todas as ocorrências do padrão dentro do texto?

A solução mais simples, mas também a mais lenta, é verificar cada substring do texto em sequência para ver se ela corresponde ao padrão, a chamada força bruta. No entanto, essa abordagem tem uma complexidade de tempo de O(nm), onde n é o comprimento do texto e m é o comprimento do padrão. Isso é muito ineficiente, especialmente para textos longos.

Felizmente, existem algoritmos mais rápidos. O Algoritmo de Knuth-Morris-Pratt (KMP) é um desses algoritmos. Em vez de se mover um caractere por vez, como na busca de padrões convencional, ele permite que você **"pule"** partes do texto com base no conhecimento adquirido até o momento.

2.Compreendendo os Prefixos e Sufixos de Prefixos
-------
No contexto do algoritmo KMP, prefixos são partes iniciais do padrão. Para o padrão **"ABCDE"**, os prefixos são **"A"**, **"AB"**, **"ABC"**, **"ABCD"**, excluindo-se a própria string original.

??? Checkpoint 1 

**a)** Quais são os prefixos da palavra **"INFORMATICA"**?  
**b)** Quantos prefixos existem? Descreva o processo de como você chegou a essa resposta.  

::: Gabarito
**a)** Os prefixos da palavra **"INFORMATICA"** são **"I"**, **"IN"**, **"INF"**, **"INFO"**, **"INFOR"**, **"INFORM"**, **"INFORMA"**, **"INFORMAT"**, **"INFORMATI"**, **"INFORMATIC"**.  
**b)** Existem 10 prefixos. Para encontrar esses prefixos, começamos do primeiro caractere e vamos adicionando um caractere de cada vez até chegar ao penúltimo.     
:::
???

Um sufixo de prefixo é qualquer sufixo que pode ser extraído de um prefixo do padrão. No caso do prefixo **"ABC"**, temos dois sufixos: **"BC"** e **"C"**.

??? Checkpoint 2  
Quais são os sufixos possíveis para cada prefixo da palavra **"INFORMATICA"** que você encontrou no checkpoint 1?
::: Gabarito
Os sufixos de cada prefixo são os seguintes:  
"I": nenhum sufixo  
"IN": **"N"**  
"INF": **"NF"**, **"F"**  
"INFO": **"NFO"**, **"FO"**, **"O"**  
"INFOR": **"NFOR"**, **"FOR"**, **"OR"**, **"R"**  
E assim por diante.  
:::
???

**Mas por que precisamos saber sobre prefixos e sufixos?**  
  
Vamos dizer que estamos procurando o padrão **"ABCABC"** dentro de um texto e encontramos um match parcial - **"ABCAB"**, mas o próximo caractere no texto é **"D"**, não **"C"**. Isso significa que temos um desajuste. Em um algoritmo de busca normal, começaríamos a busca novamente a partir do próximo caractere.

No entanto, o algoritmo KMP faz algo mais inteligente. Ele observa o match parcial ("ABCAB") e verifica se há algum sufixo deste match parcial que corresponda a um prefixo do padrão original. Neste caso, **"AB"** no final de **"ABCAB"** é um sufixo do match parcial e também um prefixo do padrão original **"ABCABC"**. Isso significa que podemos **"saltar"** para o próximo local no texto que alinha este sufixo **"AB"** com o prefixo **"AB"** do padrão original na próxima etapa da busca, pois já sabemos que a parte **"AB"** é uma correspondência válida.

Assim, em vez de mover um caractere de cada vez, **o algoritmo KMP pode mover vários caracteres de uma vez**, tornando a busca muito mais eficiente. Essa é a ideia central do algoritmo KMP.

![](pikachu.jpg)


3.A tabela LPS
-------

A tabela LPS é uma representação pré-computada (cache) que armazena informações sobre cada prefixo do padrão e o tamanho do maior sufixo desse prefixo que também é um prefixo. Esse tamanho é usado como um índice que indica quantos caracteres a palavra ou frase deve avançar.

:tabela_prefixo

Agora que aprendemos, vamos fazer alguns exercícios para fixar o conteúdo.
??? Exercício 1 

Construa a tabela de prefixos e sufixos para:

![](Exercicios/Exercicio1.png)

::: Gabarito
![](Gabaritos/Gabarito1.png)
:::
::: Gabarito Detalhado
:Gabarito_Detalhado_1
:::
???
??? Exercício 2 

Construa a tabela de prefixos e sufixos para:

![](Exercicios/Exercicio2.png)

::: Gabarito
![](Gabaritos/Gabarito2.png)
:::
::: Gabarito Detalhado
:Gabarito_Detalhado_2
:::
???
??? Exercício 3 

Construa a tabela de prefixos e sufixos para:

![](Exercicios/Exercicio3.png)


::: Gabarito
![](Gabaritos/Gabarito3.png)
:::
::: Gabarito Detalhado
:Gabarito_Detalhado_3
:::

???
!!!
Escrever mais (explicação dos exercícios, etc) e falar da complexidade
!!!

4.Pulo com a tabela
--------

Agora que entendemos como acontece o pulo com a tabela de prefixos/sufixos

:Funcionamento

5.Implementação em C
-------

O KMP usa uma tabela de falhas (também conhecida como tabela de borda) para armazenar informações sobre o padrão que são usadas para evitar comparações repetidas. A tabela de falhas é construída antes de iniciar a correspondência de padrões e é baseada no padrão a ser encontrado.

!!!
A ser melhorado
!!!

???
Como seria uma implementação do algoritmo KMP em C?

:::
Aqui está um exemplo de implementação do algoritmo KMP em C:

```c
#include <stdio.h>
#include <string.h>

void preencher_tabela(int tabela[], char padrao[])
{
    int tam_padrao = strlen(padrao);
    int i = 0, j = -1;
    tabela[0] = -1;

    while (i < tam_padrao)
    {
        while (j >= 0 && padrao[i] != padrao[j])
        {
            j = tabela[j];
        }

        i++;
        j++;
        tabela[i] = j;
    }
}

void encontrar_padrao(char texto[], char padrao[])
{
    int tam_texto = strlen(texto);
    int tam_padrao = strlen(padrao);
    int tabela[tam_padrao];
    preencher_tabela(tabela, padrao);
    int i = 0, j = 0;

    while (i < tam_texto)
    {
        while (j >= 0 && texto[i] != padrao[j])
        {
            j = tabela[j];
        }

        i++;
        j++;

        if (j == tam_padrao)
        {
            printf("Padrao encontrado na posicao %d\n", i - j);
            j = tabela[j];
        }
    }
}

int main()
{
    char texto[] = "ababcabcabababcabcabc";
    char padrao[] = "abcabc";
    encontrar_padrao(texto, padrao);
    return 0;
}
```
:::
???

