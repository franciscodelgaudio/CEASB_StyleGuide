# C# at CEASB Style Guide

## Diretrizes de Formatação

### Regras de Nomenclatura

#### =Código

*   =Nomes de classes, métodos, enumerações, campos públicos, propriedades públicas, namespaces: `PascalCase`.
*   =Nomes de variáveis locais, parâmetros: `camelCase`.
*   =Nomes de campos e propriedades privadas, protegidas, internas e protegidas internas: `_camelCase`.
*   =Para a escrita de palavras, qualquer coisa sem espaços internos, incluindo siglas, é considerada uma "palavra". Por exemplo, `MyRpc` em vez de `MyRPC`.
*   =Escolha nomes de identificador facilmente legíveis.
*   =Favoreça a legibilidade em vez da brevidade.
*   =Não use sublinhados, hifens ou outros caracteres não alfanuméricos.
*   =Não use abreviações ou contrações como parte de nomes de identificador.

#### =Arquivos

*   =Nomes de arquivos e diretórios são em `PascalCase`, por exemplo, `MyFile.cs`.
*   =Onde for possível, o nome do arquivo deve ser o mesmo que o nome da classe principal no arquivo, por exemplo, `MyClass.cs`.
*   =Em geral, prefira uma classe principal por arquivo.

#### =Classes, Structs, Interfaces e Genéricos

*   =Nomes de interfaces começam com `I`, por exemplo, `IInterface`.
*   =Nomeie classes e structs com substantivos ou frases nominais, usando PascalCasing.
*   =Nomeie interfaces com frases adjetivas ou, ocasionalmente, com substantivos ou frases nominais.
*   =Considere encerrar o nome de classes derivadas com o nome da classe base.

#### =Métodos

*   =Nomeie os métodos usando verbos ou frases verbais.

#### =Propriedades

*   =Nomeie as propriedades usando um substantivo, uma frase nominal ou um adjetivo.
*   =Não tenha propriedades que correspondam ao nome dos métodos "Get".
```c#
    // Incorreto
    public string TextWriter { get {...} set {...} }
    public string GetTextWriter(int value) { ... }
```
*   =Nomeie as propriedades de coleção com uma frase no plural que descreva os itens na coleção em vez de usar uma frase no singular seguida por "List" ou "Collection".
```c#
    // Incorreto
    public List<string> NameList { get; set; }
    // Correto
    public List<string> Names { get; set; }
```
*   =Nomeie as propriedades boolianas com uma frase afirmativa (CanSeek em vez de CantSeek). Opcionalmente, você também pode prefixar as propriedades boolianas com "Is", "Can" ou "Has", mas somente quando isso adicionar valor.
*   =Considere nomear uma propriedade com o mesmo nome de seu tipo.
```c#
    public Color Color { get; set; }
```

#### =Eventos

*   =Nomeie os eventos com um verbo ou uma frase verbal.
*   =Nomeie os eventos com um conceito de antes e depois, usando os tempos verbais presente e pretérito.
*   =Nomeie os manipuladores de eventos (delegados usados como tipos de eventos) com o sufixo "EventHandler".
*   =Nomeie as classes de argumento de evento com o sufixo "EventArgs".
```c#
    public ClosingEventArgs() => {};
    public ClosedEventArgs() => {};

    public delegate void ClosingEventHandler(object sender, ClosingEventArgs e);
    public delegate void ClosedEventHandler(object sender, ClosedEventArgs e);
    
    public event ClosingEventHandler Closing;
    public event ClosedEventHandler Closed;
```

#### =Genéricos e Enumerações

