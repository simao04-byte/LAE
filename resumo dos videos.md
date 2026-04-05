# Resumo das Aulas -- JVM, Kotlin e Sistema de Tipos

## 1. Execução de um Programa na JVM

Quando executas:

``` bash
java App
```

Acontece:

1.  O programa `java` inicia a **JVM (Java Virtual Machine)**
2.  Passas o **nome da classe inicial**
3.  A JVM procura o método:

``` java
public static void main(String[] args)
```

Se não existir → erro.

------------------------------------------------------------------------

## 2. Ficheiros `.class`

Quando compilas:

``` bash
javac App.java
```

é criado:

    App.class

Um `.class` contém:

-   **Metadados do tipo**
-   **Bytecode executável da JVM**

Metadados incluem:

-   nome da classe
-   métodos
-   campos
-   assinatura de métodos
-   herança

Ferramenta para visualizar:

``` bash
javap -c App.class
```

------------------------------------------------------------------------

## 3. Unidade mínima da JVM

A **unidade mínima da JVM é o tipo**.

Cada ficheiro `.class` define **um tipo**.

Exemplos:

-   classe
-   interface
-   enum

------------------------------------------------------------------------

## 4. Class Loading

A JVM **não carrega todas as classes no início**.

Fluxo:

1.  Carrega a classe inicial.
2.  Carrega outras classes **apenas quando necessárias**.

Exemplo:

``` java
new X()
```

Se `X.class` não existir → erro.

Consequência:

Erros podem aparecer **apenas quando um determinado caminho do código é
executado**.

------------------------------------------------------------------------

## 5. Componentes da JVM

### ClassLoader

Responsável por carregar classes para memória.

    .class → memória

------------------------------------------------------------------------

### Verifier

Verifica:

-   se métodos existem
-   se assinaturas são compatíveis

------------------------------------------------------------------------

### JIT Compiler

Significa:

    Just‑In‑Time Compiler

Função:

    Bytecode JVM → Código nativo do CPU

Melhora performance.

------------------------------------------------------------------------

## 6. Dynamic Linking

Java usa **ligação dinâmica**.

Significa:

As ligações entre classes são verificadas **em runtime**.

Se a assinatura de um método não mudar, podes recompilar apenas uma
classe.

------------------------------------------------------------------------

## 7. Sistema de Tipos

O sistema de tipos é a **Constituição da linguagem**.

Define:

-   tipos existentes
-   operações permitidas
-   regras de compatibilidade

------------------------------------------------------------------------

## 8. Tipos Primitivos vs Não Primitivos

### Primitivos

Exemplos:

    int
    float
    boolean
    char

Características:

-   armazenam **valor diretamente**
-   tratados **por valor**

------------------------------------------------------------------------

### Não primitivos

Exemplos:

    classes
    listas
    objetos

Características:

-   armazenam **referência**
-   tratados **por referência**

------------------------------------------------------------------------

## 9. Classe vs Objeto

### Classe

Modelo que define:

-   propriedades
-   métodos

------------------------------------------------------------------------

### Objeto

Instância concreta da classe.

Exemplo:

``` kotlin
class Rectangle
```

Objetos:

    Rectangle r1
    Rectangle r2

Cada um com valores diferentes.

------------------------------------------------------------------------

## 10. Kotlin vs Java vs JVM

  Sistema   Características
  --------- ------------------------
  JVM       simples
  Java      muito parecido com JVM
  Kotlin    mais abstrato

O compilador Kotlin traduz conceitos Kotlin → JVM.

------------------------------------------------------------------------

## 11. Propriedades Kotlin

Kotlin:

``` kotlin
class Rectangle(val height, var width)
```

Propriedades.

Na JVM isto vira:

-   campo privado
-   getter
-   setter

------------------------------------------------------------------------

## 12. Data Classes

``` kotlin
data class Rectangle(...)
```

O compilador gera automaticamente:

-   `toString()`
-   `equals()`
-   `hashCode()`
-   `copy()`
-   `componentN()`

------------------------------------------------------------------------

## 13. Bytecode da JVM

A JVM executa **bytecode**.

Exemplo de instruções:

    aload
    astore
    checkcast
    invoke

------------------------------------------------------------------------

## 14. Máquina de Stack

A JVM usa uma **stack machine**.

Operações principais:

    load  → coloca valor na stack
    store → retira valor da stack

------------------------------------------------------------------------

## 15. Herança

Exemplo:

``` kotlin
class A
class B : A()
```

B herda tudo de A.

Principal objetivo:

**Reutilização de código**.

------------------------------------------------------------------------

## 16. Tipo Estático vs Tipo Dinâmico

Variável:

    A a

Tipo estático:

    A

Objeto real pode ser:

    A
    B
    C

desde que herdem de A.

------------------------------------------------------------------------

## 17. Casting

### Upcast

``` java
A a = new B()
```

Sempre seguro.

------------------------------------------------------------------------

### Downcast

``` java
B b = (B) a
```

Pode falhar.

Erro possível:

    ClassCastException

------------------------------------------------------------------------

## 18. Instrução `checkcast`

A JVM usa a instrução:

    checkcast

Função:

Verificar em runtime se o objeto é compatível com o tipo.

------------------------------------------------------------------------

## 19. Boxing e Unboxing

Conversão entre:

    primitivo
    objeto

### Boxing

    int → Integer

### Unboxing

    Integer → int

------------------------------------------------------------------------

## 20. Ideia Central da Disciplina

Fluxo geral:

    Linguagem alto nível (Java/Kotlin)
            ↓
          Compilador
            ↓
        Bytecode JVM
            ↓
            JVM
            ↓
     Código nativo CPU

A JVM é o **runtime real**.
