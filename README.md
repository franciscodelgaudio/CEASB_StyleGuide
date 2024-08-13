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

#### Arquivos

*   Nomes de arquivos e diretórios são em `PascalCase`, por exemplo, `MyFile.cs`.
*   Onde for possível, o nome do arquivo deve ser o mesmo que o nome da classe principal no arquivo, por exemplo, `MyClass.cs`.
*   Em geral, prefira uma classe principal por arquivo.

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

## Diretrizes de Codificação em C#

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
