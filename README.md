# Fluxo de Trabalho

O Ciclo de Refinamento de Código é um fluxo de trabalho estruturado para garantir a qualidade e a 
consistência do código em cada etapa do desenvolvimento. Ele é composto pelas seguintes etapas:

*   Codificação: Nessa fase, os desenvolvedores escrevem o código conforme os
requisitos e especificações do projeto, focando na funcionalidade básica e na lógica principal.
*   Revisão de Estilo: O código passa por uma revisão cuidadosa para assegurar que esteja em
conformidade com as convenções de estilo e boas práticas estabelecidas no guia de estilo da equipe.
*   Revisão Lógica: Após a revisão de estilo, o código é avaliado quanto à sua lógica e estrutura modular.

<div align="center">
<img src="https://github.com/user-attachments/assets/bcca3fbe-b42c-45da-b626-c8addf1ec087" alt="Descrição da imagem" width="500" height="350">
</div>

Esse ciclo iterativo permite uma abordagem sistemática para o desenvolvimento de software, garantindo que o código entregue seja de qualidade e esteja em conformidade com os padrões estabelecidos.

# Unity at CEASB Style Guide

## Diretrizes de Organização

### Estrutura de Arquivos

O esqueleto básico do projeto deve seguir a ordenação a seguir:

```
Assets
├── 3rdParty
│ └── [CompanyName]
| | └── [Package Name]
| | | |── [Package Name] 
│ | | └── Version.txt (Com URL de origem, changelog) 
├── Art 
│ ├── Animation
│ │ ├── AnimationClips 
│ │ └── Animators
│ ├── Audio 
│ │ ├── AudioClips 
│ │ └── AudioMixers 
│ ├── Fonts 
│ ├── Materials 
│ ├── Models 
│ ├── Shaders 
│ ├── Sprites 
│ └── Textures
├── Documentation 
├── Prefabs 
│ └── MyHeroPrefab (usando MyHero.cs) 
├── Resources
├── Scenes
├── Scripts 
│ ├── Editor 
│ │ └── [MeuProjeto] (namespace MeuProjeto) 
│ │ | └── MyHeroEditor.cs 
│ ├── Runtime
│ │ └── [MeuProjeto] (namespace MeuProjeto) 
│ │ | ├── MyHero.cs 
│ │ | └── MyHeroSettings.cs 
│ └── Tests
| | └── [Desenvolvedor 1]
| | └── [Desenvolvedor 2]
└── Settings
  └── PhysicMaterials
  └── Presets
  └── Rendering
  └── Resources
  └── UIToolkit
```

### Arquivos

*   Áres de teste ou sandbox devem ser separadas com subpastas com nome dos respectivos desenvolvedores.
*   Nomes de arquivos e diretórios são em `PascalCase`, por exemplo, `MyFile.cs`.

### Criação de Subpastas

*   Crie uma subpasta se houver pelo menos 5 arquivos que podem ser agrupados por função, uso, ou contexto específico.
*   Crie uma subpasta caso ultrapasse 15 arquivos em uma pasta.
*   Não crie mais de quatro níveis de subpastas. Exemplo: `Assets > Art > Models > Player > Armadura` é aceitável, mas `Assets > Art > Models > Player > Armadura > Defesa` não é.

### Hierarchy

*   Use separadores `------ CATEGORIA ------` para agrupar logicamente os objetos que pertencem à mesma categoria ou funcionalidade.
*   Use nomes descritivos para indicar a função ou o grupo de objetos que estão abaixo deles. Por exemplo, `------ INIMIGOS ------`.
*   Use `snake_case` para nomear os objetos da hierarquia.
*   Use prefabs para manter a consistência e facilitar a reutilização de objetos. Sempre que possível, crie prefabs para objetos que serão usados várias vezes.

### Tags vs Layers

*   Use Layers para diferenciar tipos de objetos que precisam de configurações distintas, como física, renderização, ou interações com a câmera.
*   Use Tags para identificar GameObjects de forma única. Elas são úteis para encontrar e manipular objetos específicos em scripts.
*   Evite usar muitas tags para não complicar a gestão do projeto. Mantenha as tags simples e descritivas.
*   Nomeie as Layers de forma clara e descritiva. Exemplo: Player, Enemy, EnvironmentCollision.
*   Use nomes de tags consistentes e em inglês, mesmo que o projeto seja em outro idioma.

