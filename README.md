# Encapsulando Algoritmos✨✨


![homem trabalhando no buraco](../img_readme/homem_trabalhando_buraco_315.png)

---

> Estamos em processo de encapsulamento. Já encapsulamos a criação de objetos, invocação de métodos, interfaces complexas, patos, pizzas... O que poderia ser agora? Vamos começar a encapsular partes de algoritmos para que as subclasses possam se conectar diretamente a um processo computacional sempre que quiserem. Vamos até aprender sobre um princípio de design inspirado em Hollywood. Vamos começar...
> 

---
## É Hora de Mais Cafeína

Algumas pessoas não conseguem viver sem café. Outras não conseguem viver sem o chá. O ingrediente comum? Cafeína, claro!
Mas há mais. O chá e o café são feitos de maneiras muito semelhantes. Vamos dar uma olhada:

![receita starbuzz cafe](../img_readme/receita_starbuzz_316.png)

## Preparando Algumas Classes de Café e Chá (em Python, é claro)

Vamos brincar de “codificar barista” e escrever alguns códigos para criar café e chá.

Aqui está o código para café.

```python
# Nossa classe para fazer café.
class Cafe:
    # Aqui está a receita de café, 
    # tirada diretamente do manual de treinamento.
    # Cada uma das etapas é implementada 
    # como um método separado.
    def preparar_receita(self):
        self.ferver_agua()
        self.preparar_cafe()
        self.despejar_na_xicara()
        self.adicionar_acucar_e_leite()

	
	 # Cada um desses métodos implementa uma etapa do algoritmo.
	 def ferver_agua(self):
        print("Fervendo água")

    def preparar_cafe(self):
        print("Passando o café pelo filtro")

    def despejar_na_xicara(self):
        print("Despejando na xícara")

    def adicionar_acucar_e_leite(self):
        print("Adicionando açúcar e leite")


cafe = Cafe()
cafe.prepararReceita()
```
---

Agora o chá.

```python
class Cha:
    
    # Isso é muito semelhante ao que acabamos de implementar 
    # na Classe Cafe. 
    # A segunda e a quarta etapas são diferentes, 
    # mas é basicamente a mesma receita.
    def preparar_receita(self):
        self.ferver_agua()
        self.infundir_saquinho_de_cha()
        self.despejar_na_xicara()
        self.adicionar_limao()


    # Observe que esse método é exatamente igual  
    # ao da Classe Cafe
    # Temos alguma duplicação de código acontecendo aqui.
    def ferver_agua(self):
        print("Fervendo a água")

    # Esse método é específico para chá.
    def infundir_saquinho_de_cha(self):
        print("Infundindo o saquinho de chá")

    # Observe que esse método também é exatamente igual  
    # ao da Classe Cafe
    # Temos alguma duplicação de código acontecendo aqui.
    def despejar_na_xicara(self):
        print("Despejando na xícara")
        
    # Esse método é específico para chá.
    def adicionar_limao(self):
        print("Adicionando limão")

cha = Cha()
cha.preparar_receita()
```

### Observação Importante...

![observação duplicação código](../img_readme/duplicacao_codigo_318.png)

## Vamos abstrair as Classes Café e Chá

O diagrama das classes com o exercício de abstrair, poderia ser desenhado assim.

![abstraindo cafe e cha](../img_readme/abstraindo_classes_cafe_cha_320.png)

## Levando o design mais adiante...

Então, o que mais as classes `Coffee` (**Café**) e `Tea` (**Chá**) têm em comum? Vamos começar com as receitas.

![receitas cafe e cha](../img_readme/receitas_cafe_cha_321.png)

Observe que ambas as receitas seguem o mesmo algoritmo. Veja a figura abaixo.

![receitas mesmo algoritmo](../img_readme/receitas_mesmo_algoritmo_321.png)

Surge, então a pergunta: podemos encontrar uma maneira de abstrair um método chamado `preparar_receita()` também? Sim, vamos tentar...

## Abstraindo o método `preparar_receita()`

Vamos abstrair `preparar_receita	()` usando um passo a passo para cada subclasse (ou seja, `Cafe` e `Cha`).

* O primeiro problema que temos é que a classe `Cafe` usa os métodos `preparar_cafe()` e `adicionar_acucar_e_leite()`, enquanto que a classe `Cha` usa os métodos `infundir_saquinho_de_cha()` e `adicionar_limao()`.

