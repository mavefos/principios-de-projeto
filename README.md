# aplicaçao de princípios fundamentais de projeto de software, com base no modelo SOLID. 

# principios abordados 
1. SRP - Single Responsibility Principle
2. OCP - Open-Closed Principle
3. DIP - Dependency Inversion Principle
4. Composição em vez de Herança

### 1. SRP — Single Responsibility Principle 
o que é e para que serve? 
cada classe deve possuir uma única responsabilidade e um único motivo para modificaçao. o objetivo é reduzir acoplamento entre funcionalidades distintas.

**Exemplo:**

```python
class GeradorDeRelatorio:
    def gerar(self, dados):
        return f"Relatorio: {dados}"

class ImpressoraDeRelatorio:
    def imprimir(self, relatorio):
        print(relatorio)

dados = "vendas do mes"
relatorio = GeradorDeRelatorio().gerar(dados)
ImpressoraDeRelatorio().imprimir(relatorio
```
no código, cada classe possui uma única responsabilidade, gerar ou imprimir. SRP se aplica pois as responsabilidades estao separadas.

### 2. OCP — Open-Closed Principle 
o que é e para que serve? 
entidades de software precisam estar abertas para extensao e fechadas para modificaçao. o objetivo é permitir assim a adiçao de novos elementos sem alterar 
o código existente. 

**Exemplo:**

```python
class Desconto:
    def calcular(self, valor):
        return valor

class DescontoClienteVip(Desconto):
    def calcular(self, valor):
        return valor * 0.9

class Carrinho:
    def __init__(self, desconto):
        self.desconto = desconto

    def total(self, valor):
        return self.desconto.calcular(valor)

vip = Carrinho(DescontoClienteVip())
print(vip.total(100))
````
nesse caso, carrinho está fechado para modificaçao, mas pode ser estendido. o OCP é aplicado justamente por permitir essa mudança sem que altere a lógica existente.


### 3. DIP — Dependency Inversion Principle
o que é e para que serve? 
módulos, sejam eles de alto ou de baixo nível, devem depender de abstraçoes
o objetivo é reduzir o acoplamento entre esses componentes e aumentar a flexibilidade do sistema

**Exemplo:**

```python
from abc import ABC, abstractmethod

class INotificador(ABC):
    @abstractmethod
    def enviar(self, mensagem):
        pass

class NotificadorEmail(INotificador):
    def enviar(self, mensagem):
        print(f"Enviando email: {mensagem}")

class Pedido:
    def __init__(self, notificador: INotificador):
        self.notificador = notificador

    def finalizar(self):
        self.notificador.enviar("Pedido finalizado!")

notificador = NotificadorEmail()
pedido = Pedido(notificador)
pedido.finalizar()

````
pedido depende da abstraçao INotificador, não da implementação concreta. o DIP é aplicado ao separar alto nível (Pedido) e baixo nível (NotificadorEmail) por meio de uma interface.

### 4. Composição em vez de Herança
o que é e para que serve? 
essa composiçao consiste em construir funcionalidades combinando objetos, para nao estender classes. o objetivo é promover o menor acoplamento, maior reutilizaçao e 
mais flexibilidade. 

**Exemplo:** 
```python
class Motor:
    def ligar(self):
        print("Motor ligado.")

class Carro:
    def __init__(self):
        self.motor = Motor()

    def ligar(self):
        self.motor.ligar()
        print("Carro ligado.")

carro = Carro()
carro.ligar()
````
o princípio é aplicado ao usar composiçao para reaproveitar comportamentos sem herança direta. carro nao está herdando motor



