*   =Nomeie parâmetros de tipo genérico com nomes descritivos, a menos que um nome de uma única letra seja autoexplicativo e um nome descritivo não agregue valor.
*   =Considere usar T como o nome do parâmetro de tipo em tipos com parâmetro de tipo de uma letra. Por exemplo, em uma classe genérica `List<T>`, `T` representa o tipo dos elementos na lista.
*   =Use nomes de prefixo descritivos de parâmetro de tipo com T. Por exemplo, `TKey` e `TValue` em um dicionário genérico `Dictionary<TKey, TValue>`.
*   =Considere indicar as restrições colocadas em um parâmetro de tipo no nome do parâmetro.
*   =Use um nome de tipo singular para uma enumeração.
*   =Não use um sufixo "Enum" em nomes de tipo enumerado.

### =Organização

*   =Modificadores ocorrem na seguinte ordem: `public protected internal private
    new abstract virtual override sealed static readonly extern unsafe volatile
    async`.
*   =Ordem dos membros da classe:
    *   =Agrupe os membros da classe na seguinte ordem:
        *   Classes aninhadas, enums, delegates e eventos.
        *   Campos static, cons e readonly.
        *   Campos e propriedades.
        *   Construtores e finalizadores.
        *   Métodos.
    *   =Dentro de cada grupo, os elementos devem estar na seguinte ordem:
        *   Public.
        *   Internal.
        *   Protected internal.
        *   Protected.
        *   Private.
    *   =Onde for possível, agrupe as implementações de interfaces juntas.

### =Regras de Espaçamento

*   =Use o estilo "Allman" para chaves: abra e feche sua própria nova linha. As chaves se alinham com o nível de recuo atual.
*   =Limite de colunas: 80.
*   =Chaves usadas mesmo quando opcionais.
*   =Sem espaço após `if`/`for`/`while`, etc., e após vírgulas.
*   =Nenhum espaço após um parêntese de abertura ou antes de um parêntese de fechamento.
*   =As quebras de linha devem ocorrer após os operadores lógicos, se necessário.

## Diretrizes de Tipo

### =Constantes

*   =Variáveis e campos que podem ser const devem sempre ser const.
*   =Se const não for possível, readonly pode ser uma alternativa adequada.
*   =Prefira constantes nomeadas a números mágicos.

### =Expressões Condicionais
*   =Prefira a combinação de várias condições relacionadas em um único `if` quando isso melhora a legibilidade.
```c#
    if (condicao1)
    {
        if (condicao2)
        { ... }
    }
    
    // Combinação de condições
    if (condicao1 && condicao2)
    { ... }
```

### Classe vs Struct

*   =Considere definir um struct em vez de uma classe se as instâncias do tipo forem pequenas e normalmente de curta duração ou se forem comumente incorporadas em outros objetos.
*   =Não forneça um construtor sem parâmetros para um struct.
*   =Não defina tipos mutáveis de valor.
*   =Evite definir um struct, a menos que o tipo tenha todas as características a seguir:
    * =Representa logicamente um único valor, semelhante aos tipos primitivos (int, double etc.).
    * =Tem um tamanho de instância inferior a 16 bytes.
    * =É imutável.
    * =Não precisará ser encaixotado com frequência.
    
```c#
    //Point é pequeno, usado em operações rápidas frequentemente e tem apenas um tipo.
    public struct Point
    {
        public int X { get; }
        public int Y { get; }

        public Point(int x, int y)
        {
            X = x;
            Y = y;
        }
    }    
```
 
### Interface

*   Defina uma interface se você precisar que alguma API comum tenha suporte de um conjunto de tipos que incluem tipos de valor.
*   Considere definir uma interface se você precisar dar suporte à sua funcionalidade em tipos que já herdam de algum outro tipo.
*   Evite o uso de interfaces de marcador (interfaces sem membros).
*   Se você precisar marcar uma classe como tendo uma característica específica (marcador), no geral, use um atributo personalizado em vez de uma interface.
*   Forneça pelo menos um tipo que é uma implementação de uma interface.
*   Forneça pelo menos uma API que consome cada interface que você define (um método que usa a interface como um parâmetro ou uma propriedade tipada como a interface).
*   Não adicione membros a uma interface que tenha sido enviada anteriormente.