![metodo preprar_receita](../img_readme/metodo_preparar_receita_322.png)

> Vamos pensar sobre isso: a moagem e a infusão não são tão diferentes. Eles são bastante análogos. Então, vamos criar um novo nome de método, digamos, `fazer_infusao()`, e usaremos o mesmo nome quer estejamos preparando café ou infundindo chá.
> 
> Da mesma forma, adicionar açúcar e leite é praticamente o mesmo que adicionar limão: ambos adicionam condimentos à bebida. Vamos também criar um novo nome de método, `adicionar_condimentos()`, para lidar com isso. 
> 
> Portanto, nosso novo método `preparar_receita()` ficará assim:

```python
def preparar_receita(self):
  self.ferver_agua()
  self.fazer_infusao()
  self.despejar_na_xicara()
  self.adicionar_condimentos()
```

* Agora temos um novo método `preparar_receita()`, mas precisamos encaixá-lo no código. Para fazer isso, começaremos com a superclasse `BebidaCafeinada`.

```python
from abc import ABC, abstractmethod

# Esta classe é abstrata
class BebidaCafeinada(ABC):
    # Este método será usado para fazer chá e café. 
    # Generalizamos as etapas 2 e 4 para `fazer_infusao()` e
    # para `adicionar_condimentos()`.
    def preparar_receita(self):
        self.ferver_agua()
        self.fazer_infusao()
        self.despejar_na_xicara()
        self.adicionar_condimentos()

    # Como as classes Cafe e Cha lidam com esses métodos 
    # de maneiras diferentes, 
    # eles terão que ser declarados como abstratos. 
    # Deixe as subclasses se preocuparem com essas coisas
    @abstractmethod
    def fazer_infusao(self):
        pass

    # Como as classes Cafe e Cha lidam com esses métodos 
    # de maneiras diferentes, 
    # eles terão que ser declarados como abstratos. 
    # Deixe as subclasses se preocuparem com essas coisas
    @abstractmethod
    def adicionar_condimentos(self):
        pass

    def ferver_agua(self):
        print("Fervendo água")

    def despejar_na_xicara(self):
        print("Despejando na xícara")


class Cha(BebidaCafeinada):
    def fazer_infusao(self):
        print("Preparando chá")

    def adicionar_condimentos(self):
        print("Adicionando limão")


class Cafe(BebidaCafeinada):
    def fazer_infusao(self):
        print("Passando café no filtro")

    def adicionar_condimentos(self):
        print("Adicionando açúcar e leite")

if __name__ == "__main__":
    cha = Cha()
    cafe = Cafe()

    print("Preparando chá...")
    cha.preparar_receita()

    print("\nPreparando café...")
    cafe.preparar_receita()
```

O diagrama de classes para o código acima está na figura abaixo.

![classe BebidaCafeinada](../img_readme/classe_BebidaCafeinada.png)

## O que nós fizemos?

A figura abaixo mostra nossos procedimentos.

![o que fizemos](../img_readme/o_que_fizemos_cafe_cha_325.png)

## Conheça o Padrão `Template Method`

Basicamente, acabamos de implementar o padrão `Template Method`. Mas, que é isso? Vejamos a estrutura da classe `BebidaCafeinada` na figura abaixo. Ela ilustra este padrão de uma forma real.

![coheça template method](../img_readme/conheca_template_method_326.png)

> #### O `Template Method` define as etapas de um algoritmo e permite que as subclasses forneçam a implementação de um ou mais passos.

## Por trás dos bastidores (behind the scenes), vamos fazer um pouco de chá...

Vamos preparar um chá e ver como funciona o `Template Method`. Você verá que ele controla um algoritmo. E em determinados pontos deste algoritmo, o método permite que a subclasse forneça a implementação dos passos...

![fazendo um pouco de chá](../img_readme/fazendo_pouco_cha_327.png)

## O que este padrão (i.e. `Template Method`) nos trouxe?

