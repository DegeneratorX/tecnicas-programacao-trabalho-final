# # Java Avançado

Aqui abordarei alguns paradigmas avançados da linguagem Java, principalmente relacionados a POO.

# Instanciação

Instanciar uma classe é criar na heap um objeto que pertence aquele tipo.

```java
class Pessoa{...}

Pessoa p = new Pessoa();
```

# Tipos de Classes

Existem 4 formas de definir classes

- class: pode ser vista por outros arquivos no mesmo package. Tipo mais padrão.
- public class: classe "principal" do arquivo. Precisa ter o mesmo nome do arquivo.
- abstract class: classe abstrata que não pode ser instanciada, e obrigatoriamente precisa ser herdada.
- final class: classe que não pode ser herdada.

# Modificadores de acesso (Encapsulamento)

Existem 3 principais tipos de encapsulamento: **public**, **protected** e **private**. Funcionam de forma semelhante ao python. No python, o acesso direto a membros privados é permitido, porém no Java ocasionará erros.

- membro public: acesso irrestrito
- membro protected: acesso via subclasses ou outras classes no mesmo package
- membro private: acesso somente dentro da própria classe que o membro foi criado.

Os modificadores de acesso funcionam tanto em atributos de classe quanto em métodos.

# Herança, Polimorfismo, Construtor, Get/Set, Abstração

### Herança

Usa a keyword **extends Classe**.

```java
public class A {
    public void foo() {}
}

class B extends A {
    public void foo() {}
}
```

Para herança múltipla, basta colocar **extends A, B** para uma classe C, por exemplo.

### Polimorfismo

Polimorfismo é o princípio que permite que classes derivadas de uma mesma superclasse tenham métodos iguais (de mesma assinatura),
mas comportamentos diferentes. Polimorfismo funciona da mesma forma do Python, porém precisa da anotação @Override para sinalizar a sobreposição.

```java
class Animal {
   public void falar() {}
}

class Gato extends Animal {
   @Override
   public void falar() {
      System.out.println("Meow");
   }
}

class Cachorro extends Animal {
   @Override
   public void falar() {
      System.out.println("Au au!");
   }
}
```

Existe também o polimorfismo de sobrecarga de métodos, que é quando vários métodos com mesmo nome na mesma classe recebem parâmetros diferentes.

```java
class Calculator {
   public int add(int a, int b) {
      return a + b;
   }
   public double add(double a, double b) {
      return a + b;
   }
   public String add(String a, String b) {
      return a + b;
   }
}
```

### Construtor

O construtor da classe é idêntico ao C++. Sempre deve ser público!

```java
public class Pessoa {
    private String nome;
    private int idade;

    // Construtor.
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }
}
```

O **this** é um ponteiro para a própria instância da classe. Funciona de forma idêntica ao C++ e ao **self** do python. A diferença pro python é que não precisa passar como parâmetro de todo método de classe.

### Get/Set

Funcionam da mesma forma que outras linguagens.

```java
class Pessoa{
    private String nome;

    public Pessoa(String nome, int idade) {this.nome = nome;}

    public String getNome(){return this.nome;}
    public void setNome(String nome){this.nome = nome;}
}
```

### Abstração

Classes com a keyword **abstract** precisam ser herdadas e não podem ser instanciadas. Como o nome já diz, são abstratas. Ou seja, uma classe abstrata de exemplo seria um Banco. E classes que herdam do Banco são BancoCorrente e BancoPoupança.

Já os métodos **abstract** precisam ser herdados e sobrepostos com polimorfismo.

```java
public abstract class MyAbstractClass { // Precisa ser herdado, se não dá erro.
    public abstract void myAbstractMethod(); // Precisa ser sobreposto, se não dá erro.
}
```

# Interface

Interfaces são convenções utilizadas pelos programadores para definir o que uma Classe implementa.

```java
interface Shape {
    double getArea();
}

// Implement the interface in a class
class Retangulo implements Shape {
    private double largura;
    private double altura;
    
    public Rectangle(double largura, double altura) {
        this.largura = largura;
        this.altura = altura;
    }
    
    public double getArea() {
        return this.largura*this.altura;
    }
}
```

Ou seja, se a classe implementa Shape, então ela precisa usar o método getArea(), caso contrário dará erro. É possível usar 2 ou mais interfaces implementadas separadas por vírgulas, como uma herança múltipla.

O uso de interfaces pode evitar problemas como o do Diamante em heranças múltiplas.

# Associação, Agregação, Composição e Sobreposição

São filosofias em POO que cria dependência entre as classes.

### Associação

O carro pode existir sem o motorista e o motorista pode existir sem o carro.

```java
// Association example
public class Carro {
   private Motorista motorista;
   
   (...)
}

public class Motorista {
   private String nome;
   
   (...)
}
```

### Agregação

O carro precisa dos pneus, mas os pneus não precisam do carro.

```java
public class Carro {
   private List<Pneu> pneus;
   
   (...)
}

public class Pneu {
   private String marca;
   
   (...)
}
```

### Composição

O carro precisa do motor e o motor precisa do carro.

```java
public class Carro {
   private Motor motor;
   
   (...)
}

public class Motor {
   private String tipo;
   
   (...)
}
```

# Final

A keyword **final** do Java é idêntica a keyword do C++: previne herança e sobreposição de métodos.

```java
public class A {
    public void foo() {}
}

final class B extends A { // Essa classe não pode ser herdada
    public final void bar() {}  // Esse método não pode ser sobreposto
}

// Dois problemas aqui: herança de classe (um erro) e sobreposição de método (outro erro).
class C extends B { 
    public void bar() {}
}
```

Porém, no Java existe uma funcionalidade extra muito boa. Sabe-se que no Java não existe a keyword **const** do C++. E por isso a linguagem adotou o próprio **final** como uma função de const, para sinalizar que uma variável é imutável.

```java
public class Main {
    public static void main(String[] args) {
        final int x = 10;  // Variável const
        x = 20;  // Erro de compilação
    }
}
```

# Generics (Templates)

Funcionam de forma idêntica aos templates do C++. São uma ferramenta poderosíssima que evita a criação desnecessária de vários métodos apenas para mudar o tipo dele. O generics cria métodos em tempo de execução que recebem em tempo real diversos tipos de dados, e trabalha em cima deles.

```java
public class Amostra<T>{
    private T dados;
    public void setDados(T novoDado){
        this.dados = novoDado;
    }
    public T getDados(){
        return this.dados;
    }
}
```

A maior parte das classes que importamos para o java, como ArrayList, usam generics.

```java
ArrayList<String> lista = new ArrayList<>(); // No lugar da String, é um generics que recebe qualquer coisa.
```

Se não fosse o generics, o programador teria de criar diversos métodos para diversas tipos abstratos de dados que poderiam ser passados via parâmetro.

Por convenção, se usa muito a letra T, igual C++.

# Annotations (Decoradores)

O uso de **annotations** em Java é similar aos decoradores em python, mas tem algumas diferenças, como por exemplo, essa:

```java
class Animal {
    public void emitirSom() {
        System.out.println("Som genérico");
    }
}

class Cachorro extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("Au au!");
    }
}
```

Aqui o uso é obrigatório para definir sobreposições em heranças, caso contrário acarretará erro em tempo de compilação.

Também existe uma mão na roda para criar métodos automáricos de Gets e Sets para cada atributo da classe.

```java
import lombok.Getter;
import lombok.Setter;

public class Pessoa {
    @Getter @Setter private String name;
    @Getter @Setter private int age;
}
```

Aqui estou usando essas annotations para gerar métodos de forma automática Get e Set para cada atributo da classe Pessoa.