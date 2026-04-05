# Lesson 02 - Introdução e Máquinas Virtuais Modernas

23-02-2025 - C.2.07

## Resumo da Aula:

-   Discussão sobre trabalho de grupo e utilização de assistentes de IA
-   Introdução às linguagens de programação compiladas vs interpretadas
-   Conceito e arquitetura da Java Virtual Machine (JVM)
-   Demonstração prática da compilação de Kotlin para bytecode
-   Diferenças entre linguagens imperativas e os seus objetivos

## Tópicos:

### Organização do trabalho de grupo

-   Os estudantes podem usar quaisquer ferramentas de IA disponíveis
-   Todo o código entregue deve ser totalmente compreendido pelos
    estudantes
-   A primeira parte do trabalho será definir os próprios requisitos do
    projeto
-   Estudantes que não fizeram LS podem propor trabalho alternativo
-   Utilização do GitHub Classroom para criação de repositórios

### Comparação de linguagens de programação

Linguagens mencionadas pelos estudantes: - x86 Assembly - Java -
JavaScript - CSS - HTML - SQL - Kotlin

Razões para a existência de várias linguagens: - Objetivos diferentes
(SQL vs Kotlin/Java) - Evolução tecnológica e melhorias - Kotlin surgiu
como evolução do Java, simplificando o código

### Linguagens compiladas vs interpretadas

#### Linguagens compiladas:

-   A compilação ocorre antes da execução
-   Duas fases distintas: programação/compilação e execução
-   Erros detetados durante a fase de compilação

#### Linguagens interpretadas (script):

-   Tradução para código nativo durante a execução
-   Exemplo: JavaScript executado pelo Node.js
-   Erros apenas aparecem em runtime
-   Maior portabilidade entre plataformas

### Conceito de Java Virtual Machine

Problema de múltiplas arquiteturas: Com L linguagens e A arquiteturas,
seriam necessários L × A compiladores.

Solução JVM: Uma máquina virtual comum.

Vantagens da JVM: - Apenas um compilador por linguagem direcionado para
a JVM - Código compilado portátil entre arquiteturas - Implementação da
JVM específica por arquitetura

Comparação com a plataforma .NET (CLR) da Microsoft.

### Demonstração prática - Compilação Kotlin

Comando de compilação: kotlinc SampleApp.kt

Geração de ficheiros .class (bytecode)

Regra: um ficheiro .class por cada tipo definido

Tipos incluem: - classes - interfaces - data classes - enums

Diferenças entre sistemas de tipos Kotlin e JVM: A JVM apenas suporta: -
classes - interfaces - enumerações

O compilador Kotlin traduz os conceitos para a JVM.

A função main é traduzida para um método public static.

### Arquiteturas atualmente suportadas

-   Linux x64, ARM
-   Windows x64, ARM
-   macOS (processadores Apple M - ARM personalizado)
-   Amazon Linux
-   Docker

### Distribuição de aplicações Java

Unidade básica: ficheiros .class

Aplicações com centenas de tipos = centenas de ficheiros

Solução: empacotar em ficheiros JAR

JAR = arquivo comprimido que contém múltiplos ficheiros .class

### Recursos:

-   Lab1
-   Código da aula no Github

# Lesson 03 - Componentes da JVM e Sistema de Tipos

27-02-2025 - C.2.07

## Resumo da aula:

-   Carregamento dinâmico de classes na JVM através de exercícios
    práticos com ficheiros .class
-   Demonstração das diferenças entre ligação estática e dinâmica em
    Java
-   Introdução aos sistemas de tipos: definições fundamentais e
    categorização de tipos primitivos vs não‑primitivos
-   Exploração dos mecanismos pass-by-value vs pass-by-reference
-   Utilização da ferramenta javap para analisar metadados em ficheiros
    .class

## Tópicos:

### Dynamic Class Loading

Comportamento de carregamento de classes da JVM: - As classes são
carregadas apenas quando necessárias (lazy loading) - Nenhum erro ocorre
quando a classe não é instanciada - ClassNotFoundException apenas ocorre
quando se tenta instanciar

Funcionalidade do Class Loader: - Carrega classes quando necessário
durante a execução - A JVM inicialmente carrega apenas a classe
principal especificada - Outras classes são carregadas conforme a
execução do programa necessita

### Dynamic vs Static Linking