Implementação sem Padrão | Implementação com Padrão
--------- | ------
`Cafe` e `Cha` comandam o show; eles controlam o algoritmo | A classe `BebidaCafeinada` comanda o show; ela possui o algoritmo e o protege
O código é duplicado em `Cafe` e `Cha` | A classe `BebidaCafeinada` maximiza a reutilização entre as subclasses.
As alterações de código no algoritmo exigem a abertura das subclasses e a realização de diversas alterações | O algoritmo reside em um determinado local e as alterações no código só precisam ser feitas lá
As classes são organizadas em uma estrutura que exige muito trabalho para adicionar uma nova bebida com cafeína | O `Template Method Pattern` fornece uma estrutura à qual outras bebidas com cafeína podem ser conectadas. Novas bebidas com cafeína só precisam implementar alguns métodos
O conhecimento do algoritmo e como implementá-lo é distribuído por muitas classes | A classe `BebidaCafeinada` concentra o conhecimento sobre o algoritmo e depende de subclasses para fornecer implementações completas

---

## Definindo o Padrão `Template Method`

Você viu como o este padrão funciona em nosso exemplo de Chá e Café. Agora, confira a definição oficial e acerte todos os detalhes.

<style>
mark{
    color:black;
    background-color: #00FF00;
}
</style>

<mark> **O `Template Method Pattern` define o esqueleto de um algoritmo em um método, adiando alguns passos para subclasses. Este padrão permite que as subclasses redefinam certos passos de um algoritmo sem alterar a estrutura dele.** 
</mark>

> Este padrão trata da criação de um _template_ (modelo) para um algoritmo. O que é um modelo? Como você viu, é apenas um método. Ou mais especificamente, é um método que define um algoritmo como um conjunto de passos. Um ou mais desses passos são definidos como abstratos e implementados por uma subclasse. Isso garante que a estrutura do algoritmo permaneça inalterada, enquanto as subclasses fornecem parte da implementação.
> 

Observe o diagrama na figura abaixo.

![diagrama de classes template method](../img_readme/diagrama_classe_template_method_329.png)

Vamos agora dar uma olhada mais de perto em como `AbstractClass` é definido, incluindo o método de modelo (`templateMethod()`) e as operações primitivas 1 e 2 (`primitiveOperations()`).

Observe a figura abaixo:

![abstract classe with hooks](../img_readme/abstract_class_with_hooks_331.png)

## Usando o "hook" no padrão `TemplateMethod`

![usando o hook](../img_readme/usando_hook_332.png)

Um **gancho** (_hook_) é um método declarado na classe abstrata, mas apenas com uma implementação vazia ou padrão. Isso dá às subclasses a capacidade de “**se conectar**” ao algoritmo em vários pontos, se desejarem. Uma subclasse também está livre para ignorar o gancho. 

Existem vários usos para ganchos. Vamos dar uma olhada em um agora. Falaremos sobre alguns outros mais tarde. 

---

#### Algumas observações:

> Para usar o _hook_, nós o substituímos em nossa subclasse. Aqui, ele controla se a classe `BebidaCafeinadaComHook` avalia uma determinada parte do algoritmo – ou seja, se adiciona um condimento à bebida.
> 
> Como sabemos se o cliente quer o condimento? Basta perguntar!

Dê uma olhada no código abaixo.

```python
from abc import ABC, abstractmethod

class BebidaCafeinadaComGancho(ABC):

  def preparar_receita(self):
    self.ferver_agua()
    self.preparar_bebida()
    self.despejar_na_xicara()
    # Adicionamos uma pequena declaração condicional que baseia seu
    # sucesso em um método concreto, chamado `cliente_quer_condimentos()`. 
    # Se o cliente QUISER condimentos, 
    # só então chamamos o método `adicionar_condimentos()`.
    if self.cliente_quer_condimentos():
      self.adicionar_condimentos()

  @abstractmethod
  def preparar_bebida(self):
    pass

  @abstractmethod
  def adicionar_condimentos(self):
    pass

  def ferver_agua(self):
    print("Fervendo água")

  def despejar_na_xicara(self):
    print("Despejando na xícara")

  # Aqui definimos um método com uma implementação default (quase sempre) vazia. 
  # Este método apenas retorna verdadeiro e não faz mais nada.
  # Isso é um `hook` porque a subclasse pode substituir esse método, 
  # mas não é necessário.
  def cliente_quer_condimentos(self):
    return True


class CafeComGancho(BebidaCafeinadaComGancho):
  def preparar_bebida(self):
    print("Passando o café pelo filtro")

  def adicionar_condimentos(self):
    print("Adicionando açúcar e leite")

  # É aqui que você substitui o `hook` 
  # e fornece sua própria funcionalidade.
  def cliente_quer_condimentos(self):
    # Obtenha a opinião do usuário sobre a decisão do condimento 
    # código otimizado para Python
    resposta = self.obter_entrada_do_usuario()
    return resposta.lower().startswith('s')

  # Este trecho de código pergunta se o usuário gostaria de leite e açúcar 
  # e obtém a entrada da linha de comando
  def obter_entrada_do_usuario(self):
    resposta = input("Você gostaria de açúcar e leite no seu café (s/n)? ")
    return resposta


class ChaComGancho(BebidaCafeinadaComGancho):
  def preparar_bebida(self):
    print("Preparando o chá")

  def adicionar_condimentos(self):
    print("Adicionando limão")

  def cliente_quer_condimentos(self):
    resposta = self.obter_entrada_do_usuario()
    return resposta.lower().startswith('s')

  def obter_entrada_do_usuario(self):
    resposta = input("Você gostaria de limão no seu chá (s/n)? ")
    return resposta


#testando o código
def main():
  cha = ChaComGancho()
  cafe = CafeComGancho()

  print("\nPreparando chá...")
  cha.preparar_receita()

  print("\nPreparando café...")
  cafe.preparar_receita()

if __name__ == "__main__":
  main()
```

