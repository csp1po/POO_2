# Bem-vindos ao mundo dos Design Patterns (*Padrões de Projeto*) Orientados a Objeto✨✨

### _Alguém resolveu seus problemas!!!_

![Casal Objetolandia](../img_readme/casal_objetoville_39.png)

---

> **Vamos aprender por que (e como) a gente pode explorar a sabedoria e as lições aprendidas por outros desenvolvedores que passaram pelo mesmo problema em termos de Design e sobreviveram à viagem.**
> 
> **Veremos o uso e os benefícios dos *Design Patterns*, alguns princípios-chave do Design Orientado a Objetos (OO) e um exemplo de como um padrão funciona.**

---


## Tudo começou com um simples aplicativo chamado _SimUDuck_


Joe trabalha para uma empresa que faz um jogo de simulação de lago com patos de grande sucesso, conhecido por `SimUDuck`. O jogo pode mostrar uma grande variedade de espécies de patos nadando e fazendo sons que imitam seus grasnados. Os projetistas iniciais do sistema usaram técnicas OO padrão e criaram uma superclasse chamda `Duck` da qual todos os outros tipos de pato herdam. Veja o diagrama de classes abaixo.

![SimDuck App](../img_readme/sim_duck_app_40.png)

> **Observação**: no ano passado, a empresa esteve sob crescente pressão dos concorrentes. Depois de uma sessão de brainstorming  jogando golfe por alguns dias, os executivos da empresa acham que é hora de uma grande inovação. Eles precisam de algo realmente impressionante para mostrar na próxima reunião de acionistas em Maui na próxima semana.

## Agora precisamos que os patos voem!!

Os executivos decidiram que patos "voadores" é exatamente o que o simulador precisa para surpreender os concorrentes. E, claro, o gerente disse a eles que não haveria problema para o Joe preparar algo em uma semana. “Afinal”, disse o chefe do Joe, “ele é um programador OO... e, _quão difícil isto pode ser?_".

![OO Genius](../img_readme/joe_OO_genius_41.png)

> Joe fez assim (veja a figura abaixo).

![Other Duck Types](../img_readme/others_duck_types_41.png)

---

## Mas alguma coisa deu muito errado!!!!

![Algo deu errado](../img_readme/algo_deu_errado_42.png)


###O que aconteceu?

* Joe não percebeu que nem todas as subclasses de ``Duck`` deveriam voar. Quando ele adicionou um novo comportamento à superclasse ``Duck``, ele também incluiu um comportamento que não era apropriado para algumas das subclasses. Ele agora tem objetos inanimados voadores no programa ``SimUDuck``.

* O que ele pensou que fosse um excelente uso de herança para fins de _reutilização_ não dá tão certo quando se trata de _manutenção_.

* Nem todas as subclasses de ``Duck`` deveriam voar.

* Uma atualização localizada no código causou um efeito colateral não-local (patos de borracha voadores!!). Veja a figura abaixo.

![pato borracha não voa](../img_readme/pato_borracha_nao_voa_42.png)

###Joe pensa em Herança

![Pensando sobre herança](../img_readme/pensando_sobre_heranca_43.png)

---
## Que tal uma Interface? - PARTE 1

> Joe percebeu que a herança provavelmente não era a resposta, porque ele acabou de receber um memorando dizendo que os executivos agora querem atualizar o produto a cada seis meses (de maneiras que ainda não decidiram). Joe sabe que a especificação continuará mudando e ele será forçado a examinar e possivelmente substituir `fly()` e `quack()` para cada nova subclasse `Duck` que já foi adicionada ao programa... para sempre. Portanto, ele precisa de uma maneira mais limpa de fazer com que apenas alguns (mas não todos) dos tipos de pato voem ou grasnem. Veja a figura abaixo.

![Que tal uma interface](../img_readme/how_about_an_interface_44.png)

## Que tal uma Interface? - PARTE 2

1. Nem todas as subclasses devem ter o comportamento de voar ou grasnar

2. Fazer subclasses implementar `Flyable` e/ou `Quackable` resolve parte do problema mas...
	* Destrói completamente a reutilização de código para esses comportamentos;

	* Pode haver mais um tipo de comportamento de voo até entre os patos que voam.


## O que você pensa sobre este projeto (design)?