### Enumeração

*   Use uma enumeração para parâmetros, propriedades e valores retornados fortemente tipados que representam conjuntos de valores.
*   Prefira usar uma enumeração, em vez de constantes estáticas.
*   Não use uma enumeração para conjuntos abertos (como a versão do sistema operacional, nomes de amigos etc.).
*   Não forneça valores de enumeração reservados destinados a uso futuro.
*   Evite expor publicamente enumerações com apenas um valor.
*   Não inclua valores sentinelas em enumerações.
*   Forneça um valor de zero em enumerações simples.

### Tipos Aninhados

*   Use tipos aninhados quando a relação entre o tipo aninhado e seu tipo externo for tal que a semântica de acessibilidade de membros seja desejável.
*   Não use tipos aninhados públicos como um constructo de agrupamento lógico; use namespaces para isso.
*   Evite tipos aninhados expostos publicamente. A única exceção a isso é se variáveis do tipo aninhado precisarem ser declaradas apenas em cenários raros, como subclasse ou outros cenários avançados de personalização.
*   Não use tipos aninhados se o tipo provavelmente for referenciado fora do tipo que o contém.
*   Não use tipos aninhados se eles precisarem ser instanciados pelo código do cliente. Se um tipo tiver um construtor público, ele provavelmente não deve ser aninhado.
*   Não defina um tipo aninhado como membro de uma interface. Há muitas linguagens que não dão suporte a esse constructo.

### ref e out

*   Use out para retornos que não são também entradas.
*   Coloque os parâmetros out após todos os outros parâmetros na definição do método.
*   ref deve ser usado raramente, quando é necessário modificar uma entrada.
*   Não use ref como uma otimização para passar structs.
*   Não use ref para passar um contêiner modificável para um método. ref só é necessário quando o contêiner fornecido precisa ser substituído por uma instância de contêiner completamente diferente.

### Array vs List

*   Em geral, prefira `List<>` em vez de arrays para variáveis públicas, propriedades e tipos de retorno.
*   Prefira `List<>` quando o tamanho do contêiner pode mudar.
*   Prefira arrays quando o tamanho do contêiner é fixo e conhecido no momento da construção.
*   Prefira arrays para arrays multidimensionais.
*   Nota:
    * Arrays e `List<>` representam contêineres lineares e contíguos.
    * Semelhante aos arrays em C++ vs  `std::vector`, arrays têm capacidade fixa, enquanto `List<>` pode ser expandido.
    * Em alguns casos, arrays são mais performáticos, mas, em geral, `List<>` é mais flexível.

### Removendo de Contêineres Enquanto Itera

C# não fornece um mecanismo óbvio para remover itens de contêineres enquanto itera. Existem algumas opções:

*   Se tudo o que é necessário é remover itens que satisfazem uma condição, someList.RemoveAll(somePredicate) é recomendado.
*   Se outros trabalhos precisam ser feitos na iteração, RemoveAll pode não ser suficiente.
    Um padrão alternativo comum é criar um novo contêiner fora do loop, inserir itens para
    manter no novo contêiner e trocar o contêiner original pelo novo ao final da iteração.

### Chamando delegates

*   Ao chamar um delegado, use `Invoke()` e o operador condicional nulo - por exemplo,
    `SomeDelegate?.Invoke()`. Isso marca claramente a chamada no local da chamada como
    ‘um delegado que está sendo chamado’. A verificação nula é concisa e robusta contra
    condições de corrida de threads.

### A Palavra-Chave `var`

*   O uso de `var` é encorajado se ajudar na legibilidade ao evitar nomes de tipos que
    são braulhentos, óbvios ou não importantes.