---

> Este foi um exemplo muito interessante de como um gancho (_hook_) pode ser usado para controlar condicionalmente o fluxo do algoritmo na classe abstrata.

---

## Perguntas & Respostas (Q & A)

**Pergunta #1**: Ao criar um `template method`, como posso saber quando usar métodos abstratos e quando usar ganchos?

**Resposta #1**: Use métodos abstratos quando sua subclasse DEVE fornecer uma implementação do método ou o passo do algoritmo. Use _hooks_ quando essa parte do algoritmo for opcional. Com eles, uma subclasse pode optar por implementá-lo, mas não é obrigatório.

**Pergunta #2**: Para que realmente servem os ganchos (_hooks_)?

**Resposta #2**: Existem alguns usos de ganchos. Como acabamos de dizer, um gancho pode fornecer uma maneira para uma subclasse implementar uma parte opcional de um algoritmo ou, se não for importante para a implementação da subclasse, pode ignorá-la. Outro uso é dar à subclasse a chance de reagir a algum passo do método modelo que está prestes a acontecer ou que acabou de acontecer. Por exemplo, um método de gancho como `justReorderedList()` permite que a subclasse execute alguma atividade (como reexibir uma representação na tela) após uma lista interna ser reordenada. Como você viu, um gancho também pode fornecer a uma subclasse a capacidade de tomar uma decisão pela classe abstrata.

**Pergunta #3**: Uma subclasse precisa implementar todos os métodos abstratos da classe abstrata?

**Resposta #3**: Sim, cada subclasse concreta define todo o conjunto de métodos abstratos e fornece uma implementação completa das etapas indefinidas do algoritmo do método modelo.

**Pergunta #4**: Parece que eu deveria manter meus métodos abstratos em número pequeno. Caso contrário, será um grande trabalho implementá-los na subclasse.

**Resposta #4**: É bom ter isso em mente ao escrever métodos de modelo. Às vezes, você pode fazer isso não tornando as etapas do seu algoritmo muito granulares. Mas é obviamente uma compensação: quanto menos granularidade, menos flexibilidade.
Lembre-se também de que algumas etapas serão opcionais, portanto você pode implementá-las como ganchos em vez de métodos abstratos, aliviando a carga das subclasses de sua classe abstrata.

---
---

## Um pouco de formalidade...

## Padrão `Template Method` (325)

### Objetivo

Permitir a definição do esqueleto de um algoritmo em uma classe abstrata e deixar que as subclasses implementem os passos específicos desse algoritmo.

### Características

Algumas características principais desse padrão são:

* Evita a duplicação de código, pois as partes comuns do algoritmo são colocadas na superclasse, enquanto as partes variáveis são delegadas às subclasses.

* Facilita a extensão do algoritmo, pois basta criar uma nova subclasse e implementar os métodos abstratos que representam os passos do algoritmo.

* Permite controlar a estrutura do algoritmo na superclasse, impedindo que as subclasses alterem ou ignorem algum passo importante.