Compatibilidade binária em Java: - Ficheiros .class podem ser
substituídos sem recompilar classes dependentes - Compatibilidade
mantida quando as assinaturas dos métodos não mudam

Função do componente Verifier: - Valida assinaturas de métodos em
runtime - Garante que métodos chamados existem e têm assinaturas
corretas

Vantagens do linking dinâmico: - Correção de bugs sem recompilar todas
as classes dependentes - Substituição flexível de componentes sem
quebrar código existente

### Fundamentos do Sistema de Tipos

Definição: A "constituição" de uma linguagem de programação.

Conjunto de regras fundamentais que governam o comportamento da
linguagem.

Especifica: - Tipos suportados - Regras de utilização desses tipos

Objetivos dos tipos: - Restringir operações permitidas sobre valores -
Definir alocação de memória - Controlar compatibilidade entre operações

### Categorias de Tipos

Tipos primitivos: - Integrados na linguagem (int, boolean, etc.) -
Semântica pass-by-value (valor copiado durante atribuição) - Instruções
especiais e armazenamento otimizado

Tipos não-primitivos: - Tipos definidos pelo utilizador ou bibliotecas -
Semântica pass-by-reference (referência copiada) - Implementados
internamente usando tipos primitivos

### Ferramenta javap

Utilitário do JDK para análise de ficheiros .class.

Disponível apenas no JDK, não no JRE.

Funcionalidades: - Mostra estrutura da classe em formato legível -
Revela informação de tipos e métodos gerados pelo compilador - Mostra
metadados de bytecode para análise

### Diferenças de Sistemas de Tipos

Kotlin vs JVM:

Kotlin suporta funções globais; a JVM exige que tudo esteja dentro de
classes.

O compilador Kotlin gera classes wrapper: FileName + Kt

### Métodos estáticos vs métodos de instância

Métodos estáticos: - Pertencem à classe - Invocados através do nome da
classe

Métodos de instância: - Pertencem aos objetos - Requerem instância para
invocação

Parâmetro implícito "this" disponível em métodos de instância.

### Gestão de Memória

Pass-by-value: - Cada variável contém cópia independente do valor

Pass-by-reference: - Variáveis contêm referências para objetos em
memória - Várias variáveis podem referenciar o mesmo objeto

Garbage Collector gere automaticamente a memória.

### Recursos:

-   Código da aula no Github
-   Gravação da aula

# Lesson 04 - Sistemas de Tipos Kotlin e JVM

02-03-2025 - C.2.07

## Resumo da Aula:

-   Introdução aos sistemas de tipos em linguagens de programação
-   Comparação entre sistemas de tipos Kotlin e Java/JVM
-   Mecanismos de tradução de Kotlin para bytecode JVM
-   Conceito de properties vs fields e métodos
-   Data classes e código gerado automaticamente
-   Demonstração prática de compilação e análise de bytecode

## Tópicos:

### Visão Geral dos Sistemas de Tipos

Sistema de tipos definido como regras fundamentais de uma linguagem.

Comparado com uma constituição que define princípios fundamentais.

Cada linguagem possui o seu próprio sistema de tipos.

Kotlin tem o seu sistema de tipos.\
JVM tem o seu sistema de tipos.\
Java tem um sistema muito semelhante ao da JVM.

O código precisa respeitar as regras da JVM para poder executar.

Os compiladores fazem a tradução entre os sistemas de tipos.

### Diferenças entre Sistemas de Tipos Kotlin e Java

Tipos primitivos em Kotlin vs JVM.

Int é primitivo em Kotlin mas não na JVM.

Diferenças no tratamento de Strings (imutáveis).

### Taxonomia de tipos em Kotlin

-   Classes (regular, data, abstract, final)
-   Interfaces
-   Objects
-   Enum classes

### Limitações do sistema de tipos Java

Java apenas suporta classes com fields e métodos.

Não existe conceito nativo de property.

Sintaxe mais verbosa.

### Properties vs Fields e Métodos

Properties em Kotlin: - Combinação de parâmetro e propriedade usando
val/var - O compilador gera automaticamente getters e setters

Properties privadas apenas geram fields.

### Equivalente em Java

-   Fields privados
-   Métodos getter/setter públicos
-   Atribuição manual no construtor

### Demonstração de compilação

Classe Rectangle em Kotlin gera o mesmo bytecode que em Java.

Grande redução de código.

### Data Classes

