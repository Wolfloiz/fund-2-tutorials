# Sistema Nervoso

## Step 1
Neste tutorial, você irá utilizar o Micro:Bit para simular os sentidos humanos.
Usaremos o logotipo sensível ao toque para representar o tato, a matriz de LEDs
para a visão e o sensor de som para a audição. Cada um dos "sentidos" irá nos
retornar uma função diferente que o Micro:Bit é capaz de executar.

## Step 2
Para a parte do código que representa o **tato** vamos utilizar o logotipo para mostrar 
uma mensagem. Primeiro, acesse a categoria ``||input:Input||`` e adicione o laço 
``||input:no logotipo pressionado||``. Em seguida, vá até a categoria ``||basic:Básico||``
e pegue o bloco ``||basic:mostrar string||`` e o encaixe dentro do laço. Altere a escrita
contida no espaço circular para uma de sua preferência. Essa mensagem será exibida quando 
o logotipo for tocado. 

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
```

## Step 3
Para representar a **visão**, vamos utilizar a matriz de LEDs para ativar uma animação.
Primeiro, vá até a aba ``||basic:Básico||``e selecione o laço``||basic:sempre||``, caso ele
não esteja na área de trabalho.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    }
})
```
## step 4 
Vá até a aba ``||logic:Lógica||`` e selecione o bloco condicional ``||logic:se-então||``
e posicione-o dentro do laço ``||basic:sempre||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (true) {
    }	
})
```

## step 5 
Retorne à aba ``||logic:Lógica||`` e selecione o bloco triangular comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do laço 
``||logic:se-então||``, substituindo a palavra ``||logic:verdadeiro||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (0 == 0) {
    }	
})
```

## Step 6
Agora, acesse a aba ``||input:Input||``, clique em ``||input:nível de luz||`` e
use substitu o para substiruir o primeiro **0**.
Altere o segundo **0** para 200.
Esse valor é a quantidade de luz captada pela matriz de LEDs do Micro:Bit.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
    }
})
```

## Step 7
Agora iremos criar uma animação para responder ao ``||input:nível de luz||``. 
Para isso, acesse a aba ``||basic:Básico|``, selecione ``||basic:mostrar ícone||``
e o encaixe dentro do laço ``||logic: se-então||``. Duplique o bloco 
``||basic:mostrar ícone||`` e altere a imagem do coração grande para o coração pequeno. 

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.Heart)
        basic.showIcon(IconNames.SmallHeart)
    }  
})
```

## Step 8
Por último, vamos fazera representação da **audição**. Acesse novamente a aba ``||logic:Lógica||``
e selecione outro bloco ``||logic:se-então||`` e posicione-o dentro do laço ``||basic:sempre||``
logo abaixo do bloco condicional anterior.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.Heart)
        basic.showIcon(IconNames.SmallHeart)
    }
		if (true) {
		}	
})
```

## Step 9
Retorne à aba ``||logic:Lógica||`` e selecione o bloco triangular comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do laço 
``||logic:se-então||``, substituindo a palavra ``||logic:verdadeiro||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.Heart)
        basic.showIcon(IconNames.SmallHeart)
    }
    if (0 == 0) {
    }	
})
```

## Step 10
Agora, acesse a aba ``||input:Input||``, clique em ``||input:nível de som||`` e
use substitu o para substiruir o primeiro **0**. Altere o segundo **0** para 175.
Esse valor é a intensidade de som captada sensor de som do Micro:Bit.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.Heart)
        basic.showIcon(IconNames.SmallHeart)
    }
    if (input.soundLevel() > 175) {
    }	
})   
```

## Step 11
Agora, para a resposta ao nível de som, vá até a aba ``||music:Música||``, selecione
o primeiro bloco ``||music:play risadinha until done||`` e o encaixe dentro do segundo laço ``||logic:se-então||``

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("Ola!")
})
basic.forever(function () {
    if (input.lightLevel() > 200) {
        basic.showIcon(IconNames.Heart)
        basic.showIcon(IconNames.SmallHeart)
    }
    if (input.soundLevel() > 175) {
    	  music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
    }	
})
```

## Step 12
Pronto! Você já pode carregar seu código para o Micro:bit e testar os sentidos
na estrutura de blocos de montar. 

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```