* Pode usar métodos concretos, abstratos ou _hooks_ (ganchos) na superclasse. Os métodos concretos são aqueles que já têm uma implementação padrão. Os métodos abstratos são aqueles que devem ser obrigatoriamente implementados pelas subclasses. Os métodos **ganchos** são aqueles que podem ser sobrescritos pelas subclasses para adicionar algum comportamento opcional.


### Aplicações (casos de uso)

#### 1. Implementação de um algoritmo com passos específicos:

O `Template Method` é adequado quando você tem um algoritmo que segue uma sequência de etapas, mas algumas dessas etapas podem variar de uma classe derivada para outra. O padrão permite definir a estrutura geral do algoritmo na classe base e delegar a implementação de etapas específicas para as subclasses. Isso promove a reutilização de código e mantém a consistência na estrutura do algoritmo.

#### 2. Frameworks e Bibliotecas:

É comumente usado em frameworks e bibliotecas para fornecer uma estrutura básica que pode ser estendida ou personalizada por desenvolvedores. Por exemplo, em um framework de construção de interfaces gráficas, a classe base pode fornecer um método de renderização genérico, enquanto as subclasses podem implementar a renderização específica para diferentes tipos de componentes.

#### 3. Processamento em lote:

Quando você está lidando com processamento em lote, como processamento de dados em lote, o `Template Method` pode ser útil. A classe base pode definir um fluxo geral de processamento, enquanto as subclasses podem fornecer implementações específicas de etapas de processamento, como leitura de dados, transformação e gravação.

#### 4. Jogos e simulações:

Jogos e simulações muitas vezes envolvem personagens ou elementos que seguem um conjunto de ações predefinidas, mas com variações específicas. O padrão `Template Method` pode ser usado para definir o comportamento geral dos personagens ou elementos do jogo, enquanto as subclasses implementam ações específicas para cada personagem ou elemento.

#### 5. Construção de documentos:

Na construção de documentos, como documentos **HTML** ou **XML**, o `Template Method` pode ser aplicado. A classe base pode definir a estrutura geral do documento, como cabeçalho e rodapé, enquanto as subclasses podem preencher o conteúdo específico do documento.

#### 6. Processamento de pedidos em sistemas de comércio eletrônico:

Em sistemas de comércio eletrônico, o processamento de pedidos segue um conjunto de etapas comuns, como verificação de estoque, cálculo de custos e geração de fatura. O `Template Method` pode ser usado para definir a estrutura geral do processamento de pedidos, com subclasses implementando as etapas específicas para diferentes tipos de produtos ou serviços.

Em suma, este padrão é útil sempre que você tem um algoritmo com uma estrutura fixa, mas com partes que podem variar de uma implementação para outra. Adicionalmente, ele ajuda a promover a reutilização de código, a manutenção e a extensibilidade de sistemas orientados a objetos.


### Estrutura Básica

![diagram de classe factory method](../img_readme/diagrama_classe_template_method.png)

> A descrição da **Estrutura Básica** segue abaixo.
> 
> Temos a `AbstractClass`: define as operações ou passos de um algoritmo com a ajuda de métodos abstratos. Esses passos são substituídos por subclasses concretas.
> 
> Temos também a `ConcreteClass`: implementa os passos (conforme definidos pelos métodos abstratos) para executar aqueles que são específicos da subclasse do algoritmo.
> 
> E por último, temos o `TemplateOperation()`: define o esqueleto do algoritmo. Múltiplos passos definidos por métodos abstratos são chamados nesse método para definir a sequência ou o próprio algoritmo.


### Participantes

* `AbstractClass` (**Aplicação**)
	* Define **operações primitivas** abstratas que subclasses concretas definem para implementar os passos de um algoritmo.
	* Implementa um método modelo (_template_) que define o esqueleto de um algoritmo. Este método chama operações primitivas, bem como operações definidas em `AbstractClass` ou de outros objetos.

* `ConcreteClass` (**Minha aplicação**)
	* Implementa as operações primitivas para realizar passos específicos da subclasse do algoritmo.


###Colaborações

* `ConcreteClass` depende de `AbstractClass` para implementar os passos invariantes do algoritmo.


### Exemplos de Código

#### Exemplo #1: Criação de um jogo de estratégia simples baseado em IA (extraído do livro "Dive into Design Patterns de Alexander Shvetz").

