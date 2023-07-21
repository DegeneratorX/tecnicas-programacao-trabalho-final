# Java Intermediário

Aqui abordarei alguns paradigmas intermediários da linguagem Java, principalmente relacionados a programação procedural.

# Classes

**Classes** são uma herança do **struct** do C mais elaborada, voltada para evitar repetições de linhas de código.

Tudo em Java é um objeto, e tudo trabalha com classes. Fará mais sentido no arquivo *3_JAVA_AVANÇADO.md*.

Por enquanto basta saber que a classe precisa sempre estar declarada no início do programa, e precisa ter o mesmo nome do arquivo. Por convenção, a classe possui letras maiúsculas nas iniciais.

```java
public class Main{
    ...
}
```

# Métodos

Como tudo é objeto, e tudo em Java está dentro de classes, então não existe funções convencionais. Todas as funções passam a ser métodos.

```java
public static int fala_oi(String parametro) {
    System.out.println(parametro);
    return 2 + 2;
}
public static void main(String[] a){
    int variavel = fala_oi("Oie"); // variavel recebe 4.
}
```

Os métodos funcionam da mesma forma do C e C++. Falarei sobre as keywords public, private e static depois.

# Lambdas

O único tipo de função que existe em Java são as funções anônimas, vistas também em Python.

```java
interface LambdaExpression {
    int apply(int x, int y);
}

public static void main(String[] args) {
    // Lê-se: defino objeto "multiply" recebendo x e y como parâmetros tal que produzo x*y.
    LambdaExpression multiply = (x, y) -> x * y; // Lambda sendo definida
    System.out.println(multiply.apply(2, 2));
}
```

Compare com python:

```python
multiply = lambda x, y: x * y
print(multiply(2, 2))
```

Perceba que **multiply** em Java é uma instância primitiva da interface LambdaExpression (LambdaExpression pode ser qualquer nome).

A necessidade de um tipo específico LambdaExpression é para que a função anônima tenha um tipo (pois Java é uma linguagem fortemente tipada), e isso é alcançado com o uso de interface.

O uso de **interfaces** é único em Java e será detalhado no arquivo *3_JAVA_AVANCADO.md*.

# Estrutura de dados (listas, tuplas, dicionários, sets)

Para esse caso, importamos a lib java.util.*.

### ArrayList

Muito parecido com o vector do C++ e list do Python. É um array dinâmico implementado na heap, e pode aumentar ou diminuir de tamanho. Implementa elementos bem próximos uns dos outros na memória.

```java
ArrayList<Integer> list = new ArrayList<>(); // Lista de inteiros.

list.add(5); // Equivalente ao push_back() em C++ ou append() em python.
list.add(10);

System.out.println(list.get(0)); // Acessando índices. Imprime 5.
System.out.println(list.get(1)); // Imprime 10.

list.set(1, 20); // Muda o segundo elemento de 10 para 20 pelo índice. Equivalente a list[1] = 20 no python.

list.remove(0); // Dá um pop no primeiro elemento. Dá para remover qualquer elemento pelo índice.
```

### Tupla

Para fazer algo equivalente as tuplas do python em Java, utilizamos a classe **Arrays**, que é uma classe utility que nos ajuda a trabalhar com arrays, e a interface **List**. Nesse caso iremos simular o funcionamento de uma tupla.

```java
List<Integer> tuple = Arrays.asList(5, 10, 15);
```

List não é uma classe, mas uma interface. ArrayList implementa a List para criar arrays, assim como a LinkedList, que não irei abordar aqui por ser trivial seu uso. Basta saber que a sintaxe para a tupla é dessa forma.

Nesse caso, Arrays.asList(5,10,15) retorna uma lista imutável.

### Dicionários (HashMap)

Dicionários possuem chave e valor.

```java
// Criação de um HashMap
HashMap<String, Object> d1 = new HashMap<String, Object>();
d1.put("chave1", "valor da chave1");
d1.put("chave2", 30);
```

### Conjuntos (HashSet)

Nos conjuntos, valores não se repetem.

```java
HashSet<Integer> s1 = new HashSet<Integer>();
s1.add(1);
s1.add(2);
```

# Try Catch (Exceções)

```java
public static void main(String[] args) {
    try {
        System.out.println(divide(2, 0));
    } catch (ArithmeticException e) {
        System.out.println("Você está tentando dividir por 0.");
        System.out.println(e.getMessage());  // Printará o erro.
    }
}

public static double divide(double n1, double n2) {
    if (n2 == 0) {
        throw new ArithmeticException("divisão por zero");  // Lançando a exceção ArithmeticException. Equivalente ao raise do Python.
    }
    return n1 / n2;
}
```

Funciona de forma muito parecida com python. Perceba que eu trato a própria exceção que levantei.

No Java existe uma particularidade na assinatura de métodos. É possível já declarar um levantamento de exceção caso o programa dê erro no método em tempo de execução. Isso é cosmético e não afeta o programa, mas é uma boa prática pra avisar ao desenvolvedor que tipo de erro pode ser levantado alí, seja com ou sem throw.

```java
public static int divide(int n1, int n2) throws ArithmeticException { // Boa prática
    if (denominator == 0) {
        throw new ArithmeticException("Não pode dividir por zero.");
    }
    return n1 / n2;
}
```

# Package e Módulos

Similar ao namespace do C++, serve para organizar a hierarquia de arquivos apenas.

É uma boa prática utilizar a keyword **package** para definir o local onde está o código.

Por exemplo:

```java
package pasta.example;

public class ClasseGenerica {
    // ...
}
```

Significa que esse arquivo está nesse diretório: scr/pasta/example/ClasseGenerica.java

Para importar arquivos .java para sua main, é necessário apenas declarar tudo na mesma package, e não precisa importar nada. Se tudo estiver no mesmo diretório de projeto, é possível instanciar outras classes em arquivos diferentes e assim trabalhar com ela.

# Arquivos

Para manipular arquivos, é um pouco mais complexo que no Python.

```java
private List<String> lerArquivo(String nomeDoArquivo) throws IOException {
    List<String> lista = new ArrayList<>();
    try (BufferedReader arq = new BufferedReader(new FileReader(nomeDoArquivo))) {
        String linha;
        while ((linha = arq.readLine()) != null) {
            linha = linha.trim(); // Retira espaços das linhas
            if (linha.contains("\n")) { // Se contém o caractere de \n
                linha.replace("\n", ""); // Retira ele
            }
            lista.add(linha); // Adiciono na lista
        }
    } catch (IOException e) {
        System.out.println("Erro ao ler arquivo");
        e.printStackTrace();
    }
    return lista;
}
```

O código acima basicamente lê o arquivo, tira espaços, tira \n e adiciona linha por linha em uma estrutura de dados de array de forma bem separada. Caso dê erro, ele trata a exceção. No final retorna a lista.

As classes BufferedReader e FileReader pertencem ao pacote java.io.*.