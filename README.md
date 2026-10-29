# Adaline para uma função lógica AND com entrada e alvo bipolar(1,-1)

## 1. Descrição do projeto

Este projeto implementa, em Java, um exemplo de treinamento de uma rede neural artificial **ADALINE** (*Adaptive Linear Neuron*) para aprender a função lógica **AND** com entradas e alvos bipolares (`1` e `-1`). O código é baseado no Exemplo 2.17, página 83, do livro *Fundamentals of Neural Networks*, de Laurene V. Fausett.

Durante o treinamento, a rede calcula uma saída linear para cada padrão de entrada e ajusta os pesos e o bias de acordo com o erro entre a saída calculada e o alvo desejado. Após o treinamento, o programa permite executar testes interativos por meio de caixas de diálogo.

## 2. Objetivos

- Implementar o algoritmo ADALINE em Java para a função lógica AND.
- Utilizar entradas e alvos representados por valores bipolares.
- Inicializar os pesos com valores fixos e o bias com um valor aleatório.
- Ajustar os pesos e o bias durante o treinamento.
- Calcular o erro quadrático total do conjunto de treinamento.
- Registrar estatísticas das épocas e permitir testes interativos da rede treinada.

## 3. A função lógica AND com entradas bipolares

Neste exemplo, os valores das entradas são representados de forma bipolar: `1` e `-1`. O alvo é `1` quando ambas as entradas são `1`; nos demais casos, o alvo é `-1`.

| Entrada `x1` | Entrada `x2` | Alvo |
|---:|---:|---:|
| 1 | 1 | 1 |
| 1 | -1 | -1 |
| -1 | 1 | -1 |
| -1 | -1 | -1 |

Os quatro padrões são armazenados na matriz `s`, e os alvos correspondentes são armazenados no vetor `alvo`. A variável `num` informa a quantidade de padrões de treinamento, enquanto `n` define a quantidade de entradas por padrão.

## 4. Conceito de ADALINE

ADALINE é a sigla de *Adaptive Linear Neuron*. O modelo calcula uma combinação linear das entradas com seus respectivos pesos e adiciona o bias. A diferença entre o alvo desejado e a saída linear é usada para ajustar os parâmetros da rede durante o treinamento.

A saída linear é calculada por:

\[
y_{in} = \sum_{i=1}^{n} x_i w_i + b
\]

Em que:

- `x_i` representa uma entrada;
- `w_i` representa o peso associado à entrada;
- `b` representa o bias;
- `n` é a quantidade de entradas;
- `y_in` é a saída linear calculada.

O erro para cada padrão é:

\[
erro = t - y_{in}
\]

Em que `t` representa o alvo desejado.

## 5. Ajuste dos pesos e do bias

O programa utiliza a taxa de aprendizagem `alfa` para atualizar os pesos com base no erro calculado.

A atualização de cada peso é:

\[
w_i \leftarrow w_i + \alpha \cdot erro \cdot x_i
\]

A atualização do bias é:

\[
b \leftarrow b + \alpha \cdot (t-y_{in})
\]

No código, a taxa de aprendizagem é `0.02`. As atualizações são feitas após o cálculo do erro de cada padrão, portanto os padrões seguintes da mesma época são processados com os parâmetros atualizados.

## 6. Como o programa funciona

O programa está implementado no método `main` da classe `Principal` e realiza as seguintes etapas:

1. Define os quatro padrões bipolares da função AND e os respectivos alvos.
2. Define a quantidade de padrões, a quantidade de entradas, a taxa de aprendizagem e o número máximo de épocas.
3. Inicializa o bias com um valor aleatório e define os dois pesos iniciais como `1`.
4. Calcula o erro quadrático inicial do conjunto de treinamento.
5. Inicia o treinamento enquanto o número de épocas for menor que o limite e o erro total for maior que o limiar.
6. Para cada padrão, calcula a saída linear, determina o erro e atualiza os pesos e o bias.
7. Armazena as estatísticas de cada época em uma string e as apresenta ao final do treinamento.
8. Pergunta se o usuário deseja testar a rede.
9. Quando solicitado, permite selecionar um padrão pelo índice e calcula sua saída.
10. Aplica a função de ativação bipolar: retorna `1` se `y_in >= 0` e `-1` caso contrário.

### 6.1 Parâmetros utilizados

| Parâmetro | Valor utilizado | Significado |
|---|---:|---|
| `num` | `4` | Quantidade de padrões do conjunto de treinamento. |
| `n` | `2` | Quantidade de entradas por padrão. |
| `alfa` | `0.02` | Taxa de aprendizagem usada na atualização dos pesos e do bias. |
| `omega` | `0.1` | Variável declarada como *threshold*, mas não utilizada nos cálculos do código atual. |
| `epoca` | `1000` | Número máximo de épocas de treinamento. |
| `limiar` | `1.25` | Limite do erro quadrático total usado como condição de parada. |
| `conta_epoca` | Inicialmente `0` | Contador das épocas executadas. |
| `b` | Aleatório | Bias inicial, gerado por `Math.random()`. |
| `w` | `{1, 1}` | Pesos iniciais das duas entradas. |

O treinamento termina quando o erro quadrático total fica menor ou igual a `1.25`, ou quando são alcançadas `1000` épocas. Como o bias inicial é aleatório, os resultados do treinamento podem variar entre execuções.

## 7. Principais métodos e recursos

O código fornecido concentra a implementação no método `main`; não há métodos auxiliares definidos na classe `Principal`.

