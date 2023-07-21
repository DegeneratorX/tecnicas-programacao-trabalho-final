# Java Introdutório

Possuo no meu github 3 repositórios gigantescos de Python, do básico, procedural e POO. Não irei fazer o mesmo aqui. Apenas irei colocar resumidamente (baseado no Python e C++) os conceitos básicos de Java, para ajudar na disciplina de Técnicas de Programação 2023.1.

Portanto, os pré-requisitos para entender esses arquivos .md são:

- Noção do básico, intermediário e POO em Python ou C++.

O motivo é bem simples. Já documentei muita coisa sobre essas duas linguagens. Seria redundante abordar coisas tão semelhantes novamente, mas nesse repositório. Tudo será muito resumido apenas pra familiarizar.

# Instalação

Java é uma linguagem interpretada. Precisa do JDK para funcionar. Porém, funciona em qualquer máquina.

Para instalar, basta no windows ir no site da Oracle. No caso do Linux, se já não vier pré-instalado, use os comandos:

```batch
sudo apt-get install default-jdk
```

E para verificar se instalou, use:

```batch
java -version
```

# Primeiro programa

Para criar um arquivo Java (assim como .py), deve-se terminar com **.java**.

O arquivo que estiver com a função Main precisa ter o mesmo nome da classe que habita essa função. Coisas do java, fazer o quê.

```java
// Nome do arquivo: Main.class
// Faça isso ou dará erro.
public class Main{
    public static void main(String[] args){
        System.out.println("Olá, mundo");
    }
}
```

Tudo é objeto no Java, e tudo precisa estar dentro de uma classe, inclusive a main(). Funciona mais ou menos como o namespace do C++. Portanto, funções aqui passam a serem métodos sem exceção. A única função que existe no Java é a lambda (anônima).

Classes, métodos e atributos public, protected e private funcionam igual no python, mas são mais eficientes no Java.

A keyword **static** sempre será atrelada a atributos e métodos de uma classe, afinal é impossível ter funções ou variáveis static, já que a linguagem não é funcional, e portanto o static não pode ter aqueles comportamentos do C++, que guardam valores em memória estática.

A keyword **void** é porque o método main() nunca pode retornar nada. E o método main() recebe parâmetros em string no começo da execução, que serão guardados dentro de um array de argumentos **args** (poderia ser qualquer nome).

Por fim, imprimir no terminal é através da biblioteca/classe built-in **System** (java.lang.System), que trabalha com entrada e saída de dados no sistema. Ao acessar um atributo como **out** dentro da classe System, que é público e static (independe de instância), na verdade estamos acessando uma instância da classe PrintStream, que possui métodos como printf(), print() e println(), sendo esse último equivalente ao print() do python.

# for, ifs, whiles, tipos primitivos...

Esses carinhas funcionam da mesma forma do C++, mas existe meios mais simples de trabalhar com **for** hoje em dia, basicamente iterando como no python.

```java
// Estilo Java
for (int i = 0; i < this.lista.size(); i++) {
    System.out.println(lista.get(i));
}
```

```java
// Novo estilo. Itera sobre a lista e imprime tudo dela.
for (String s : this.lista) {
    System.out.println(s);
}
```

Sobre tipos primitivos de dados, não irei abordar. É a mesma coisa do C++. Acredito que o que muda é o uso de String. No C++ usa-se muito std::string ou const char*, mas aqui é a classe String.

# Input

Essa é a forma em Java de ler entrada de dados do usuário no terminal (como a função scanf() em c, cin no c++ ou input() no python):

```java
Scanner scanner = new Scanner(System.in); // Instancio um objeto que vai ler entradas
System.out.print("Digite seu nome: ");
String nome = scanner.nextLine(); // recebe os dados
System.out.print("Digite sua idade: ");
String idade = Integer.parseInt(scanner.nextLine());
```

Assim como em python, o input recebe String, e é preciso converter (casting) o tipo caso deseje. Nesse caso converto de String para Inteiro.

# Arrays

Sendo um pouco diferente do C++ na declaração e na forma como se cria arrays, todos os arrays são objetos guardados na heap.

```java
int array[] = new int[10]; // Vetor de tamanho 10
int matriz[][] = new int[4][5]; // Matriz de 4 linhas e 5 colunas

array[7] = 200 // acesso a elementos do array
matriz[2][1] = 233; // acesso a elementos da matriz
```

A forma como se cria é bem mais simples que C++. Lembrando que não existe ponteiros explícitos em Java.

# Print

Existem formas diferentes de imprimir valores no terminal.

### println() pula 1 linha no término da função.
```java
System.out.println("Olá mundo"); // Forma tradicional
System.out.println("Minha altura é " + altura + "."); // Formatação simples
```

### printf() é uma formatação avançada, parecida com C.
```java
System.out.printf("Minha altura é %f.%n",altura); // %f indica float. %n indica pular linha.
```

O tabelamento também é possível, criando resultados como esses:

```java
System.out.printf("%-15s%-15s%-15s %n", "ID", "nome", "altura"); // Formatação avançada
System.out.printf("%-15d%-15s%-15.8f %n", variavelId, variavelNome, variavelAltura);
```
```bash
ID      nome      altura    
0       José      1.75000000
```

# Manipulação de String

### String Length

Para saber o tamanho da String, usamos o método **length()**.

```java
int totalChars = string_1.length();
System.out.printf("Caracteres: %d", totalChars);
```

### Capitalizar

```java
String titulo = "BeM viNdO";
System.out.println(titulo.toLowerCase()); // Tudo minúsculo
System.out.println(titulo.toUpperCase()); // Tudo maiúsculo
System.out.println(titulo.substring(0, 1).toUpperCase() + titulo.substring(1).toLowerCase()); // Primeira letra maiúscula apenas
```

### Índices e Slice

- Acesso a índices
```java
String texto = "Python s2";
System.out.println(texto.charAt(2)); // Imprime 't'. Equivalente a texto[2] no python ou C.
```

- Slicing
```java
String texto = "Python s2";

String novaString = texto.substring(2, 6); // Começa no 2 e termina no 6. Imprime "thon"
System.out.println(novaString);

novaString = texto.substring(0, 6);
System.out.println(novaString);

novaString = texto.substring(texto.length() - 9, texto.length() - 3); // Imprime "python"
System.out.println(novaString);
```

Perceba que no último caso, estou acessando índices como se fosse **texto[-9]** e **texto[-3]** no python, com índices negativos, posso ter acesso diferenciado começando a partir do último caractere até o primeiro.

# Casting

Existem algumas formas de fazer casting.

### Implícita

```java
int numInt = 10;
float numFloat = numInt; // Conversão implícita de int pra float.
double numDouble = numInt; // Conversão implícita de float pra double.
```

Conversão direta implícita. Não é recomendado fazer, dado que será mais difícil encontrar onde está essa conversão caso ocorram futuros bugs.

### Explícita

```java
int numInt = 10;
float numFloat = (float) numInt;
byte numByte = (byte) numInt;
```

Conversão direta explícita. O seu uso eventual não há problema, pois ficaria mais fácil de achar onde está a conversão futuramente.

### String para número (Parse)

```java
String str = "10";
int numInt = Integer.parseInt(str);
float numFloat = Float.parseFloat(str);
double numDouble = Double.parseDouble(str);
```

**Parse** trabalha apenas de string $\implies$ qualquer primitivo.

### Número para string (To)

```java
int numInt = 10;
String str1 = Integer.toString(numInt);

int numDouble = 10.5;
String str2 = Double.toString(numInt);
```

**To** trabalha de qualquer primitivo $\implies$ string.