![Ideia mais absurda](../img_readme/ideia_mais_absurda_45.png)

##O que você faria se fosse o Joe??

Sabemos que nem todas as subclasses devem ter comportamento de voar ou grasnar, então **herança** não é a resposta certa. Mas, embora ter as subclasses implementando `Flyable` e/ou `Quackable` resolva parte do problema (sem patos de borracha que voam inadequados), ele destrói completamente a reutilização de código para esses comportamentos, criando apenas um pesadelo de manutenção *diferente*. E é claro que pode haver mais de um tipo de comportamento de voo, mesmo entre os patos que voam...
Neste ponto, você pode estar esperando que um **Design Pattern** chegue montado em um cavalo branco e salve o dia. Mas que graça isso teria? **Não**, vamos descobrir uma solução à moda antiga - **aplicando bons princípios de Design de Software Orientado a Objeto**.

![Seria um sonho](../img_readme/seria_um_sonho_45.png)

****

##IMPORTANTE. NUNCA ESQUEÇA:

##Não importa o quão bem você projete um aplicativo, ao longo do tempo ele deve crescer e mudar ou morrerá.


###Então, como resolver o problema?

Qual a única coisa que podemos contar sempre no desenvolvimento de software???

> **ALTERAÇÃO!!!**

###Considerações:

* Herança não funcionou muito bem

* Nem todas as subclasses possuem o mesmo comportamento

* A ideia  da Interface pareceu promissora, mas classes de interface não possuem implementação, acabando com a reutilização

* Se o comportamento mudar, todas as subclasses onde esse comportamento é definido devem ser alteradas


Felizmente, existe um **Princípio de Design** para essa situação.


![Princípio de Design](../img_readme/principio_design_47.png)

> Em outras palavras, se você tem algum aspecto do seu código que está mudando, digamos a cada novo requisito, então você sabe que tem um comportamento que precisa ser retirado e separado de todas as coisas que não mudam.
> 
> Aqui está outra maneira de pensar sobre esse princípio: ***pegue as partes que variam e as encapsule, para que mais tarde você possa alterar ou estender as partes que variam sem afetar as que não variam***.
> 
> Por mais simples que seja esse conceito, ele forma a base para quase todos os Padrões de Projeto (_Design Patterns_). Todos os padrões fornecem uma maneira de *permitir que alguma parte de um sistema varie independentemente de todas as outras partes*.
> 
> Resumindo:
> 
> 1. Pegue o que varia e “encapsule” isto para que não afete o resto do seu código.
> 
> 2. O resultado? Menos consequências não intencionais de alterações de código e mais flexibilidade em seus sistemas!
> 

###Então, como resolver o problema?

Vamos tirar o comportamento do pato das classes ``Duck``!!

* Sabemos que ``fly()`` e ``quack()`` são as partes da classe ``Duck`` que variam entre os patos.

* Para separar esses comportamentos da classe ``Duck``, iremos tirar os dois métodos acima desta classe e criar um novo conjunto de classes para representar cada comportamento. Veja a figura abaixo.

![Duck Behaviors](../img_readme/duck_behaviors_48.png)

Isto significa que a partir de agora, os comportamentos de ``Duck`` ficarão em uma classe separada, ou seja, uma classe que implementa uma interface de comportamento. Assim, as classes de ``Duck`` não vão precisar conhecer nenhum detalhe de implementação para seus comportamentos.

Surge, então uma pergunta: como vamos criar um conjunto de classes que implementam os comportamentos ``fly`` e ``quack``?

Vamos usar um segundo **Princípio de Design**, como mostra a figura abaixo.

![Princípio de Design](../img_readme/principio_design_49.png)

Usaremos uma Interface para representar cada comportamento. Por exemplo, ``FlyBehavior`` e ``QuackBehavior``, e cada implementação de um comportamento implementará uma dessas interfaces. O diagrama de classes ficaria assim (veja figura abaixo).

![Flying Behavior](../img_readme/fly_behavior_49.png)

Com nosso novo design, as subclasses ``Duck`` usarão um comportamento representado por uma interface (``FlyBehavior`` e ``QuackBehavior``), de modo que a implementação real do comportamento não ficará preso à subclasse ``Duck``. Em outras palavras, o comportamento concreto específico é codificado na classe que implementa ``FlyBehavior`` ou ``QuackBehavior``.