*   Encorajado:

    *   Quando o tipo é óbvio - e.g. `var apple = new Apple();`, ou `var
        request = Factory.Create<HttpRequest>();`
    *   Para variáveis transitórias que são passadas diretamente para outros métodos -
        e.g. `var item = GetItem(); ProcessItem(item);`

*   Desencorajado:

    *   Ao trabalhar com tipos básicos - e.g. `var success = true;`
    *   Ao trabalhar com tipos numéricos incorporados resolvidos pelo compilador - e.g. `var
        number = 12 * ReturnsFloat();`
    *   Quando os usuários se beneficiariam claramente ao conhecer o tipo - e.g. `var
        listOfItems = GetList();`

### Atributos

*   Atributos devem aparecer na linha acima do campo, propriedade ou método com
    o qual estão associados, separados do membro por uma quebra de linha.
*   Múltiplos atributos devem ser separados por quebras de linha. Isso facilita
    a adição e remoção de atributos e garante que cada atributo seja fácil de pesquisar.

### Nomeação de Argumentos

Quando o significado de um argumento de função não é óbvio, considere uma das seguintes soluções:

*   Se o argumento for uma constante literal e a mesma constante for usada em
    várias chamadas de função de uma forma que pressupõe tacitamente que elas
    são iguais, use uma constante nomeada para tornar essa restrição explícita
    e garantir que ela se mantenha.
*   Considere alterar a assinatura da função para substituir um argumento bool
    por um argumento enum. Isso tornará os valores dos argumentos auto-descritivos.
*   Substitua expressões grandes ou complexas aninhadas por variáveis nomeadas.
*   Para funções que têm várias opções de configuração, considere definir uma
    única classe ou struct para armazenar todas as opções e passar uma instância dela.
    Essa abordagem tem várias vantagens. As opções são referenciadas pelo nome no
    local da chamada, o que esclarece seu significado. Também reduz a contagem de
    argumentos da função, tornando as chamadas de função mais fáceis de ler e escrever.
    Como benefício adicional, os locais de chamada não precisam ser alterados quando uma nova opção é adicionada.
    
Considere o seguinte exemplo:

```c#
// Bad - what are these arguments?
DecimalNumber product = CalculateProduct(values, 7, false, null);
```

versus:

```c#
// Good
ProductOptions options = new ProductOptions();
options.PrecisionDecimals = 7;
options.UseCache = CacheUsage.DontUseCache;
DecimalNumber product = CalculateProduct(values, options, completionDelegate: null);
```
## Diretrizes de Métodos em C#

### Sobrecarga de Métodos

*   Tente usar nomes de parâmetro descritivos para indicar o padrão usado por sobrecargas mais curtas.
*   Evite variar arbitrariamente nomes de parâmetro em sobrecargas. Se um parâmetro em uma sobrecarga representar a mesma entrada que um parâmetro em outra sobrecarga, os parâmetros deverão ter o mesmo nome.
*   Evite ser inconsistente na ordenação dos parâmetros em membros sobrecarregados. Parâmetros com o mesmo nome devem aparecer na mesma posição em todas as sobrecargas.
*   Faça apenas a sobrecarga mais longa virtual (se a extensibilidade for necessária). Sobrecargas mais curtas devem simplesmente chamar uma sobrecarga mais longa.
*   Não use os modificadores ref ou out para sobrecarregar membros.
*   Não faça sobrecargas com parâmetros na mesma posição e tipos semelhantes ainda que com semântica diferente.
*   Permita que null seja passado para argumentos opcionais.
*   Use sobrecarga de membro em vez de definir membros com argumentos padrão.

### Propriedades

*   Crie propriedades somente get se o chamador não puder alterar o valor da propriedade.
*   Não forneça propriedades somente set ou propriedades com um setter que tenha acessibilidade mais ampla do que o getter.
*   Forneça valores padrão concretos para todas as propriedades, garantindo que os padrões não resultem em uma brecha de segurança ou código extremamente ineficiente.
*   Permita que as propriedades sejam definidas em qualquer ordem, mesmo que isso resulte em um estado temporário inválido do objeto.
*   Preserve o valor anterior se um setter de propriedade gerar uma exceção.
*   Evite gerar exceções de getters de propriedade.