# C# at CEASB Style Guide

## Diretrizes de Documentação

### Comentários

#### Formatação

*   Faça comentários em português.
*   Use comentários de uma única linha `//` para explicações breves.
*   Evite comentários de várias linhas `/* */` para explicações mais longas. Os comentários não são localizados. Em vez disso, explicações mais longas estão no artigo complementar.
*   Para descrever métodos, classes, campos e todos os membros públicos, use `<summary>` utilizando apenas uma linha.
*   Comece o texto do comentário com uma letra maiúscula.
*   Finalize o texto do comentário com um ponto final.
*   Insira um espaço entre o delimitador de comentário `//` e o texto do comentário, conforme mostrado no exemplo a seguir.


#### Declaração

*   Comente para explicar o porquê. não o como. O código bem escrito deve ser autoexplicativo.
*   Mantenha os comentários curtos e diretos, utilizando uma linguagem clara e precisa.
*   Use `TODO` para indicar partes do código que precisam de melhorias ou que serão implementadas no futuro.
*   Use `FIXME` para marcar trechos de código que contêm problemas ou que necessitam de revisão urgente.
*   Use `NOTE` para destacar informações importantes ou advertências sobre o comportamento do código.

Exemplos:

```c#
/// <summary> Move o jogador na direção especificada. </summary>
/// <param name="direction">A direção do movimento.</param>
public void MovePlayer(Vector3 direction)
{
    // Código do método
}

private void Update()
{
    if (Input.GetKeyDown(KeyCode.P))
    {
        // TODO: Implementar funcionalidade de pausa
        PauseGame();
    }
}
```

## Diretrizes de Formatação

### Regras de Nomenclatura

#### Código

*   Todo o código, incluindo nomes de variáveis, classes e métodos, deve ser escrito em inglês.
*   Prefira configurar variáveis diretamente no Inspetor ao invés de buscar características por código.
*   Nomes de classes, métodos, enumerações, campos públicos, propriedades públicas, namespaces: `PascalCase`.
*   Nomes de variáveis locais, parâmetros: `camelCase`.
*   Nomes de campos e propriedades privadas, protegidas, internas e protegidas internas: `_camelCase`.
*   Para a escrita de palavras, qualquer coisa sem espaços internos, incluindo siglas, é considerada uma "palavra". Por exemplo, `MyRpc` em vez de `MyRPC`.
*   Escolha nomes de identificador facilmente legíveis.
*   Favoreça a legibilidade em vez da brevidade.
*   Não use sublinhados, hifens ou outros caracteres não alfanuméricos.
*   Não use abreviações ou contrações como parte de nomes de identificador.

#### Classes, Structs, Interfaces e Genéricos

*   Nomes de interfaces começam com `I`, por exemplo, `IInterface`.
*   Nomeie classes e structs com substantivos ou frases nominais, usando PascalCasing.
*   Nomeie interfaces com frases adjetivas ou, ocasionalmente, com substantivos ou frases nominais.
*   Considere encerrar o nome de classes derivadas com o nome da classe base.

#### Métodos

*   Nomeie os métodos usando verbos ou frases verbais.

#### Propriedades

*   Nomeie as propriedades usando um substantivo, uma frase nominal ou um adjetivo.
*   Não tenha propriedades que correspondam ao nome dos métodos "Get".
```c#
    // Incorreto
    public string TextWriter { get {...} set {...} }
    public string GetTextWriter(int value) { ... }
```
*   Nomeie as propriedades de coleção com uma frase no plural que descreva os itens na coleção em vez de usar uma frase no singular seguida por "List" ou "Collection".
```c#
    // Incorreto
    public List<string> NameList { get; set; }
    // Correto
    public List<string> Names { get; set; }
```
*   Nomeie as propriedades boolianas com uma frase afirmativa (CanSeek em vez de CantSeek). Opcionalmente, você também pode prefixar as propriedades boolianas com "Is", "Can" ou "Has", mas somente quando isso adicionar valor.
*   Considere nomear uma propriedade com o mesmo nome de seu tipo.
```c#
    public Color Color { get; set; }
```

#### Eventos