Código gerado automaticamente: - component1, component2 - copy -
toString - equals - hashCode

### Diferença com classes normais

Classes normais mostram referência de memória em toString.

Data classes mostram valores das propriedades.

### Quando usar data classes

Para objetos cujo objetivo principal é guardar dados.

### Identidade vs Igualdade

=== mesma referência\
== mesmo conteúdo

### Recursos:

-   Lab2
-   Código da aula no Github
-   Gravação da aula

# Lesson 05 - OOP, Herança e Bytecode JVM

06-03-2025 - C.2.10

## Resumo da Aula:

-   Fundamentos das instruções de bytecode da JVM e modelo de execução
    baseado em stack
-   Mecanismos de herança em programação orientada a objetos
-   Diferenças entre verificação de tipos em compilação e em runtime
-   Operações de casting (upcasting vs downcasting)
-   Introdução aos conceitos de boxing/unboxing

## Tópicos:

### Bytecode JVM e Arquitetura Baseada em Stack

As instruções da JVM utilizam um modelo de execução baseado em stack.

A stack segue o princípio LIFO (Last In, First Out).

Instruções com prefixo "load" colocam valores na stack.

Instruções com prefixo "store" retiram valores da stack.

Parâmetros de função são identificados por posição.

Primeiro parâmetro posição 0, segundo posição 1.

A tabela de variáveis locais contém parâmetros e variáveis locais.

### Conceitos de Herança em OOP

Classes representam conceitos do mundo real.

Objetivo principal da herança: - reutilização de código - evitar
duplicação

Classe derivada herda membros da classe base.

Pode adicionar funcionalidades.

### Compatibilidade de tipos

Instâncias da classe derivada podem substituir instâncias da classe
base.

Derived objects "são" base objects.

### Sistema de tipos estático vs dinâmico

Tipo estático: - tipo declarado da variável

Tipo dinâmico: - tipo real do objeto em runtime

O tipo dinâmico deve ser compatível com o tipo estático.

### Casting e Segurança

Upcasting: - sempre seguro

Downcasting: - potencialmente inseguro - requer verificação em runtime

A JVM usa a instrução checkcast.

Se falhar lança exceção.

Kotlin usa operador as para casting verificado.

### Tipos Primitivos e Boxing

Tipos primitivos como Int e Double.

Tipos primitivos nullable requerem boxing.

Int? torna-se objeto wrapper.

Boxing = converter valor primitivo para objeto.

Unboxing = extrair valor primitivo do objeto.

Unboxing de null gera exceção.

### Recursos:

-   Código da aula no Github
-   Gravação parte 1
-   Gravação parte 2

# Lesson 06 - Sistema de Tipos, Boxing, Unboxing e Generics

09-03-2025 - C.2.07

## Resumo da Aula:

-   Operações de boxing e unboxing entre tipos primitivos e tipos
    referência
-   Casting de tipos e instruções JVM associadas
-   Type erasure em generics Java
-   Compilação Kotlin para bytecode com conversões automáticas

## Tópicos:

### Boxing e Unboxing

Tipos nullable em Kotlin requerem boxing.

Exemplo: Int? não pode ser representado como int primitivo.

A JVM usa classe Integer como wrapper.

Boxing cria objeto usando Integer.valueOf().

Unboxing usa métodos como intValue() e doubleValue().

Gerado automaticamente pelo compilador Kotlin.

### Impacto de performance

Boxing requer alocação de objeto.

Unboxing requer chamadas de método.

Pode causar overhead em loops intensivos.

### Casting e Instruções JVM

Upcasting: - seguro

Downcasting: - gera instrução checkcast

Pode lançar ClassCastException.

### Análise de Bytecode

Instruções comuns: - invokestatic Integer.valueOf() - invokevirtual
intValue() - checkcast - instanceof

Tabela de variáveis mostra tipos primitivos e tipos referência.

### Generics e Type Erasure

Objetivo dos generics: - evitar duplicação de código - permitir tipos
parametrizados

Problema: A JVM não suporta generics nativamente.

Durante compilação ocorre type erasure.

Tipos genéricos tornam-se Object.

O compilador gera casts automaticamente.

### Implicações em runtime

Não é possível saber parâmetros genéricos em runtime.

Pode causar ClassCastException.

### Recomendações

-   evitar casts inseguros
-   usar is antes de as
-   evitar generics raw
-   compreender custos de boxing/unboxing