Observe o diagrama de classes abaixo que ilustra um "esqueleto" que o padrão `Template Method` fornece para várias ramificações de IA em um jogo de estratégia.

![ex 01 template method](../img_readme/classe_template_method_ex01.png)

Todas as raças (i.e. Orcs, Monstros) do jogo tem quase o mesmo tipo de unidades e construções. Portanto você pode reutilizar a mesma estrutura de IA para várias raças, enquanto é capaz de sobrescrever alguns dos detalhes. Com essa abordagem, você pode sobrescrever a IA dos Orcs para torná-la mais agressiva, fazer os humanos mais orientados a defesa e fazer os monstros serem incapazes de construir qualquer coisa. Adicionando uma nova raça ao jogo irá necessitar a criação de uma nova subclasse IA e a sobrescrição dos métodos padrão declarados na classe IA base.


O código ficaria assim.

```python
from abc import ABC, abstractmethod

# A classe abstrata define um método padrão que contém um
# esqueleto de algum algoritmo composto de chamadas, geralmente
# para operações abstratas primitivas. Subclasses concretas
# implementam essas operações, mas deixam o método padrão em si
# intacto.
class GameAI(ABC):
    # O método padrão define o esqueleto de um algoritmo.
    def turn(self):
        self.collectResources()
        self.buildStructures()
        self.buildUnits()
        self.attack()

    # Algumas das etapas serão implementadas diretamente na
    # classe base.
    def collectResources(self):
        for s in self.builtStructures:
            s.collect()

    # E algumas delas podem ser definidas como abstratas.
    @abstractmethod
    def buildStructures(self):
        pass

    @abstractmethod
    def buildUnits(self):
        pass

    # Uma classe pode ter vários métodos padrão.
    def attack(self):
        enemy = self.closestEnemy()
        if enemy is None:
            self.sendScouts(self.map.center)
        else:
            self.sendWarriors(enemy.position)

    @abstractmethod
    def sendScouts(self, position):
        pass

    @abstractmethod
    def sendWarriors(self, position):
        pass

# Classes concretas têm que implementar todas as operações
# abstratas da classe base, mas não podem sobrescrever o método
# padrão em si.
class OrcsAI(GameAI):
    def buildStructures(self):
        if self.has_resources():
            # Construir fazendas, depois quartéis, e então uma
            # fortaleza.
            pass

    def buildUnits(self):
        if self.has_resources():
            if not self.has_scouts():
                # Construir peão, adicionar ele ao grupo de
                # scouts (batedores).
                pass
            else:
                # Construir um bruto, adicionar ele ao grupo
                # dos guerreiros.
                pass

    # ...

    def sendScouts(self, position):
        if self.scouts_count() > 0:
            # Enviar batedores para posição.
            pass

    def sendWarriors(self, position):
        if self.warriors_count() > 5:
            # Enviar guerreiros para posição.
            pass

# As subclasses também podem sobrescrever algumas operações com
# uma implementação padrão.
class MonstersAI(GameAI):
    def collectResources(self):
        # Monstros não coletam recursos.
        pass

    def buildStructures(self):
        # Monstros não constroem estruturas.
        pass

    def buildUnits(self):
        # Monstros não constroem unidades.
        pass
```

---

#### Exemplo #2: Jogo: Cenário de uma agência de viagens (extraído do livro "Learning Python Design Patterns de Chetan Giridhar")

Imagine o caso de uma agência de viagens, digamos, Dev Travels. Agora, como eles normalmente funcionam? Eles definem várias viagens para vários locais e elaboram um pacote de férias para você. Um pacote é essencialmente uma viagem que você, como cliente, realiza. Uma viagem possui detalhes como os locais visitados, o transporte utilizado e outros fatores que definem o roteiro da viagem. Essa mesma viagem pode ser customizada de forma diferenciada de acordo com as necessidades dos clientes. 

Considerações sobre o desenvolvimento. Temos algumas classes representam a classe concreta:

* Neste caso, temos duas classes concretas principais – `VeniceTrip` e `MaldivesTrip` – que implementa a classe abstrata `Trip`
* Estas classes concretas representam duas viagens diferentes feitas pelos turistas com base em sua escolha e interesses:
	* `VeniceTrip` e `MaldivesTrip` implementam `setTransport()`, `day1()`, `day2()`, `day3()` e `returnHome()`.

