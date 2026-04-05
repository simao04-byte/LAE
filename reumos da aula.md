# Aula 02 -- Introdução e Máquinas Virtuais Modernas

**23-02-2025 --- C.2.07**

## Resumo da Aula

-   Discussão sobre trabalho de grupo e utilização de assistentes de IA
-   Introdução às linguagens de programação compiladas vs interpretadas
-   Conceito e arquitetura da Java Virtual Machine (JVM)
-   Demonstração prática da compilação de Kotlin para bytecode
-   Diferenças entre linguagens imperativas e os seus objetivos

## Tópicos

### Organização do trabalho de grupo

-   Os estudantes podem utilizar quaisquer ferramentas de IA disponíveis
-   Todo o código entregue deve ser totalmente compreendido pelos
    estudantes
-   A primeira parte do trabalho consiste em definir os próprios
    requisitos do projeto
-   Estudantes que não fizeram LS podem propor trabalho alternativo
-   Utilização do GitHub Classroom para criação de repositórios

### Comparação de linguagens de programação

Linguagens mencionadas: - x86 Assembly - Java - JavaScript - CSS -
HTML - SQL - Kotlin

Razões para existirem várias linguagens: - Objetivos diferentes (SQL vs
Kotlin/Java) - Evolução tecnológica - Kotlin surgiu como evolução do
Java

### Linguagens compiladas vs interpretadas

#### Compiladas

-   Compilação ocorre antes da execução
-   Fase de compilação + fase de execução
-   Erros aparecem na compilação

#### Interpretadas

-   Tradução ocorre durante execução
-   Exemplo: JavaScript com Node.js
-   Erros aparecem em runtime
-   Maior portabilidade

### Java Virtual Machine (JVM)

Problema: L linguagens e A arquiteturas → L × A compiladores.

Solução: Uma máquina virtual comum.

Vantagens: - Um compilador por linguagem - Código portátil -
Implementação específica por arquitetura

### Compilação Kotlin

Comando:

kotlinc SampleApp.kt

Gera ficheiros `.class` (bytecode).

Regra: - Um `.class` por tipo

Tipos: - classes - interfaces - data classes - enums

### Arquiteturas suportadas

-   Linux x64 / ARM
-   Windows x64 / ARM
-   macOS (Apple Silicon)
-   Amazon Linux
-   Docker

### Distribuição Java

Unidade básica: `.class`

Aplicações grandes → centenas de ficheiros.

Solução: **JAR**

JAR = arquivo comprimido com múltiplos `.class`.

------------------------------------------------------------------------

# Aula 03 -- Componentes da JVM e Sistema de Tipos

**27-02-2025 --- C.2.07**

## Resumo

-   Dynamic class loading
-   Linking dinâmico vs estático
-   Introdução aos sistemas de tipos
-   Tipos primitivos vs não-primitivos
-   Ferramenta `javap`

### Dynamic Class Loading

-   Classes carregadas apenas quando necessárias
-   JVM carrega primeiro a classe principal
-   Outras classes carregadas durante execução
-   `ClassNotFoundException` ocorre na instanciação

### Linking Dinâmico

-   `.class` podem ser substituídos sem recompilar tudo
-   Compatível se assinatura de métodos não mudar

Verifier: - verifica assinaturas de métodos - garante que métodos
existem

Vantagens: - corrigir bugs sem recompilar tudo - substituir componentes

### Sistema de Tipos

Sistema de tipos = regras fundamentais da linguagem.

Define: - tipos suportados - operações permitidas - uso de memória

### Categorias de Tipos

#### Primitivos

-   `int`, `boolean`, etc.
-   pass-by-value
-   armazenamento otimizado

#### Não-primitivos

-   classes e objetos
-   pass-by-reference

### Ferramenta javap

Utilitário do JDK.

Funções: - ver estrutura de classes - mostrar métodos gerados - analisar
bytecode

### Métodos

**Static** - pertencem à classe

**Instance** - pertencem ao objeto - possuem `this`

### Memória

Pass-by-value: - cópia independente

Pass-by-reference: - várias variáveis podem referir o mesmo objeto

Garbage Collector gere memória automaticamente.

------------------------------------------------------------------------

# Aula 04 -- Kotlin e JVM Type Systems

**02-03-2025 --- C.2.07**

## Sistema de Tipos

Sistema de tipos = constituição da linguagem.

-   Kotlin tem sistema próprio
-   JVM tem sistema próprio
-   Java aproxima-se da JVM

Compilador traduz regras Kotlin → JVM.

### Diferenças

Kotlin: - suporta funções globais - possui properties

JVM/Java: - tudo dentro de classes - apenas fields e methods

### Properties

Kotlin:

`val` → getter\
`var` → getter + setter

Properties privadas: - apenas field

### Java equivalente

-   fields privados
-   getters/setters
-   construtor manual

### Data Classes

Geram automaticamente:

-   `toString()`
-   `equals()`
-   `hashCode()`
-   `copy()`
-   `componentN()`

Usadas para objetos que representam dados.

### Igualdade

`===` → mesma referência\
`==` → mesmo conteúdo

------------------------------------------------------------------------

# Aula 05 -- OOP, Herança e Bytecode

**06-03-2025 --- C.2.10**

## Bytecode JVM

Modelo baseado em stack (LIFO).

`load` → coloca valor na stack\
`store` → remove da stack

Tabela de variáveis contém: - parâmetros - variáveis locais

### Herança

Objetivo: - reutilização de código

Classe derivada herda membros da classe base.

Regra:

Derived **is-a** Base.

### Tipos

Static type: - definido no código

Dynamic type: - tipo real do objeto em runtime

Dynamic type deve ser compatível com static type.

### Casting

Upcasting: - seguro

Downcasting: - verificado em runtime

Instrução JVM:

`checkcast`

Pode gerar:

`ClassCastException`

### Boxing

Tipos primitivos: - `Int` - `Double`

Nullable:

`Int?` → `Integer`

Boxing: int → Integer

Unboxing: Integer → int

------------------------------------------------------------------------

# Aula 06 -- Boxing, Unboxing e Generics

**09-03-2025 --- C.2.07**

## Boxing e Unboxing

Nullable types requerem boxing.

Exemplo:

`Int?` → `Integer`

Boxing usa:

`Integer.valueOf()`

Unboxing usa:

`intValue()`

### Performance

Boxing: - cria objetos

Unboxing: - chamada de métodos

Pode causar overhead.

### Casting JVM

Upcasting: - seguro

Downcasting: - usa `checkcast`

### Bytecode comum

-   `Integer.valueOf()`
-   `intValue()`
-   `checkcast`
-   `instanceof`

### Generics

Objetivo: - evitar duplicação de código - permitir tipos parametrizados

Problema:

JVM não suporta generics diretamente.

### Type Erasure

Durante compilação:

`List<T>` → `List<Object>`

Compilador adiciona casts automáticos.

### Consequências

Não é possível saber tipos genéricos em runtime.

Pode causar `ClassCastException`.

### Recomendações

-   evitar casts inseguros
-   usar `is` antes de `as`
-   evitar raw generics
