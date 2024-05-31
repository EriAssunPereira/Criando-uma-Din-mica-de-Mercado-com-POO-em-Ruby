# Criando-uma-Dinâmica-de-Mercado-com-POO-em-Ruby

Criando uma dinâmica de mercado usando Programação Orientada a Objetos (POO) em Ruby. Vamos dividir o código em três arquivos principais, representando diferentes módulos do nosso sistema de mercado: `Produto`, `Carrinho` e `Mercado`.

### Módulo Produto
Este módulo será responsável por criar e gerenciar os produtos disponíveis no mercado.

```ruby
module Produto
  class Item
    attr_accessor :nome, :preco

    def initialize(nome, preco)
      @nome = nome
      @preco = preco
    end
  end
end
```

### Módulo Carrinho
O módulo Carrinho gerenciará os itens que o usuário deseja comprar.

```ruby
module Carrinho
  class Compra
    attr_reader :itens

    def initialize
      @itens = []
    end

    def adicionar_item(item)
      itens << item
    end

    def total
      itens.sum(&:preco)
    end
  end
end
```

### Módulo Mercado
O módulo Mercado simulará a interação do usuário com o mercado, permitindo escolher e comprar produtos.

```ruby
module Mercado
  class Interface
    def initialize
      @carrinho = Carrinho::Compra.new
    end

    def escolher_produto(produto)
      @carrinho.adicionar_item(produto)
      puts "Você adicionou #{produto.nome} ao carrinho."
    end

    def checkout
      total = @carrinho.total
      puts "O total da sua compra é R$#{total}."
      # Aqui você pode adicionar mais lógica para pagamento, etc.
    end
  end
end
```

### Integração dos Módulos
Para integrar os módulos, você pode criar um arquivo separado que irá instanciar os objetos e simular a compra.

```ruby
require_relative 'produto'
require_relative 'carrinho'
require_relative 'mercado'

# Criação de produtos
banana = Produto::Item.new('Banana', 0.99)
maca = Produto::Item.new('Maçã', 1.50)

# Inicialização do mercado
mercado = Mercado::Interface.new

# Simulação do usuário escolhendo produtos
mercado.escolher_produto(banana)
mercado.escolher_produto(maca)

# Finalização da compra
mercado.checkout
```

Este exemplo é uma base simples para um sistema de mercado. Você pode expandir adicionando mais funcionalidades como gestão de estoque, promoções, e métodos de pagamento. Lembre-se de testar cada parte do código para garantir que tudo esteja funcionando como esperado.