#### Propriedades Indexadas

*   Considere usar indexadores para dar acesso aos dados armazenados em uma matriz interna.
*   Considere fornecer indexadores em tipos que representam coleções de itens.
*   Evite usar propriedades indexadas com mais de um parâmetro.
*   Evite indexadores com tipos de parâmetro que não System.Int32, System.Int64, System.String, System.Object ou uma enumeração.
*   Use o nome Item para propriedades indexadas, a menos que haja um nome obviamente melhor (por exemplo, confira a propriedade Chars[] em System.String).
*   Não forneça um indexador e métodos semanticamente equivalentes.
*   Não forneça mais de uma família de indexadores sobrecarregados em um tipo.
*   Não use propriedades indexadas não padrão.

### Construtores

*   CONSIDERE fornecer construtores simples, idealmente padrão.
*   CONSIDERE o uso de um método de fábrica estático em vez de um construtor se a semântica da operação desejada não for mapeada diretamente para a construção de uma nova instância ou se seguir as diretrizes de design do construtor não parecer natural.
*   USE parâmetros de construtor como atalhos para definir as propriedades principais.
*   USE o mesmo nome para parâmetros de construtor e uma propriedade se os parâmetros do construtor forem usados para simplesmente definir a propriedade.
*   FAÇA um trabalho mínimo no construtor.
*   GERE exceções de construtores de instância, se apropriado.
*   DECLARE explicitamente o construtor público sem parâmetros em classes, se esse construtor for necessário.
*   EVITE definir explicitamente construtores sem parâmetros em structs.
*   EVITE chamar membros virtuais em um objeto dentro de seu construtor.

### Eventos

*   Use o termo "gerar” para eventos em vez de "lançar" ou "disparar".
*   Use System.EventHandler<TEventArgs> em vez de criar manualmente novos representantes para serem usados como manipuladores de eventos.
*   CONSIDERE usar uma subclasse de EventArgs como argumento do evento, a menos que você tenha certeza absoluta de que o evento nunca precisará carregar nenhum dado para o método de manipulação de eventos. Nesse caso, use diretamente o tipo EventArgs.
*   Use um método virtual protegido para gerar cada evento. Isso é aplicável somente a eventos não estáticos em classes não seladas, não a structs, classes seladas ou eventos estáticos.
*   Defina um parâmetro para o método protegido que gera um evento.
*   Não transmita nulo como remetente ao gerar um evento não estático.
*   Transmita nulo como remetente ao gerar um evento estático.
*   Não transmita nulo como o parâmetro de dados do evento ao gerar um evento.
*   Considere gerar eventos que o usuário final possa cancelar. Isso só se aplica a pré-eventos.

#### Eventos Personalizados

*   Use um tipo de retorno nulo para manipuladores de eventos.
*   Use object como o tipo do primeiro parâmetro do manipulador de eventos e chame-o de sender.
*   Use System.EventArgs ou a respectiva subclasse como o tipo do segundo parâmetro do manipulador de eventos e chame-o de e.
*   Não tenha mais de dois parâmetros em manipuladores de eventos.

### Campos

*   NÃO forneça campos de instância públicos ou protegidos.
*   USE campos constantes para constantes que nunca serão alteradas.
*   USE campos estáticos públicos readonly para instâncias de objeto predefinidas.
*   NÃO atribua instâncias de tipos mutáveis a campos readonly.

### Métodos de Extensão

