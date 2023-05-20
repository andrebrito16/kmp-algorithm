[Desafios de Programação](https://ensino.hashi.pro.br/desprog/)

Algoritmo de Knuth-Morris-Pratt (KMP) 
======

1.Introdução
-------

O algoritmo de Knuth-Morris-Pratt (KMP) é uma das soluções mais eficientes para o problema de correspondência de padrões em uma string. Esse problema é muito importante em diversas áreas, como processamento de linguagem natural, análise de dados e bioinformática.

Desenvolvido em 1977 pelos pesquisadores Donald Knuth, James Morris e Vaughan Pratt, o algoritmo KMP tem sido amplamente utilizado em diversas aplicações, desde então.

Este handout tem como objetivo apresentar o funcionamento detalhado do algoritmo KMP, como ele pode ser implementado e otimizado, e como ele se compara com outros algoritmos de correspondência de padrões. Além disso, também exploraremos alguns exemplos práticos do uso do algoritmo.

2.E por que estudar o algoritmo KMP?
-------

Sabe quando você quer encontrar uma frase ou palavra, e para isso usa o famoso CTRL + F, ele costuma indicar as posições das ocorrências ou mostrar que ela não está presente no texto.

O algoritmo torna esse processo mais rápido, evitando repetições de comparações desnecessárias, a gente vai aprender um pouco mais na frente, mas ele usa uma tabela para auxiliar o processo. 
Começando o algoritmo compara o primeiro caractere do padrão (frase ou palavra) com o primeiro caractere do texto, caso os demais caracteres tenham correspondência, ele compara caractere por caractere, até encontrar uma diferença. Encontrada a diferença, o algoritmo vai usar a tabela para saber o quanto deve “pular” para o próximo caractere. 

Sendo o KMP um poderoso algoritmo para solucionar o problema de correspondência de padrões de forma rápida e eficiente.

!!!
Essa parte 2 ("E por que estudar o algoritmo KMP?") poderia ser um expositvo? Ou melhor em texto?
!!!

3.Como funciona o algoritmo KMP?
-------

Ele faz as correspondências do texto, porém quando encontra um caractere diferente, ele procura o índice na tabela desse caractere, e a partir dele sabe-se o quanto deve seguir para os próximos caracteres. 

!!!
IDEIAS: fazer slides que mostram melhor esse “pulo” de acordo com a tabela.
!!!

???
Como acha a tabela do algoritmo?

:::Resposta

A tabela tão falada é de sufixos e prefixos, então com os caracteres que queremos, fazemos os sufixos e os prefixos deles e pegamos o maior tamanho entre os sufixos e prefixos iguais, sendo esse o índice e o indicativo de quanto a nossa palavra ou frase deve pular.

:tabela
:::
???

!!!
IDEIAS: fazer slides para mostrar como acha a tabela
!!!


4.Implementação em C
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

6.Comparação com outros algoritmos
-------

Existem diversos algoritmos para solucionar o problema de correspondência de padrões, cada um com suas próprias características e complexidades.

O algoritmo de força bruta é a solução mais simples para o problema de correspondência de padrões. Ele consiste em percorrer a string de texto e comparar o padrão com cada uma das substrings. Esse método tem complexidade de tempo O(nm), onde n é o tamanho da string e m é o tamanho do padrão. Apesar de sua simplicidade, esse algoritmo não é eficiente para strings grandes ou padrões longos, já que ele realiza muitas comparações desnecessárias.

``` c
// pseudocódigo em C do algoritmo de força bruta
int bruteForce(char* texto, char* padrao) {
    int n = strlen(texto); // Tamanho da string de texto
    int m = strlen(padrao); // Tamanho da string de padrão
    int i, j; // Índices para percorrer as strings

    for (i = 0; i <= n - m; i++) { // Percorre a string de texto
        for (j = 0; j < m; j++) { // Percorre a string de padrão
            if (texto[i+j] != padrao[j]) // Se encontrar uma diferença, sai do loop interno
                break;
        }
        if (j == m) // Se o índice j chegou ao final do padrão, significa que encontrou uma ocorrência
            return i;
    }

    return -1; // Se não encontrou ocorrência, retorna -1
}
```

O algoritmo de Boyer-Moore, assim como o KMP, utiliza informações sobre a string e o padrão para evitar comparações desnecessárias. Ele é considerado um dos algoritmos mais rápidos para o problema de correspondência de padrões na prática, com uma complexidade de tempo média O(n/m). O algoritmo utiliza duas heurísticas: o salto ruim (bad character rule) e o salto bom (good suffix rule), para determinar o deslocamento necessário na string de texto.

``` c
// TODO: pseudocódigo em C do algoritmo de Boyer-Moore
```

No entanto, é importante lembrar que a eficiência dos algoritmos depende das características específicas da string e do padrão em questão. Por isso, é importante avaliar o desempenho de cada algoritmo para cada caso específico.

Ainda não foram realizados testes para comparar o desempenho do algoritmo KMP com os algoritmos de força bruta e Boyer-Moore. Na próxima sprint, vamos apresentar os resultados desses testes e comparar o desempenho dos algoritmos para diferentes tamanhos de string e padrão.

## TABELA MERAMENTE ILUSTRATIVA 

| Tamanho da string | Tamanho do padrão | Força Bruta | KMP | Boyer-Moore |
|-------------------|-------------------|-------------|-----|-------------|
| 10^4              | 10                | 0.003s      | 0.001s | 0.002s      |
| 10^5              | 100               | 0.308s      | 0.011s | 0.001s      |
| 10^6              | 1000              | 32.5s       | 0.125s | 0.008s      |

