# Programação Orientada a Objetos (POO) em Python

## 1. Fundamentos e Os Quatro Pilares da POO

A Programação Orientada a Objetos é um paradigma que organiza o software em torno de objetos que combinam dados (atributos) e comportamentos (métodos). Os quatro pilares fundamentais são:

* **Encapsulamento:** Agrupamento de dados e comportamentos em uma classe, controlando o acesso ao estado interno. Em Python, utiliza-se convenções como `_atributo` (protegido por convenção) ou `__atributo` (que ativa o *name mangling* para ocultação).
* **Herança:** Mecanismo que permite criar relações hierárquicas, onde uma classe filha herda atributos e métodos de uma classe pai, promovendo o reuso de código.
* **Abstração:** Isolamento da interface conceitual de seus detalhes concretos de implementação. Define o *quê* o objeto faz, postergando o *como*, formalizada em Python através de Classes Base Abstratas (`abc`).
* **Polimorfismo:** Capacidade de tratar objetos de diferentes tipos de maneira uniforme através de uma interface ou comportamento comum.

---

## 2. Classes, Instâncias e Atributos

* **Classe vs. Instância:** Uma classe atua como um modelo estrutural (um molde), enquanto a instância é o objeto concreto construído a partir desse modelo.
* **O parâmetro `self`:** Representa a instância atual que está executando o método. Ele é passado implicitamente pelo interpretador Python no momento da chamada.
* **Método Construtor (`__init__`):** Responsável por inicializar os atributos de instância logo após a criação do objeto.
* **Atributos de Classe vs. Instância:** Atributos de classe possuem o mesmo valor para todas as instâncias (definidos diretamente no corpo da classe), enquanto atributos de instância variam para cada objeto individualmente.

---

## 3. Herança, Sobrescrita e o uso de `super()`

* **Hierarquia "É-um":** A herança modela relações taxonômicas (ex: um `Gerente` é um `Funcionario`).
* **Sobrescrita de Métodos (Override):** Uma classe filha pode redefinir um método herdado da classe pai para especializar seu comportamento.
* **A função `super()`:** Retorna um proxy para acessar membros da classe pai. É fundamental em hierarquias cooperativas para reaproveitar a lógica do construtor ou de métodos herdados sem duplicar código:

```python
class Subclasse(Superclasse):
    def __init__(self, argumento):
        super().__init__(argumento)
```

---

## 4. Classes Abstratas (`abc`)

O módulo nativo `abc` permite estabelecer contratos rígidos que as classes filhas são obrigadas a cumprir:

* Uma classe com métodos decorados com `@abstractmethod` não pode ser instanciada diretamente.
* Qualquer subclasse concreta deve implementar obrigatoriamente todos os métodos abstratos definidos na base, sob pena de levantar um erro (`TypeError`) em tempo de execução.

---

## 5. Dicas

1. **Argumentos mutáveis como valores padrão:** Utilizar listas ou dicionários diretamente na assinatura do construtor (ex: `def __init__(self, lista=[])`) faz com que o objeto seja compartilhado entre todas as instâncias. O correto é inicializar com `None` e instanciar internamente:
   ```python
   self.lista = [] if lista is None else list(lista)
   ```
2. **Uso incorreto de `super()`:** Chamar diretamente o nome da classe pai (`Funcionario.__init__(self)`) em vez de `super().__init__()` quebra a flexibilidade da MRO (*Method Resolution Order*) em hierarquias complexas.
3. **Violação do Princípio de Substituição de Liskov (LSP):** Modificar a assinatura de um método herdado na classe filha de forma incompatível com o contrato original introduz erros severos de execução.

---

## 6. Lista de Exercícios Recomendados para Treinamento

Para fixar o conteúdo e se preparar para as questões práticas da avaliação, resolva os seguintes desafios práticos por conta própria:

1. **Hierarquia de Animais:** Implemente uma classe base abstrata `Animal` com um método abstrato `emitir_som()`. Crie as classes concretas `Cachorro` e `Gato` com implementações polimórficas distintas.
2. **Sistema de Gestão de Pedidos:** Crie uma classe `Pedido` que valide itens e calcule o subtotal, aplicando diferentes estratégias de desconto por meio de composição.
3. **Rede de Notificações:** Desenvolva uma hierarquia de notificações utilizando uma classe abstrata `Notificador` com subclasses concretas `Email`, `SMS` e `Push`.
4. **Simulação de Pagamentos com Contrato:** Modele um sistema de checkout utilizando uma classe abstrata `GatewayPagamento` com o método `autorizar(valor)` e implemente duas formas de pagamento distintas.