*   EVITE definir métodos de extensão de maneira frívola, especialmente em tipos que não são seus.
*   CONSIDERE usar métodos de extensão em qualquer um dos seguintes cenários:
*   EVITE definir métodos de extensão em System.Object.
*   NÃO coloque métodos de extensão no mesmo namespace que o tipo estendido, a menos que seja para adicionar métodos a interfaces ou para gerenciamento de dependências.
*   EVITE definir dois ou mais métodos de extensão com a mesma assinatura, mesmo que eles residam em namespaces diferentes.
*   CONSIDERE definir métodos de extensão no mesmo namespace que o tipo estendido se o tipo for uma interface e se os métodos de extensão forem destinados a serem usados na maioria ou em todos os casos.
*   NÃO defina métodos de extensão que implementam um recurso em namespaces normalmente associados a outros recursos. Em vez disso, defina-os no namespace associado ao recurso ao qual pertencem.
*   EVITE a nomenclatura genérica de namespaces dedicados aos métodos de extensão (por exemplo, "Extensões"). Use um nome descritivo (por exemplo, "Roteamento") em vez disso.

### Sobrecarga de Operador

*   EVITE definir sobrecargas de operador, exceto em tipos que devem parecer tipos primitivos (internos).
*   CONSIDERE definir sobrecargas de operador em um tipo que deve parecer um tipo primitivo.
*   DEFINA sobrecargas de operador em structs que representam números (como System.Decimal).
*   NÃO seja engraçadinho ao definir sobrecargas de operador.
*   NÃO forneça sobrecargas de operador, a não ser que pelo menos um dos operandos seja do tipo que define a sobrecarga.
*   SOBRECARREGUE operadores de maneira simétrica.
*   CONSIDERE fornecer métodos com nomes amigáveis que correspondem a cada operador sobrecarregado.

#### Operadores de Conversão

*   NÃO forneça um operador de conversão se essa conversão não for claramente esperada pelos usuários finais.
*   NÃO defina operadores de conversão fora do domínio de um tipo.
*   NÃO forneça um operador de conversão implícita se a conversão potencialmente tiver perda.
*   NÃO gere exceções de conversões implícitas.
*   GERE System.InvalidCastException se uma chamada para um operador de conversão resultar em uma conversão de perda e o contrato do operador não permitir conversões com perda.

### Parâmetros

*   Use o tipo de parâmetro menos derivado que fornece a funcionalidade exigida pelo membro.
*   NÃO use parâmetros reservados.
*   NÃO tenha métodos expostos publicamente que usem ponteiros, matrizes de ponteiros ou matrizes multidimensionais como parâmetros.
*   Coloque todos os parâmetros out seguindo todos os valores e parâmetros ref (excluindo matrizes de parâmetros), mesmo que isso resulte em uma inconsistência na ordenação de parâmetros entre sobrecargas (consulte Sobrecarga de membro).
*   Seja consistente na nomeação dos parâmetros ao substituir membros ou implementar membros da interface.

#### Enum e Boolean

*   Use enumerações se um membro tiver dois ou mais parâmetros boolianos.
*   NÃO use boolianos, a menos que você tenha certeza absoluta de que nunca haverá necessidade de mais de dois valores.
*   Considere o uso de boolianos para parâmetros de construtor que são realmente valores de dois estados e são usados para inicializar propriedades booleanas.

#### Validação de Argumentos

*   Valide argumentos passados para membros públicos, protegidos ou explicitamente implementados. Gere System.ArgumentException ou uma de suas subclasses, se a validação falhar.
*   Gere ArgumentNullException se um argumento nulo for passado e o membro não oferecer suporte a argumentos nulos.
*   Valide parâmetros de enumeração.
*   NÃO use Enum.IsDefined para verificações de intervalo de enumeração.
*   Lembre-se de que os argumentos mutáveis podem ter sido alterados após a validação.

#### Passagem de Parâmetros

*   Evite usar os parâmetros out ou ref.
*   Não passe tipos de referência por referência.

### Eventos e retornos de chamadas