*   Nomeie os eventos com um verbo ou uma frase verbal.
*   Nomeie os eventos com um conceito de antes e depois, usando os tempos verbais presente e pretérito.
*   Nomeie os manipuladores de eventos (delegados usados como tipos de eventos) com o sufixo "EventHandler".
*   Nomeie as classes de argumento de evento com o sufixo "EventArgs".
```c#
    public ClosingEventArgs() => {};
    public ClosedEventArgs() => {};

    public delegate void ClosingEventHandler(object sender, ClosingEventArgs e);
    public delegate void ClosedEventHandler(object sender, ClosedEventArgs e);
    
    public event ClosingEventHandler Closing;
    public event ClosedEventHandler Closed;
```

#### Genéricos e Enumerações

*   Nomeie parâmetros de tipo genérico com nomes descritivos, a menos que um nome de uma única letra seja autoexplicativo e um nome descritivo não agregue valor.
*   Considere usar T como o nome do parâmetro de tipo em tipos com parâmetro de tipo de uma letra. Por exemplo, em uma classe genérica `List<T>`, `T` representa o tipo dos elementos na lista.
*   Use nomes de prefixo descritivos de parâmetro de tipo com T. Por exemplo, `TKey` e `TValue` em um dicionário genérico `Dictionary<TKey, TValue>`.
*   Considere indicar as restrições colocadas em um parâmetro de tipo no nome do parâmetro.
*   Use um nome de tipo singular para uma enumeração.
*   Não use um sufixo "Enum" em nomes de tipo enumerado.

### Organização

*   Onde for possível, o nome do arquivo deve ser o mesmo que o nome da classe principal no arquivo, por exemplo, `MyClass.cs`.
*   Em geral, prefira uma classe principal por arquivo.
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
*   Sem espaço após `if`/`for`/`while`, etc., e após vírgulas.
*   Nenhum espaço após um parêntese de abertura ou antes de um parêntese de fechamento.
*   As quebras de linha devem ocorrer após os operadores lógicos, se necessário.

## Diretrizes de Tipo

### Constantes

*   Variáveis e campos que podem ser const devem sempre ser const.
*   Se const não for possível, readonly pode ser uma alternativa adequada.
*   Prefira constantes nomeadas a números mágicos.

### Expressões Condicionais
*   Prefira a combinação de várias condições relacionadas em um único `if` quando isso melhora a legibilidade.
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

*   Considere definir um struct em vez de uma classe se as instâncias do tipo forem pequenas e normalmente de curta duração ou se forem comumente incorporadas em outros objetos.
*   Não forneça um construtor sem parâmetros para um struct.
*   Não defina tipos mutáveis de valor.
*   Evite definir um struct, a menos que o tipo tenha todas as características a seguir:
    * Representa logicamente um único valor, semelhante aos tipos primitivos (int, double etc.).
    * Tem um tamanho de instância inferior a 16 bytes.
    * É imutável.
    * Não precisará ser encaixotado com frequência.
    
```c#
    // Point é pequeno, usado em operações rápidas frequentemente e tem apenas um tipo.
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

*   Considere definir uma interface se você precisar dar suporte à sua funcionalidade em tipos que já herdam de algum outro tipo.
Exemplo:
```c#
    // Se você tem uma classe que já herda de outra classe,
    // mas precisa adicionar funcionalidade adicional, uma interface pode ser a solução.
    public class Animal
    {
        public void Eat() { /* ... */ }
    }
    
    public interface ICanFly
    {
        void Fly();
    }
    
    public class Bird : Animal, ICanFly
    {
        public void Fly() { /* ... */ }
    }
```
*   Sempre que você define uma interface, deve haver pelo menos uma classe que a implemente.
*   Forneça pelo menos um método que usa a interface como um parâmetro ou uma propriedade tipada como a interface.

### Enumeração

*   Use uma enumeração para parâmetros, propriedades e valores retornados fortemente tipados que representam conjuntos de valores.
*   Não use uma enumeração para conjuntos abertos (como a versão do sistema operacional, nomes de amigos etc.).
```c#
    // Incorreto
    // Conjuntos abertos podem mudar frequentemente, tornando as enumerações inadequadas.
    public enum OperatingSystem
    {
        Windows,
        MacOS,
        Linux
    }
