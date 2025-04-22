# Flutter Mason Bricks Doc

- Antes de começar é importante fazer todo o [setup do flutter](https://docs.flutter.dev/get-started/install) pois sem o dart-sdk não é possível utilizar o mason.

## Setup

Você pode consultar a [doc oficial](https://docs.brickhub.dev/) caso ache necessário porém aqui ta um passo a passo do que devemos fazer para utilizar o mason da melhor forma possivel.</br>
Para utilizar o mason você deve ativar o mason_cli no seu sistema através do comando:

```
# 🎯 Activate from https://pub.dev
dart pub global activate mason_cli
```

Após isso feito você pode entrar no diretório onde seus projetos estão armazenados e rodar um:

```
mason init
```

📁Ops é importante rodar isso na pasta onde ficam seus projetos e não na pasta do projeto em si para não subir arquivos desnecessários no repositório do seu projeto.

## Adicionando bricks

Após isso feito será gerado um arquivo `mason.yaml` com a seguinte configuração:

```
# Register bricks which can be consumed via the Mason CLI.
# https://github.com/felangel/mason
bricks:
  # Sample Brick
  # Run `mason make hello` to try it out.
  hello: 0.1.0+1
  # Bricks can also be imported via git url.
  # Uncomment the following lines to import
  # a brick from a remote git url.
  # widget:
  #   git:
  #     url: https://github.com/felangel/mason.git
  #     path: bricks/widget
```

Você pode rodar um `mason remove hello` para limpar esses comentários e a brick hello que não iremos utilizar.

Agora com seu `mason.yaml` limpo podemos começar importar as bricks que vamos de fato utilizar.

Existem duas formas de você adicionar bricks em seu projeto, se a brick que você for utilizar estiver publicada no [brickhub](https://brickhub.dev/) você pode rodar o seguinte comando:

```
mason add $brick_name
```

Porém se ainda não estiver publicado você pode adicionar bricks locais clonando nosso repositório e adicionando o path no `mason.yaml` desse modo:

```
bricks:
  hello: 0.1.0+1
  $brick_name:
    path: "flutter-mason-bricks\\$brick_name"
```

Depois rode o comando abaixo para que sua brick possa ser utilizada:
```
mason upgrade
```

Rode o comando abaixo para verificar se a brick está disponível no computador:
```
mason list
```

O retorno deve ser algo assim:
```
/$MASON.YAML/$PATH/
└── $NOME_DA_BRICK 0.0.1+1 -> /$PATH/$DA/$BRICK/
```

Com as bricks adicionadas para utilizar basta rodar o comando:

```
mason make brick_name
```

Caso queira especificar em qual pasta deva gerar sua brick basta passar o atributo `-o` e o path que gostaria que a brick fosse gerada por exemplo:

```
mason make brick_name -o lib/features/
```

## Criando // dando manutenção em uma brick:

Quando você cria e da manutenção nas bricks a tendencia é aparecer muitos erros de código devido ao analyzer do VS code para evitar isso adicionamos um arquivo chamado `analysis_options.yaml` com a seguinte configuração:

```
analyzer:
  exclude:
    - brick_name1
    - brick_name2
```

## Publicando uma brick ou atualizando bricks existentes:

É necessário ter acesso a uma conta do brickhub que pode ser criada através do [formulario](https://docs.google.com/forms/d/e/1FAIpQLSf2DCJuskMuOmXFyeL5VBoW4oGVB27XHQGtaSmJRhW_ebDP1g/viewform) disponibilizado na [site oficial](https://brickhub.dev/).

Para publicar uma brick você deve fazer o login com o comando
```bash
$ mason login
```
após isso o mason ira pedir as crendenciais e após logado basta rodar um:

```bash
$ mason publish --directory /diretorio_da_brick
```