*   CONSIDERE usar retornos de chamada para permitir que os usuários forneçam código personalizado a ser executado pela estrutura.
*   CONSIDERE usar eventos para permitir que os usuários personalizem o comportamento de uma estrutura sem necessidade de entender o design orientado ao objeto.
*   PREFIRA eventos a retornos de chamada simples, pois eles são mais familiares para uma gama maior de desenvolvedores e são integrados ao preenchimento de declaração do Visual Studio.
*   EVITE usar retornos de chamada em APIs sensíveis ao desempenho.
*   USE os novos tipos Func<...>, Action<...> ou Expression<...> em vez de delegados personalizados ao definir APIs com retornos de chamada.
*   MEÇA e entender as implicações de desempenho de usar Expression<...>, em vez de usar delegados Func<...> e Action<...>.
*   Entenda que, ao chamar um delegado, você está executando código arbitrário, o que pode ter repercussões de segurança, correção e compatibilidade.

### Exceções

*   NÃO retorne códigos de erro.
*   RELATE relata falhas de execução gerando exceções.
*   CONSIDERE encerrar o processo chamando System.Environment.FailFast (.NET Framework recurso 2.0), em vez de gerar uma exceção, se o código encontrar uma situação em que não seja seguro para execução adicional.
*   NÃO use exceções para o fluxo normal de controle, se possível.
*   CONSIDERE as implicações de desempenho de gerar exceções. As taxas de geração acima de 100 por segundo provavelmente afetarão visivelmente o desempenho da maioria dos aplicativos.
*   DOCUMENTE todas as exceções geradas por membros publicamente chamáveis devido a uma violação do contrato de membro (em vez de uma falha do sistema) e trate-as como parte de seu contrato.
*   NÃO tem membros públicos que possam gerar ou não com base em alguma opção.
*   NÃO tenha membros públicos que retornem exceções como o valor retornado ou um parâmetro out.
*   CONSIDERE usar métodos do construtor de exceções.
*   NÃO gere exceções de blocos de filtro de exceção.
*   EVITE gerar explicitamente exceções de blocos finally. Exceções geradas implicitamente resultantes de métodos de chamada que geram são aceitáveis.

#### Tipos de Exeções

Exceção e SystemException
*   NÃO lance System.Exception ou System.SystemException.
*   NÃO capture System.Exception ou System.SystemException no código da estrutura, a menos que você pretenda relançar.
*   EVITE capturar System.Exception ou System.SystemException, exceto em manipuladores de exceção de nível superior.

ApplicationException
*   NÃO lance ou derive de ApplicationException.

InvalidOperationException
*   LANCE um InvalidOperationException se o objeto estiver em um estado inadequado.

ArgumentException, ArgumentNullException e ArgumentOutOfRangeException
*   LANCE ArgumentException ou um de seus subtipos se argumentos ruins forem passados para um membro. Prefira o tipo de exceção mais derivado, se aplicável.
*   DEFINA a propriedade ParamName ao lançar uma das subclasses de ArgumentException.
*   USE value para o nome do parâmetro de valor implícito dos setters de propriedade.

NullReferenceException, IndexOutOfRangeException e AccessViolationException
*   NÃO permita que APIs de chamada pública lancem de forma explícita ou implícita NullReferenceException, AccessViolationException ou IndexOutOfRangeException. Essas exceções são reservadas e lançadas pelo mecanismo de execução e na maioria dos casos indicam um bug.

StackOverflowException
*   NÃO lance StackOverflowException explicitamente. A exceção deve ser lançada explicitamente apenas pelo CLR.
*   NÃO capture StackOverflowException.

OutOfMemoryException
*   NÃO lance OutOfMemoryException explicitamente. Essa exceção deve ser lançada apenas pela infraestrutura CLR.

ComException, SEHException e ExecutionEngineException
*   NÃO lance COMException, ExecutionEngineException e SEHException explicitamente. Essas exceções devem ser lançadas apenas pela infraestrutura CLR.
