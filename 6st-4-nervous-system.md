### @diffs true
# Sistema Nervoso

## Passo 1
Neste tutorial, você irá utilizar o Micro:Bit para simular os sentidos humanos.
Usaremos o logotipo sensível ao toque para representar o tato, a matriz de LEDs
para a visão e o sensor de som para a audição. Cada um dos "sentidos" irá nos
retornar uma função diferente que o Micro:Bit é capaz de executar.

## Passo 2
Para a parte do código que representa o **tato** vamos utilizar o logotipo para mostrar 
uma mensagem. Primeiro, acesse a categoria ``||input:Input||`` e adicione o laço 
``||input:no logotipo pressionado||``. Em seguida, vá até a categoria ``||basic:Básico||``
e selecione os blocos ``||basic:mostrar string||`` e ``||basic:limpar tela||``. Posicione-os dentro do laço ``||input:no logotipo pressionado||``. 
Altere a escrita contida no espaço circular para uma de sua preferência. Essa mensagem será exibida quando 
o logotipo for tocado. 

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
```

## Passo 3
Para representar a **visão**, vamos utilizar a matriz de LEDs para ativar uma animação.
Primeiro, vá até a aba ``||basic:Básico||``e selecione o laço ``||basic:sempre||``, caso ele
não esteja na área de trabalho.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    }
})
```
## Passo 4 
Vá até a aba ``||logic:Lógica||`` e selecione o bloco condicional ``||logic:se-então||``
e posicione-o dentro do laço ``||basic:sempre||``.

```blocks
basic.forever(function () {
    if (true) {
    }	
})
```

## Passo 5 
Retorne à aba ``||logic:Lógica||`` e selecione o bloco triangular comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do laço 
``||logic:se-então||``, substituindo a palavra ``||logic:verdadeiro||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    if (0 == 0) {
    }	
})
```

## Passo 6
Agora, acesse a aba ``||input:Input||``, clique em ``||input:nível de luz||`` e
use-o para substituir o primeiro **0**.
Altere o segundo **0** para **200** e o sinal de ``||logic:=||`` para ``||logic:>||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
    }
})
```

## Passo 7
Agora, iremos criar uma animação para responder ao ``||input:nível de luz||``. 
Para isso, acesse a aba ``||basic:Básico|``, selecione ``||basic:mostrar ícone||``
e o encaixe dentro do laço ``||logic: se-então||``. Duplique o bloco 
``||basic:mostrar ícone||`` e altere a imagem do primeiro de coração grande para o coração pequeno. 
Feito isso, retorne ao menu ``||basic:Básico|`` e acrescente um bloco ``||basic:limpar tela||`` neste laço.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.SmallHeart)
        basic.showIcon(IconNames.Heart)
        basic.clearScreen()
    }
})
```

## Passo 8
Por último, vamos fazer a representação da **audição**. Acesse novamente a aba ``||logic:Lógica||``
e selecione outro bloco ``||logic:se-então||`` e posicione-o dentro do laço ``||basic:sempre||``
logo abaixo do laço condicional anterior.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.SmallHeart)
        basic.showIcon(IconNames.Heart)
        basic.clearScreen()
    }
		if (true) {
		}	
})
```

## Passo 9
Retorne à aba ``||logic:Lógica||`` e selecione o bloco triangular comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do laço 
``||logic:se-então||``, substituindo a palavra ``||logic:verdadeiro||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.SmallHeart)
        basic.showIcon(IconNames.Heart)
        basic.clearScreen()
    }
    if (0 == 0) {
    }	
})
```

## Passo 10
Agora, acesse a aba ``||input:Input||``, clique em ``||input:nível de som||`` e
use substitu o para substiruir o primeiro **0**. Altere o segundo **0** para 175 e o sinal de ``||logic:=||`` para ``||logic:>||``.
Esse valor é a intensidade de som captada sensor de som do Micro:Bit.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.SmallHeart)
        basic.showIcon(IconNames.Heart)
        basic.clearScreen()
    }
    if (input.soundLevel() > 175) {
    }	
})   
```

## Passo 11
Agora, para a resposta ao nível de som, vá até a aba ``||music:Música||``, selecione
o primeiro bloco ``||music:play risadinha until done||`` e o encaixe dentro do segundo laço ``||logic:se-então||``

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Hello!")
    basic.clearScreen()
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.SmallHeart)
        basic.showIcon(IconNames.Heart)
        basic.clearScreen()
    }
    if (input.soundLevel() > 175) {
    	  music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
    }	
})
```

## Passo 12
Pronto! Você já pode carregar seu código para o Micro:bit e testar os sentidos
na estrutura de blocos de montar. 

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```