O código ficaria assim:

```python
from abc import ABC, abstractmethod
   
class Trip(ABC):
    
  @abstractmethod
  def setTransport(self):
    pass

  @abstractmethod
  def day1(self):
    pass

  @abstractmethod
  def day2(self):
    pass

  @abstractmethod
  def day3(self):
    pass

  @abstractmethod
  def returnHome(self):
    pass
      
  def itinerary(self):
    self.setTransport()
    self.day1()
    self.day2()
    self.day3()
    self.returnHome()


class VeniceTrip(Trip):
  
  def setTransport(self):
    print("Take a boat and find your way in the Grand Canal")
  
  def day1(self):
    print("Visit St Mark's Basilica in St Mark's Square")
  
  def day2(self):
    print("Appreciate Doge's Palace")
  
  def day3(self):
    print("Enjoy the food near the Rialto Bridge")
  
  def returnHome(self):
    print("Get souvenirs for friends and get back")


class MaldivesTrip(Trip):
  
  def setTransport(self):
    print("On foot, on any island, Wow!")

  def day1(self):
      print("Enjoy the marine life of Banana Reef")
  
  def day2(self):
      print("Go for the water sports and snorkelling")
  
  def day3(self):
      print("Relax on the beach and enjoy the sun")
  
  def returnHome(self):
      print("Dont feel like leaving the beach..")


#implementação da Dev Travel Agency
class TravelAgency:
  def arrange_trip(self):
    choice = input("What kind of place you'd like to go historical or to a beach?")
    if choice == 'historical':
      self.trip = VeniceTrip()
      self.trip.itinerary()
    if choice == 'beach':
      self.trip = MaldivesTrip()
      self.trip.itinerary()


TravelAgency().arrange_trip()
```

---

#### Exemplo #3: Usando um DVD Player

Um DVD Player pode ler CDs, DVDs e Blue-Rays. Aparentemente, a lógica `play()` para cada fonte de mídia é a mesma: ler → modular → saída.

Mas a parte lida (i.e. `play()`) pode variar de acordo com diferentes fontes de mídia. Esta variação pode ser definida dentro da subclasse específica da fonte de mídia. A figura abaixo ilustra o processo de funcionamento.

![ex03 dvd player example](../img_readme/dvd_player_example_ex03.webp)

A estrutura do projeto usando o padrão `Template Method` ficaria assim. Observe que a figura mostra o desenvolvimento feito em linugagem Java. Porém, vamos implementar em Python.

![ex03 project structure](../img_readme/project_structure_ex03.webp)

O código ficaria assim:

```python
from abc import ABC, abstractmethod

# This is an abstract base class
class MediaDisk(ABC):
    @abstractmethod
    def readBytes(self):
        pass

    @abstractmethod
    def modulateBytes(self):
        pass

    def play(self):
        self.readBytes()
        self.modulateBytes()
        self.output()

    def output(self):
        print("Convert Bytes to Sound")


# Inheriting from the abstract base class
class DVDMediaDisk(MediaDisk):
    def readBytes(self):
        # Read bytes from DVD (specific to DVD)
        pass

    def modulateBytes(self):
        # Modulation constants specific to DVD
        # Quality differences
        pass


# Inheriting from the abstract base class
class CDMediaDisk(MediaDisk):
    def readBytes(self):
        pass

    def modulateBytes(self):
        pass


# Main driver code
if __name__ == "__main__":
  md_driver = CDMediaDisk()
  md_driver.play()

  md_driver2 = DVDMediaDisk()
  md_driver2.play()
```
---

#### Exemplo #4: Algoritmo para construir uma casa.

As etapas (passos) que precisam ser executadas para construir uma casa são: construir fundações, construir pilares, construir paredes e janelas. O ponto importante é que não podemos alterar a ordem de execução porque não podemos construir janelas antes de construir a fundação. Portanto, neste caso podemos criar um `Template Method` que utilizará métodos diferentes para construir a casa. Agora, construir a fundação de uma casa é igual para todos os tipos de casas, seja uma casa de madeira ou uma casa de vidro. Portanto, podemos fornecer uma implementação básica para isso, se as subclasses quiserem substituir esse método, elas podem, mas principalmente é comum para todos os tipos de casas. O diagrama de classes que representa este exemplo está na figura abaixo.


![template method ex04](../img_readme/classe_template_method_ex04.png)