| Método ou recurso | Responsabilidade |
|---|---|
| `main(String args[])` | Ponto de entrada do programa. Define os padrões de treinamento, inicializa os parâmetros, executa o treinamento e conduz os testes interativos. |
| `Math.random()` | Gera o valor inicial aleatório do bias. |
| `Math.pow(erro, 2)` | Calcula o quadrado do erro de cada padrão para acumular o erro quadrático total. |
| `String.format("%.4f", valor)` | Formata os valores numéricos das estatísticas com quatro casas decimais. |
| `JOptionPane.showInputDialog(...)` | Exibe caixas de diálogo para perguntar se o usuário deseja testar a rede e qual padrão deseja executar. |

### 7.1 Tecnologias e ferramentas

| Tecnologia ou ferramenta | Utilização |
|---|---|
| **Java 8 (JDK 8)** | Linguagem e ambiente de desenvolvimento utilizados para implementar e executar o programa. |
| **Apache Maven** | Gerencia a estrutura do projeto, as configurações de compilação e as tarefas definidas no arquivo `pom.xml`. O código apresentado não possui dependências externas explícitas. |
| `java.lang.Math` | Fornece os métodos `random()` e `pow()`, utilizados na inicialização do bias e no cálculo do erro quadrático. A classe `Math` é importada implicitamente pelo Java. |
| `javax.swing.JOptionPane` | Exibe caixas de diálogo para a interação com o usuário durante os testes. |
| `String.format()` | Formata os valores numéricos exibidos nas estatísticas do treinamento. |

## 8. Requisitos

- **JDK 8** ou versão compatível.
- **Apache Maven** instalado e configurado, caso a compilação e a execução sejam realizadas por Maven.
- Ambiente com interface gráfica para utilizar as caixas de diálogo do `JOptionPane`.
- Terminal ou prompt de comando para executar os comandos Maven.

## 9. Estrutura do projeto

Considerando a estrutura convencional de um projeto Maven, os arquivos podem estar organizados da seguinte forma:

```text
adaline-and-bipolar/
├── pom.xml
├── README.md
└── src/
    └── main/
        └── java/
            └── Principal.java
```

O arquivo `Principal.java` contém o treinamento e os testes. O arquivo `pom.xml` define as configurações do projeto Maven. Se o projeto utilizar um pacote Java ou uma estrutura diferente, ajuste essa representação para corresponder à organização real dos arquivos.

## 10. Compilação e execução

Na pasta raiz do projeto, onde está localizado o `pom.xml`, execute:

```bash
mvn clean package
```

Esse comando limpa os arquivos de compilação anteriores e empacota o projeto. A forma exata de execução depende das configurações definidas no `pom.xml`.

Se o projeto estiver configurado com o plugin Maven Exec, execute:

```bash
mvn exec:java -Dexec.mainClass="Principal"
```

Se a classe `Principal` estiver dentro de um pacote, utilize o nome totalmente qualificado, por exemplo `br.edu.exemplo.Principal`.

Em um projeto simples sem pacote, também é possível compilar e executar diretamente pelo JDK:

```bash
javac -d target/classes src/main/java/Principal.java
java -cp target/classes Principal
```

## 11. Saída e interação do programa

Durante o treinamento, o programa apresenta:

- Mensagem de início do treinamento.
- Número da época atual.
- Entradas, taxa de aprendizagem, saída linear, alvo, pesos e bias.
- Erro quadrático total e limiar ao final do treinamento.
- Mensagem de início dos testes.

Na etapa de testes, o usuário informa se deseja realizar um teste e seleciona o índice do padrão. Os índices válidos são `0`, `1`, `2` e `3`, correspondentes às quatro linhas da matriz `s` e do vetor `alvo`. O resultado apresenta o padrão escolhido, seu alvo e a saída bipolar calculada.

## 12. Observações sobre a implementação

- A variável `gerador`, criada com `new java.util.Random()`, não é utilizada. O bias inicial é gerado por `Math.random()`.
- A variável `omega` é declarada como *threshold*, mas não participa dos cálculos apresentados.
- Os pesos são inicializados com o valor `1`, enquanto o bias é inicializado aleatoriamente.
- O erro quadrático total é calculado antes do treinamento e recalculado em cada época. A condição de parada utiliza o valor acumulado durante a última época executada.
- O código atualiza os pesos e o bias imediatamente após processar cada padrão de treinamento.
- A saída `y_in` usada para calcular o erro é linear. A função de ativação bipolar é aplicada somente na etapa de testes.
- O programa não valida os valores informados pelo usuário. O índice escolhido deve estar entre `0` e `3`, e as respostas às caixas de diálogo devem ser números inteiros válidos.
- A variável `saida` acumula as estatísticas de todas as épocas em uma única `String`, o que pode aumentar o consumo de memória em execuções longas.
- A apresentação decimal de `String.format()` pode variar conforme a configuração regional do sistema.

## 13. Limitações

- O programa trabalha apenas com os quatro padrões definidos para a função AND com duas entradas bipolares.
- O bias inicial é aleatório, de modo que os resultados podem variar entre execuções.
- O treinamento é limitado a `1000` épocas e utiliza um limiar de erro fixo em `1.25`.
- Não há validação dos dados digitados durante os testes.
- A interface utiliza `JOptionPane`, exigindo um ambiente gráfico.
- A implementação está concentrada no método `main`, o que limita a modularidade e a reutilização do código.

## 14. Referência

FAUSETT, Laurene V. *Fundamentals of Neural Networks: Architectures, Algorithms, and Applications*. Exemplo 2.17, p. 83.