```
*   Evite expor publicamente enumerações com apenas um valor.
*   Forneça um valor de zero em enumerações simples.
```c#
    public enum Status
    {
        None = 0, // Valor zero representando "nenhum estado"
        Active,
        Inactive
    }
```

### ref e out

*   Use out para retornos que não são também entradas.
```c#
    // O parâmetro out é usado quando você precisa retornar múltiplos valores de um método,
    // mas esses valores não são usados como entradas.
    public void GetCoordinates(out int x, out int y)
    {
        x = 10;
        y = 20;
    }
    
    public void ExampleUsage()
    {
        int x, y;
        GetCoordinates(out x, out y);
        Console.WriteLine($"Coordinates: ({x}, {y})");
    }
```


*   Coloque os parâmetros out após todos os outros parâmetros na definição do método.
*   ref deve ser usado raramente, quando é necessário modificar uma entrada.

### Array vs List

*   Em geral, prefira `List<>` em vez de arrays para variáveis públicas, propriedades e tipos de retorno.
*   Prefira `List<>` quando o tamanho do contêiner pode mudar.
*   Prefira arrays quando o tamanho do contêiner é fixo e conhecido no momento da construção.
*   Prefira arrays para arrays multidimensionais.

### Chamando delegates

*   Ao chamar um delegado, use `Invoke()` e o operador condicional nulo - por exemplo,
    `SomeDelegate?.Invoke()`.

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

## Diretrizes de Métodos em C#

### Sobrecarga de Métodos

*   Se um parâmetro em uma sobrecarga representar a mesma entrada que um parâmetro em outra sobrecarga, os parâmetros deverão ter o mesmo nome.
*   Parâmetros com o mesmo nome devem aparecer na mesma posição em todas as sobrecargas.
*   Permita que `null` seja passado para argumentos opcionais.

### Propriedades

*   Crie propriedades somente `get` se o chamador não puder alterar o valor da propriedade.
*   Não forneça propriedades somente `set` ou propriedades com um setter que tenha acessibilidade mais ampla do que o getter.

#### Propriedades Indexadas

*   Considere usar indexadores para dar acesso aos dados armazenados em uma matriz interna.
*   Se você estiver criando uma classe que representa uma coleção de itens, como uma lista personalizada ou um dicionário.
*   Evite usar propriedades indexadas com mais de um parâmetro.
*   Use o nome `Item` para propriedades indexadas.
```c#
    public class MyList
    {
        public List<string> Item = new List<string>();
    
        // Indexador para acessar itens na lista
        public string this[int index]
        {
            get { return Item[index]; }
            set { Item[index] = value; }
        }
    }
```

### Construtores

*   Faça construtores simples, idealmente padrão.
*   Use parâmetros de construtor como atalhos para definir as propriedades principais.
*   Use o mesmo nome para parâmetros de construtor e uma propriedade se os parâmetros do construtor forem usados para simplesmente definir a propriedade.
*   Construtores devem ser simples e rápidos, evitando lógica complexa.
*   Se um construtor não puder inicializar corretamente uma instância, ele deve lançar uma exceção.
Exemplo das regras acima:
```c#
    public class Account
    {
        public string Username { get; }
    
        public Account(string username)
        {
            if (string.IsNullOrWhiteSpace(username))
            {
                throw new ArgumentException("Username cannot be null or empty");
            }
            Username = username;
        }
    }
```

#### Casting

*   Não forneça um casting se essa conversão não for claramente esperada pelos usuários finais.
*   Não forneça um operador de conversão implícita se a conversão potencialmente tiver perda.

### Eventos

*   Considere usar eventos para permitir que os usuários personalizem o comportamento de uma estrutura sem necessidade de entender o design orientado ao objeto.
*   Prefira o tipo `UnityEvent` em vez dos novos tipos.
*   Prefira os novos tipos `Func<...>`, `Action<...>` ou `Expression<...>` em vez de delegados personalizados.


```c#
    // Ao invés de criar um delegado personalizado MyDelegate, use Action:
    public void ExecuteAction(Action<int> action)
    {
        action(42);  // Executa a ação passada
    }
    
    // Uso
    ExecuteAction(x => Console.WriteLine(x * 2));  // Imprime 84
```
