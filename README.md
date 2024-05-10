A busca em profundidade (DFS - *Depth-First Search*) é um algoritmo usado para explorar grafos ou árvores. Ele começa em um nó inicial e explora tanto quanto possível ao longo de cada ramo antes de retroceder.

### 1. Conceito Básico
A DFS é útil para encontrar caminhos, componentes conectados e ciclos em grafos. Ela pode ser implementada de forma recursiva ou usando uma pilha.

### 2. Implementação em C++
Vou te mostrar uma implementação de DFS usando um grafo representado como lista de adjacência.

### 3. Exemplo Prático
#### Código em C++
```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Grafo {
private:
    int numVertices;
    vector<vector<int>> adj;
    void dfsRecursivo(int v, vector<bool>& visitado);

public:
    Grafo(int vertices);
    void adicionarAresta(int v, int w);
    void dfs(int v);
    void dfsIterativa(int v);
};

Grafo::Grafo(int vertices) {
    numVertices = vertices;
    adj.resize(vertices);
}

void Grafo::adicionarAresta(int v, int w) {
    adj[v].push_back(w);
}

void Grafo::dfsRecursivo(int v, vector<bool>& visitado) {
    visitado[v] = true;
    cout << v << " ";

    for (int i : adj[v]) {
        if (!visitado[i]) {
            dfsRecursivo(i, visitado);
        }
    }
}

void Grafo::dfs(int v) {
    vector<bool> visitado(numVertices, false);
    dfsRecursivo(v, visitado);
    cout << endl;
}

void Grafo::dfsIterativa(int v) {
    vector<bool> visitado(numVertices, false);
    stack<int> pilha;

    pilha.push(v);

    while (!pilha.empty()) {
        v = pilha.top();
        pilha.pop();

        if (!visitado[v]) {
            cout << v << " ";
            visitado[v] = true;
        }

        for (int i = adj[v].size() - 1; i >= 0; --i) {
            int adjacente = adj[v][i];
            if (!visitado[adjacente]) {
                pilha.push(adjacente);
            }
        }
    }
    cout << endl;
}

int main() {
    Grafo g(5);
    g.adicionarAresta(0, 1);
    g.adicionarAresta(0, 2);
    g.adicionarAresta(1, 3);
    g.adicionarAresta(1, 4);
    g.adicionarAresta(2, 4);

    cout << "Busca em Profundidade (DFS) Recursiva a partir do vértice 0:\n";
    g.dfs(0);

    cout << "Busca em Profundidade (DFS) Iterativa a partir do vértice 0:\n";
    g.dfsIterativa(0);

    return 0;
}
```

### 4. Explicação do Código
- **Classe `Grafo`**:
  - Contém a lista de adjacência (`adj`) e métodos para adicionar arestas e realizar a busca em profundidade.

- **Método `adicionarAresta`**:
  - Adiciona uma aresta direcionada entre dois vértices.

- **Método `dfsRecursivo`**:
  - Função recursiva que executa a DFS.
  - Marca o vértice atual como visitado e explora todos os vértices adjacentes que não foram visitados.

- **Método `dfs`**:
  - Inicializa o vetor `visitado` e chama a função `dfsRecursivo`.

- **Método `dfsIterativa`**:
  - Implementação iterativa da DFS usando uma pilha.
  - Marca o vértice inicial como visitado e adiciona seus adjacentes na pilha.

### 5. Complexidade do Algoritmo
- **Tempo**: `O(V + E)`, onde `V` é o número de vértices e `E` é o número de arestas.
- **Espaço**: `O(V)`, devido ao vetor de visitados e à pilha/recursão.

### 6. README Exemplo
Aqui está um exemplo de um `README.md` que explica a DFS:

