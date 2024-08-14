# C# at CEASB Style Guide

## Diretrizes de Formatação

### Regras de Nomenclatura

#### Código

*   Nomes de classes, métodos, enumerações, campos públicos, propriedades públicas, namespaces: `PascalCase`.
*   Nomes de variáveis locais, parâmetros: `camelCase`.
*   Nomes de campos e propriedades privadas, protegidas, internas e protegidas internas: `_camelCase`.
*   A convenção de nomenclatura não é afetada por modificadores como const, static, readonly, etc.
*   Para a escrita de palavras, qualquer coisa sem espaços internos, incluindo siglas, é considerada uma "palavra". Por exemplo, `MyRpc` em vez de `MyRPC`.
*   Nomes de interfaces começam com `I`, por exemplo, `IInterface`.
*   Escolha nomes de identificador facilmente legíveis.
*   Favoreça a legibilidade em vez da brevidade.
*   Não use sublinhados, hifens ou outros caracteres não alfanuméricos.
*   Não use abreviações ou contrações como parte de nomes de identificador.

#### Arquivos

*   Nomes de arquivos e diretórios são em `PascalCase`, por exemplo, `MyFile.cs`.
*   Onde for possível, o nome do arquivo deve ser o mesmo que o nome da classe principal no arquivo, por exemplo, `MyClass.cs`.
*   Em geral, prefira uma classe principal por arquivo.

#### Classes, Structs, Interfaces e Genéricos

*   NOMEIE classes e structs com substantivos ou frases nominais, usando PascalCasing.
*   NOMEIE interfaces com frases adjetivas ou, ocasionalmente, com substantivos ou frases nominais.
*   CONSIDERE encerrar o nome de classes derivadas com o nome da classe base.
*   FAÇA nomeações de interface de prefixo com a letra I, para indicar que o tipo é uma interface.
*   VERIFIQUE se os nomes diferem-se apenas pelo prefixo "I" no nome da interface quando você estiver definindo um par classe-interface em que a classe é uma implementação padrão da interface.

#### Métodos

*   NOMEIE os métodos que sejam verbos ou frases verbais.

#### Propriedades

*   NOMEIE as propriedades usando um substantivo, uma frase nominal ou um adjetivo.
*   NÃO tenha propriedades que correspondam ao nome dos métodos "Get", como no exemplo a seguir:
*   NOMEIE as propriedades de coleção com uma frase no plural que descreva os itens na coleção em vez de usar uma frase no singular seguida por "List" ou "Collection".
*   NOMEIE as propriedades boolianas com uma frase afirmativa (CanSeek em vez de CantSeek). Opcionalmente, você também pode prefixar as propriedades boolianas com "Is", "Can" ou "Has", mas somente quando isso adicionar valor.
*   CONSIDERE nomear uma propriedade com o mesmo nome de seu tipo.

#### Eventos

*   NOMEIE os eventos com um verbo ou uma frase verbal.
*   NOMEIE os eventos com um conceito de antes e depois, usando os tempos verbais presente e pretérito.
*   NOMEIE os manipuladores de eventos (delegados usados como tipos de eventos) com o sufixo "EventHandler".
*   USE dois parâmetros nomeados como sender e e nos manipuladores de eventos.
*   NOMEIE as classes de argumento de evento com o sufixo "EventArgs".

#### Campos

*   USE PascalCasing nos nomes de campos.
*   NOMEIE os campos usando um substantivo, uma frase nominal ou um adjetivo.
*   NÃO use um prefixo para nomes de campos.

#### Genéricos e Enumerações

*   NOMEIE parâmetros de tipo genérico com nomes descritivos, a menos que um nome de uma única letra seja autoexplicativo e um nome descritivo não agregue valor.
*   CONSIDERE usar T como o nome do parâmetro de tipo em tipos com parâmetro de tipo de uma letra.
*   USE nomes de prefixo descritivos de parâmetro de tipo com T.
*   CONSIDERE indicar as restrições colocadas em um parâmetro de tipo no nome do parâmetro.
*   USE um nome de tipo singular para uma enumeração, a menos que seus valores sejam campos de bits.
*   NÃO use um sufixo "Enum" em nomes de tipo enumerado.

### Organização

*   Modificadores ocorrem na seguinte ordem: `public protected internal private
    new abstract virtual override sealed static readonly extern unsafe volatile
    async`.
*   Ordem dos membros da classe:
    *   Agrupe os membros da classe na seguinte ordem:
        *   Classes aninhadas, enums, delegates e eventos.
        *   Campos static, cons e readonly.
        *   Campos e propriedades.
        *   Construtores e finalizadores.
        *   Métodos.
    *   Dentro de cada grupo, os elementos devem estar na seguinte ordem:
        *   Public.
        *   Internal.
        *   Protected internal.
        *   Protected.
        *   Private.
    *   Onde for possível, agrupe as implementações de interfaces juntas.

### Regras de Espaçamento

*   Use o estilo "Allman" para chaves: abra e feche sua própria nova linha. As chaves se alinham com o nível de recuo atual.
*   Limite de colunas: 80.
*   Chaves usadas mesmo quando opcionais.
*   Espaço após `if`/`for`/`while`, etc., e após vírgulas.
*   Nenhum espaço após um parêntese de abertura ou antes de um parêntese de fechamento.
*   Não adicione um espaço após o parêntese e os argumentos de função, por exemplo, CollectItem(myObject, 0, 1);
*   As quebras de linha devem ocorrer antes dos operadores binários, se necessário.

## Diretrizes de Tipo

### Constantes

*   Variáveis e campos que podem ser const devem sempre ser const.
*   Se const não for possível, readonly pode ser uma alternativa adequada.
*   Prefira constantes nomeadas a números mágicos.