Talvez você tenha a mesma pergunta que a moça da figura abaixo está fazendo.

![classe abstrata](../img_readme/classe_abstrata_50.png)

A resposta para esta pergunta é: "**Programar para uma interface” na verdade significa “Programar para um supertipo**".

A palavra _interface_ está sobrecarregada aqui. Assim sendo, explora-se o polimorfismo programando para um supertipo de modo que o objeto de tempo de execução real não fique preso ao código. E poderíamos reformular "programar para um supertipo" como "o tipo declarado das variáveis deve ser um supertipo, geralmente uma **classe abstrata**, de modo que os objetos atribuídos a essas variáveis possam ser de qualquer implementação concreta do supertipo, o que significa que a classe que os declara não precisa saber sobre os tipos de objetos reais".

Convém salientar de que o uso de interfaces em Python é frequentemente realizado através de classes abstratas, já que a linguagem não possui um mecanismo de interfaces nativas como algumas outras linguagens orientadas a objetos. No entanto, as classes abstratas podem ser usadas para definir contratos e garantir a implementação de determinados métodos em classes derivadas.

##Implementando os comportamentos da Classe ``Duck``

Observe a figura abaixo. Aqui temos as duas interfaces, ``FlyBehavior`` e ``QuackBehavior``, junto com as classes correspondentes que implementam cada comportamento concreto. Você poderia usar duas classes abstratas que o resultado seria o mesmo.

![implementing duck behaviors](../img_readme/implement_duck_behaviors_51.png)

> Com esse design, outros tipos de objetos podem reutilizar nossos comportamentos de voar e grasnar porque esses comportamentos não estão mais escondidos em nossas classes ``Duck``!

> E podemos adicionar novos comportamentos sem modificar nenhuma de nossas classes de comportamento existentes ou tocar em qualquer uma das classes ``Duck`` que usam comportamentos de voo.

##Visão Geral (Big Picture)

Na figura abaixo está toda a estrutura de classes reformulada. 

![Big Picture](../img_readme/big_picture_60.png)



Temos tudo o que você esperaria: patos estendendo ``Duck``, comportamentos ``fly`` implementando ``FlyBehavior`` e comportamentos ``quack`` implementando ``QuackBehavior``. 

Observe também que começamos a descrever as coisas de maneira um pouco diferente. Em vez de pensar nos comportamentos do pato como um *conjunto de comportamentos*, começaremos a pensar neles como uma *família de algoritmos*. Pense nisso: no design do ``SimUDuck``, os algoritmos representam coisas que um pato faria (diferentes formas de grasnar ou voar). 

###Observação:

A relação **HAS-A** (**TEM-UM**) é interessante: cada pato tem um ``FlyBehavior`` e um ``QuackBehavior`` ao qual delega para voar e grasnar.

Quando você coloca duas classes juntas dessa forma, você está usando **composição**. Em vez de herdar seu comportamento, os patos o obtêm vinculando-se ao objeto de comportamento correto. 

Esta é uma técnica importante. Na verdade, é a base do nosso terceiro princípio de design, o qual está representado na figura abaixo.

![Princípio de Design](../img_readme/principio_design_61.png)

A composição dá mais flexibilidade ao projeto. Ela permite encapsular uma família de algoritmos em seu próprio conjunto de classes e alterar o comportamento de um objeto em tempo de execução.

A composição é usada em muitos padrões de projeto e você verá muito mais sobre suas vantagens e desvantagens ao longo do curso.

## E por falar em Design Patterns (Padrões de Projeto)

![Primeiro Padrão de Projeto](../img_readme/primeiro_padrao_62.png)

Você acabou de aplicar seu primeiro padrão de projeto - o padrão **STRATEGY**. Isso mesmo, você usou o ``Strategy Pattern`` para reformular o aplicativo ``SimUDuck``.

Graças a esse padrão, o simulador está pronto para qualquer mudança que os executivos da empresa possam preparar em sua próxima viagem de negócios a Maui.

Agora que fizemos você percorrer o longo caminho para aprendê-lo, aqui está a definição formal desse padrão:

> O _Strategy Pattern_ define uma família de algoritmos, encapsula cada um deles e os torna intercambiáveis. A estratégia permite que o algoritmo varie independentemente dos clientes que o utilizam.

---
## Um pouco de formalidade...

Vimos várias definições de *Design Patterns*. Uma delas e: 
> Um padrão de projeto descreve um problema comum que ocorre regularmente no desenvolvimento de software e descreve uma solução geral para esses problemas que pode ser utilizada em muitos contextos diferentes.
> 
> Em geral, a solução é a descrição de um pequeno conjunto de classe e suas interações.
> 
> Em outras palavras: cada padrão encerra o conhecimento de uma pessoa muito experiente em um determinado assunto de uma forma que este conhecimento pode ser transmitido para outras pessoas menos experientes.

###Catálogo de Soluções

Desde 1995, a área de desenvolvimento de software passou a ter seu primeiro catálogo de soluções para projeto de software: o livro GoF (*Gang of Four*), como mostra a figura abaixo.

![Gang of Four Book](../img_readme/gang_of_four_book.webp)

###O Formato de Um Padrão no Livro GoF

1. **O Nome (inclui o número de página no livro)**
	* Um bom nome é essencial para que o padrão caia na boca do povo

2. **O Objetivo/Intenção**
	* 	Descreve quando aplicar o padrão
	*  Lista de condições que devem ser satisfeitas para que faça sentido aplicar o padrão

3. **Também conhecido como**

4. **Motivação**
	* Um cenário mostrando o problema e a necessidade da solução
  
5. **Aplicabilidade**
	* Como reconhecer as situações nas quais o padrão é aplicável 
	* Descreve elementos que compõem o projeto, seus relacionamentos, suas responsabilidades e colaborações

6. **Estrutura**
	* Representação gráfica da estrutura de classes (ainda não usava UML). Porém, atualmente encontra-se na Web tais diagramas.

7. **Participantes**
	* Classes e objetos que participam e quais são suas responsabilidades

8. **Colaborações**
	* Como as classes acima colaboram entre si

9. **Consequências**
	*  Vantagens, desvantagens, *trade-offs*

10. **Implementação**
	* Com quais detalhes devemos nos preocupar quando implementamos o padrão
	* Aspectos específicos de cada linguagem

11. **Exemplo de Código**
	* No caso do GoF, em C++ ou Smalltalk

12. **Usos Conhecidos**
	* Exemplos de sistemas reais de domínios diferentes onde o padrão é utilizado

13. **Padrões Relacionados**
	* Quais outros padrões devem ser usados em conjunto com este
	* Quais padrões são similares a este, e quais são as diferenças


Agora precisamos conhecer melhor em termos formais, o padrão exibido acima e que foi implementado pelo Joe no aplicativo ``SimUDuck``.

---

##Padrão Strategy (315)

###Objetivo
Definir uma família de algoritmos, encapsular cada um deles em uma classe e torná-los intercambiáveis. Ele permite que o algoritmo varie independentemente dos clientes que o utilizam.

###Características
* É uma forma de extrair da classe algo que pode mudar
* Clientes que necessitam de diferentes algoritmos que se tornam mais complexos se os incluírem em seu código
* Diferentes algoritmos são adequados em diferentes situações na resolução de um mesmo problema

###Aplicações (usos conhecidos)
* Verificação ortográfica multilíngue
* Separação silábica
* *Highlight* (Destaque/Realçe) de documentos no Emacs
* Algoritmos de ordenação
* Conectores de Banco de Dados

###Estrutura Básica

![Strategy Class Diagram](../img_readme/class_diagram_strategy.png)

> A descrição da **Estrutura Básica** segue abaixo.
> 
> Você tem contexto onde o contexto é o seu programa. O programa pode ser um videogame, por exemplo. Este programa precisa executar um algoritmo e esse algoritmo chama-se _Strategy_. Ou seja, uma estratégia para fazer alguma coisa.
> 
> Vamos supor que o videogame possa ter diferentes modos de jogo. Em outras palavras, diferentes estratégias de jogo.
> 
> Então, ao invés de ter a estratégia na própria classe principal do videogame, delega-se isso para uma outra classe, que é abstrata (por isso que está itálico), e daí vai-se ter subclasses que são as diferentes estratégias concretas que implementam essa classe abstrata de diferentes formas.
> 
> E daí, em tempo de execução, escolhe-se qual estratégia concreta que se quer usar. 