O código ficaria assim:

```python
from abc import ABC, abstractmethod

class Plan(ABC):
    def __init__(self):
        self.rate = 0.0

    @abstractmethod
    def calculate_bill(self, units):
        pass

    @abstractmethod
    def get_rate(self):
        pass

class DomesticPlan(Plan):
    def get_rate(self):
        self.rate = 3.50

    def calculate_bill(self, units):
        print(units * self.rate)

class CommercialPlan(Plan):
    def get_rate(self):
        self.rate = 7.50

    def calculate_bill(self, units):
        print(units * self.rate)

class InstitutionalPlan(Plan):
    def get_rate(self):
        self.rate = 5.50

    def calculate_bill(self, units):
        print(units * self.rate)

class GetPlanFactory:
    def get_plan(self, plan_type):
        if plan_type is None:
            return None
        if plan_type.upper() == "DOMESTICPLAN":
            return DomesticPlan()
        elif plan_type.upper() == "COMMERCIALPLAN":
            return CommercialPlan()
        elif plan_type.upper() == "INSTITUTIONALPLAN":
            return InstitutionalPlan()
        return None

class GenerateBill:
    def main(self):
        plan_factory = GetPlanFactory()

        plan_name = input("Enter the name of plan for which the bill will be generated: ")
        units = int(input("Enter the number of units for which bill will be calculated: "))

        plan = plan_factory.get_plan(plan_name)
        if plan:
            print(f"Bill amount for {plan_name} of {units} units is:", end=" ")
            plan.get_rate()
            plan.calculate_bill(units)

if __name__ == "__main__":
    bill_generator = GenerateBill()
    bill_generator.main()
```
---

#### Exemplo #5: Exemplo na rotina diária de um funcionário.

Observe a figura abaixo.

![template method ex05](../img_readme/classe_template_method_ex05.png)

Pode-se ver que algumas atividades de alguns trabalhadores são iguais, outras não. Neste exemplo, é uma boa ideia usar o `Template Method`.

O código fica assim.

```python
from abc import ABC, abstractmethod

class Worker(ABC):
    def goToWork(self):
        print("Go to work at eight a.m")

    def work(self):
        print("Work for eight hours")

    def returnToHome(self):
        print("Return from work at sixteen p.m")

    @abstractmethod
    def getUp(self):
        pass

    @abstractmethod
    def eatBreakfast(self):
        pass

    @abstractmethod
    def relax(self):
        pass

    @abstractmethod
    def sleep(self):
        pass

    def DailyRoutine(self):
        self.goToWork()
        self.work()
        self.returnToHome()
        self.getUp()
        self.eatBreakfast()
        self.relax()
        self.sleep()
        print("")


class FireFighter(Worker):
    def getUp(self):
        print("Get up at five a.m")

    def eatBreakfast(self):
        print("Eat breakfast at six a.m")

    def relax(self):
        print("Take a break at eight p.m")

    def sleep(self):
        print("Go sleep at twelve p.m")


class Lumberjack(Worker):
    def getUp(self):
        print("Get up at half past seven a.m. Flax...")

    def eatBreakfast(self):
        print("Eat during work...")

    def relax(self):
        print("Take a break at sixteen p.m. Not very ambitious...")

    def sleep(self):
        print("Go sleep at eight p.m")


class Manager(Worker):
    def getUp(self):
        print("Get up at four a.m. Ambitious :)")

    def eatBreakfast(self):
        print("Eat breakfast at six a.m")

    def relax(self):
        print("Take a break at ten p.m. Busy bee :)")

    def sleep(self):
        print("Go sleep at midnight")


class Postman(Worker):
    def getUp(self):
        print("Get up at six a.m")

    def eatBreakfast(self):
        print("Eat breakfast at seven a.m")

    def relax(self):
        print("Take a break at half past sixteen p.m")

    def sleep(self):
        print("Go sleep at eleven p.m")


#testando o código
if __name__ == "__main__":
    print("FireFighter")
    firefighter = FireFighter()
    firefighter.DailyRoutine()

    print("Lumberjack")
    lumberjack = Lumberjack()
    lumberjack.DailyRoutine()

    print("Manager")
    manager = Manager()
    manager.DailyRoutine()

    print("Postman")
    postman = Postman()
    postman.DailyRoutine()
```