### Expressões Condicionais
*   Prefira retornos antecipados em vez de aninhamento de blocos if.
*   Prefira a combinação de várias condições relacionadas em um único if quando isso melhora a legibilidade.

Exemplo:

Antes:
```c#
public void ProcessOrder(Order order)
{
    if (order != null)
    {
        if (order.IsPaid)
        {
            if (order.HasItems)
            {
                // Process the order
                Console.WriteLine("Order processed.");
            }
            else
            {
                Console.WriteLine("Order has no items.");
            }
        }
        else
        {
            Console.WriteLine("Order is not paid.");
        }
    }
    else
    {
        Console.WriteLine("Order is null.");
    }
}

```
Depois:
```c#
public void ProcessOrder(Order order)
{
    if (order == null)
    {
        Console.WriteLine("Order is null.");
        return;
    }

    if (!order.IsPaid)
    {
        Console.WriteLine("Order is not paid.");
        return;
    }

    if (!order.HasItems)
    {
        Console.WriteLine("Order has no items.");
        return;
    }

    // Process the order
    Console.WriteLine("Order processed.");
}
```
### Classe vs Struct

*   CONSIDERE definir um struct em vez de uma classe se as instâncias do tipo forem pequenas e normalmente de curta duração ou se forem comumente incorporadas em outros objetos.
*   EVITE definir um struct, a menos que o tipo tenha todas as características a seguir:
    * Representa logicamente um único valor, semelhante aos tipos primitivos (int, double etc.).
    * Tem um tamanho de instância inferior a 16 bytes.
    * É imutável.
    * Não precisará ser encaixotado com frequência.

#### Design de Struct

*   NÃO forneça um construtor sem parâmetros para um struct.
*   NÃO defina tipos mutáveis de valor.
*   VERIFIQUE se um estado em que todos os dados da instância estão definidos como zero, falsos ou nulos (conforme apropriado) é válido.
*   Implemente IEquatable<T> nos tipos de valor.
*   NÃO estenda ValueType explicitamente. Na verdade, a maioria das linguagens impede isso.
 
### Interface

*   DEFINA uma interface se você precisar que alguma API comum tenha suporte de um conjunto de tipos que incluem tipos de valor.
*   CONSIDERE definir uma interface se você precisar dar suporte à sua funcionalidade em tipos que já herdam de algum outro tipo.
*   EVITE o uso de interfaces de marcador (interfaces sem membros).
*   Se você precisar marcar uma classe como tendo uma característica específica (marcador), no geral, use um atributo personalizado em vez de uma interface.
*   FORNEÇA pelo menos um tipo que é uma implementação de uma interface.
*   Fazer isso ajuda a validar o design da interface. Por exemplo, List<T> é uma implementação da interface IList<T>.
*   Forneça pelo menos uma API que consome cada interface que você define (um método que usa a interface como um parâmetro ou uma propriedade tipada como a interface).
*   Não adicione membros a uma interface que tenha sido enviada anteriormente.

### Enumeração

*   USE uma enumeração para parâmetros, propriedades e valores retornados fortemente tipados que representam conjuntos de valores.
*   PREFIRA usar uma enumeração, em vez de constantes estáticas.
*   NÃO use uma enumeração para conjuntos abertos (como a versão do sistema operacional, nomes de amigos etc.).
*   NÃO forneça valores de enumeração reservados destinados a uso futuro.
*   EVITE expor publicamente enumerações com apenas um valor.
*   NÃO inclua valores sentinelas em enumerações.
*   FORNEÇA um valor de zero em enumerações simples.

### Tipos Aninhados

*   USE tipos aninhados quando a relação entre o tipo aninhado e seu tipo externo for tal que a semântica de acessibilidade de membros seja desejável.
*   NÃO use tipos aninhados públicos como um constructo de agrupamento lógico; use namespaces para isso.
*   EVITE tipos aninhados expostos publicamente. A única exceção a isso é se variáveis do tipo aninhado precisarem ser declaradas apenas em cenários raros, como subclasse ou outros cenários avançados de personalização.
*   NÃO use tipos aninhados se o tipo provavelmente for referenciado fora do tipo que o contém.
*   NÃO use tipos aninhados se eles precisarem ser instanciados pelo código do cliente. Se um tipo tiver um construtor público, ele provavelmente não deve ser aninhado.
*   NÃO defina um tipo aninhado como membro de uma interface. Há muitas linguagens que não dão suporte a esse constructo.

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

*   Desencourajado:

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
Derivado do guia de estilo C++ do Google.

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

*   TENTE usar nomes de parâmetro descritivos para indicar o padrão usado por sobrecargas mais curtas.

*   EVITE variar arbitrariamente nomes de parâmetro em sobrecargas. Se um parâmetro em uma sobrecarga representar a mesma entrada que um parâmetro em outra sobrecarga, os parâmetros deverão ter o mesmo nome.

*   EVITE ser inconsistente na ordenação dos parâmetros em membros sobrecarregados. Parâmetros com o mesmo nome devem aparecer na mesma posição em todas as sobrecargas.

*   FAÇA apenas a sobrecarga mais longa virtual (se a extensibilidade for necessária). Sobrecargas mais curtas devem simplesmente chamar uma sobrecarga mais longa.

*   NÃO use os modificadores ref ou out para sobrecarregar membros.
*   NÃO faça sobrecargas com parâmetros na mesma posição e tipos semelhantes ainda que com semântica diferente.
*   PERMITA que null seja passado para argumentos opcionais.
*   USE sobrecarga de membro em vez de definir membros com argumentos padrão.
