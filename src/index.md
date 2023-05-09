Main page
======

## 6. Comparação com outros algoritmos

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