```markdown
# Implementação de Busca em Profundidade (DFS) em C++

## Objetivo
Este repositório tem como objetivo fornecer uma explicação e implementação prática de um algoritmo de busca em profundidade (DFS) em C++.

## Conteúdo
- [Motivação](#motivação)
- [Explicação do Algoritmo](#explicação-do-algoritmo)
- [Complexidade do Algoritmo](#complexidade-do-algoritmo)
- [Implementação](#implementação)
- [Como Executar](#como-executar)
- [Referências](#referências)

## Motivação
A DFS é um algoritmo de busca fundamental para explorar grafos. Ela é útil para encontrar componentes conectados, detectar ciclos e executar tarefas como ordenação topológica e encontrar caminhos.

## Explicação do Algoritmo
### Passos
1. **Inicialização**: Crie um vetor `visitado` para marcar os vértices visitados.
2. **Exploração**:
   - Se recursivo, implemente uma função `dfsRecursivo`.
   - Se iterativo, use uma pilha.
3. **Visitar**:
   - Marque o vértice como visitado.
   - Imprima ou processe o vértice.
   - Explore os adjacentes não visitados.

### Diagrama do Processo
```
Inicialização --> Visitar vértice inicial
   |
   V
Explorar adjacentes --> Adjacente já visitado?
   |                         |
   Não                        Sim
   |                         |
Visitar vértice        Retroceder
```

## Complexidade do Algoritmo
**Tempo**:
- **Melhor caso**: `O(V + E)` (explora todos os vértices e arestas)

**Espaço**:
- **Recursivo**: `O(V)` (devido à recursão)
- **Iterativo**: `O(V)` (devido à pilha)

## Implementação
### Implementação em C++
```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Grafo {
private:
    int numVertices;
    vector<vector<int>> adj;
    void dfsRecursivo(int v, vector<bool>& visitado);

public:
    Grafo(int vertices);
    void adicionarAresta(int v, int w);
    void dfs(int v);
    void dfsIterativa(int v);
};

Grafo::Grafo(int vertices) {
    numVertices = vertices;
    adj.resize(vertices);
}

void Grafo::adicionarAresta(int v, int w) {
    adj[v].push_back(w);
}

void Grafo::dfsRecursivo(int v, vector<bool>& visitado) {
    visitado[v] = true;
    cout << v << " ";

    for (int i : adj[v]) {
        if (!visitado[i]) {
            dfsRecursivo(i, visitado);
        }
    }
}

void Grafo::dfs(int v) {
    vector<bool> visitado(numVertices, false);
    dfsRecursivo(v, visitado);
    cout << endl;
}

void Grafo::dfsIterativa(int v) {
    vector<bool> visitado(numVertices, false);
    stack<int> pilha;

    pilha.push(v);

    while (!pilha.empty()) {
        v = pilha.top();
        pilha.pop();

        if (!visitado[v]) {
            cout << v << " ";
            visitado[v] = true;
        }

        for (int i = adj[v].size() - 1; i >= 0; --i) {
            int adjacente = adj[v][i];
            if (!visitado[adjacente]) {
                pilha.push(adjacente);
            }
        }
    }
    cout << endl;
}

int main() {
    Grafo g(5);
    g.adicionarAresta(0, 1);
    g.adicionarAresta(0, 2);
    g.adicionarAresta(1, 3);
    g.adicionarAresta(1, 4);
    g.adicionarAresta(2, 4);

    cout << "Busca em Profundidade (DFS) Recursiva a partir do vértice 0:\n";
    g.dfs(0);

    cout << "Busca em Profundidade (DFS) Iterativa a partir do vértice 0:\n";
    g.dfsIterativa(0);

    return 0;
}
```

## Como Executar
1. Certifique-se de que você tem um compilador C++ instalado.
2. Salve o código acima em um arquivo, por exemplo, `dfs.cpp`.
3. Compile o arquivo usando um compilador C++:
   ```bash
   g++ -o dfs dfs.cpp
   ```
4. Execute o programa:
   ```bash
   ./dfs
   ```

## Referências
- [GeeksforGeeks - Depth First Search](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a