###Participantes

* **Strategy** 
	* Define uma interface comum para todos os algoritmos suportados
* **ConcreteStrategy** 
	* Implementa o algoritmo usando a interface de Strategy
* **Context**:
	* É configurado com um objeto **ConcreteStrategy**
	* Mantém uma referência para um objeto **Strategy**
	* Pode definir uma interface que permite a **Strategy** acessar seus dados

###Colaborações

* **Strategy** e **Context** interagem para implementar o algoritmo escolhido

* Os clientes usualmente criam e passam um objeto **ConcreteStrategy** para o contexto e passam a interagir diretamente com ele


### Exemplos de Código

#### Exemplo #1: Editor de Figuras

![Editor de Figuras](../img_readme/editor_figuras_diagrama_ex01.png)

Vamos supor que você tem editor de figuras (cria desenhos e figuras geométricas), por exemplo.

Porém, você quer gravar no disco a figura que você fez. Você podia ter o código que grava na própria classe principal chamada de ``EditorDeFiguras``. Mas este editor de figuras é uma coisa complexa, e se colocar tudo nessa classe principal você ia acabar com centenas de métodos, dentro dela e isso seria uma coisa muito ruim.

Então é aconselhável você pegar diferentes aspectos do ``EditorDeFiguras`` e extrair para uma classe separada, chamada de ``SalvadorDeFigura``. Observe que esta classe possui único método chamado ``Salve`` que recebe como parâmetro uma figura e ele vai salvá-la no disco de alguma forma.

Observe que existem três classes concretas que salvam diferentes formatos (i.e. **PDF**, **JPG**, **PNG**).

**Importante: existe um erro no diagrama. Os três métodos estão em itálico e não deveriam estar. Isto porque são métodos concretos.**

E então, cada método, teria algumas dezenas de linhas de código para salvar em PDF, e depois em JPG, e depois em PNG.

O interessante disso é que esses algoritmos específicos de gravar no disco diferentes formatos ficam totalmente separados da classe ``EditorDeFiguras``. 

Desta forma a nossa arquitetura fica muito melhor. Eu desenvolvi uma estratégia para salvar uma figura. 

---

#### Exemplo #2: Calculadora - Estratégia (Adição, Subtração) (extraído do livro "Easy Learning Design Patterns Python 3: Reusable Object-Oriented Software de Yang Hu")

![Calculadora](../img_readme/calculadora_diagrama_ex02.png)

O código ficaria assim:

```python
from abc import ABC, abstractmethod

############### Strategy #################
class Strategy(ABC):
    @abstractmethod
    def calculate(self, a, b):
        pass

############### Addition #################
class Addition(Strategy):
    def calculate(self, a, b):
        return a + b

############### Subtraction #############
class Subtraction(Strategy):
    def calculate(self, a, b):
        return a - b

############## Context ###################
class Context:
    def __init__(self, strategy):
        self.__strategy = strategy

    def do_calculate(self, a, b):
        return self.__strategy.calculate(a, b)

############### test #################
ctx = Context(Addition())
result = ctx.do_calculate(4, 2)
print("Addition: ", result)

ctx = Context(Subtraction())
result = ctx.do_calculate(4, 2)
print("Subtraction: ", result)

```

---

#### Exemplo #3: E-commerce escolhe diferentes bancos para pagar diferentes estratégias (extraído do livro "Easy Learning Design Patterns Python 3: Reusable Object-Oriented Software de Yang Hu")

![e-commerce](../img_readme/e-commerce_diagrama_ex03.png)

O código ficaria assim:

```python
from abc import ABC, abstractmethod

############### Pay (Abstract Class) #################
class Pay(ABC):
    @abstractmethod
    def pay(self, price):
        pass


############### MasterCard #################
class MasterCard(Pay):
    def pay(self, price):
        print("Pay", price, "$ by MasterCard")


############### Visa #################
class VisaCard(Pay):
    def pay(self, price):
        print("Pay", price, "$ by VisaCard")


############### Paypal #################
class Paypal(Pay):
    def pay(self, price):
        print("Pay", price, "$ by Paypal")


############### PayManager #################
class PayManager:
    __pay = None

    def __init__(self, pay):
        self.__pay = pay

    def do_pay(self, price):
        self.__pay.pay(price)


############### test #################
print("You need to pay $25 for the mobile phone")
code = int(input("Please select payment method 1: MasterCard 2: VisaCard 3: Paypal\n"))

payManager = None
if code == 1:
    payManager = PayManager(MasterCard())
elif code == 2:
    payManager = PayManager(VisaCard())
elif code == 3:
    payManager = PayManager(Paypal())

if payManager:
    payManager.do_pay(25)

```

---


#### Exemplo #4: Game Character(extraído do livro "Design Patterns in Python Common GOF (Gang of Four) Design Patterns implemented in Python de Sean Bradley")

![game character](../img_readme/game_character_diagrama_ex04.png)

O código ficaria assim:

```python
from abc import ABC, abstractmethod

class GameCharacter():
    # This is the context whose strategy will change
    @staticmethod
    def move(movement_style):
        # The movement algorithm has been decided by the client
        movement_style()

class IMove(ABC):
    # A Concrete Strategy Interface
    @abstractmethod
    def __call__(self):
        # Implementors must select the default method
        pass

class Walking(IMove):
    # A Concrete Strategy Subclass
    def __call__(self):
        # A walk algorithm
        print("I am Walking")

class Running(IMove):
    # A Concrete Strategy Subclass
    def __call__(self):
        # A run algorithm
        print("I am Running")

class Crawling(IMove):
    # A Concrete Strategy Subclass
    def __call__(self):
        # A crawl algorithm
        print("I am Crawling")

# The Client
GAME_CHARACTER = GameCharacter()
GAME_CHARACTER.move(Walking())
# Character sees the enemy
GAME_CHARACTER.move(Running())
# Character finds a small cave to hide in
GAME_CHARACTER.move(Crawling())

```

---

##Implementação do Projeto ``SimUDuck``

Para relembrar, segue a figura que representa o projeto.

![Big Picture](../img_readme/big_picture_60.png)


O código em Python está abaixo.


```python
from abc import ABC, abstractmethod

# Abstract FlyBehavior class
class FlyBehavior(ABC):
    @abstractmethod
    def fly(self):
        pass


# Concrete FlyBehavior implementations
class FlyNoWay(FlyBehavior):
    def fly(self):
        print("I can't fly")


class FlyWithWings(FlyBehavior):
    def fly(self):
        print("I'm flying!!")


# Abstract QuackBehavior class
class QuackBehavior(ABC):
    @abstractmethod
    def quack(self):
        pass


# Concrete QuackBehavior implementations
class Quack(QuackBehavior):
    def quack(self):
        print("Quack")


class Squeak(QuackBehavior):
    def quack(self):
        print("Squeak")


# Duck abstract class
class Duck:
    def __init__(self):
        self.fly_behavior = None
        self.quack_behavior = None

    def display(self):
        pass

    def perform_fly(self):
        self.fly_behavior.fly()

    def perform_quack(self):
        self.quack_behavior.quack()

    def swim(self):
        print("All ducks float, even decoys!")

    def set_fly_behavior(self, fb):
        self.fly_behavior = fb

    def set_quack_behavior(self, qb):
        self.quack_behavior = qb


# MallardDuck subclass
class MallardDuck(Duck):
    def __init__(self):
        super().__init__()
        self.quack_behavior = Quack()
        self.fly_behavior = FlyWithWings()

    def display(self):
        print("I'm a real Mallard duck")


# RubberDuck subclass
class RubberDuck(Duck):
    def __init__(self):
        super().__init__()
        self.fly_behavior = FlyNoWay()
        self.quack_behavior = Squeak()

    def display(self):
        print("I'm a Rubber Duck")


# DuckProject main class
if __name__ == "__main__":
    mallard = MallardDuck()
    mallard.display()
    mallard.perform_quack()
    mallard.perform_fly()
    mallard.set_fly_behavior(FlyNoWay())
    mallard.set_quack_behavior(Quack())
    mallard.display()
    mallard.perform_fly()
    mallard.perform_quack()

    rubber = RubberDuck()
    rubber.display()
    rubber.perform_fly()
    rubber.perform_quack()

```


