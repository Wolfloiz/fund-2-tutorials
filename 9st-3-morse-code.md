# Código Morse


## Passo 1

Neste tutorial, você vai aprender a usar Micro:bits para conversar usando 
Código Morse. Para a comunicação acontecer, cada Micro:bit deve ser capaz de 
enviar e receber as mensagens.


## Passo 2

Selecione o bloco ``||radio:definir grupo do rádio 1||``, na categoria 
``||radio:Rádio||``, e arraste para dentro do laço ``||basic:no iniciar||``. 
Esse bloco serve para garantir que todos os micro:bits dentro desse mesmo grupo
de rádio estejam conectados uns com os outros. Portanto, certifique-se de que o grupo configurado no seu Micro:bit 
seja diferente do utilizado pelos outros grupos da sala de aula.
 
 Altere o número do grupo de **1** para **255**, ou outro número próximo 
deste valor.

```blocks
radio.setGroup(255)
```

## Passo 3

Para enviar mensagens em Código Morse, você precisa inicialmente de três comandos:
 
 Um para enviar um traço, outro para enviar um ponto, e um último para mostrar 
 que a letra já acabou e você irá passar para a próxima. 
  
  Então, adicione os três laços ``||input:no botão A pressionado||``, 
``||input:no botão B pressionado||`` e ``||input:no botão A+B pressionado||``.

```blocks
input.onButtonPressed(Button.A, function () {
	
})
input.onButtonPressed(Button.B, function () {
	
})
input.onButtonPressed(Button.AB, function () {
	
})
radio.setGroup(255)
```

## Passo 4

Dentro do laço ``||input:no botão A pressionado||``, adicione o bloco 
``||basic:mostrar leds||`` e desenhe um quadrado 3x3 para representar um ponto. 
Já no laço ``||input:no botão B pressionado||``, adicione outro bloco 
``||basic:mostrar leds||`` e desenhe uma linha de 3 leds acesos para 
representar o traço.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
})
```

## Passo 5

Por fim, no laço ``||input:no botão A+B pressionado||`` adicione o bloco 
``||basic:mostrar leds||`` e desenhe uma seta para a direita, representando 
que a palavra foi finalizada e você está passando para a próxima.

```blocks
input.onButtonPressed(Button.AB, function () {
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
})
```

## Passo 6

Mas e agora? Como você vai transmitir as letras e palavras que está digitando 
para o outro Micro:bit? Para isso, use o bloco ``||radio:rádio envia número||`` 
que pode ser encontrado na categoria ``||radio:Rádio||``. Adicione este 
bloco abaixo de cada um dos três desenhos. No caso do **ponto**, envie o 
número **0**, no caso do **traço** envie o número **1**, e para passar 
para **próxima palavra**, envie o número **2**.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
    radio.sendNumber(0)
})
input.onButtonPressed(Button.AB, function () {
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
    radio.sendNumber(2)
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
    radio.sendNumber(1)
})
radio.setGroup(255)
```

## Passo 7

Para garantir que o sinal foi transmitido, e que você possa visualizar qual 
símbolo enviou, adicione os blocos ``||basic:pausa (ms) 100||`` e 
``||basic:limpar tela||``  abaixo de cada bloco ``||radio:rádio envia número||`` nos três laços.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
    radio.sendNumber(0)
    basic.pause(100)
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
    radio.sendNumber(2)
    basic.pause(100)
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
    radio.sendNumber(1)
    basic.pause(100)
    basic.clearScreen()
})
```

## Passo 8

Agora você deve implementar a parte do código responsável por receber as informações de outro Micro:bit e exibi-las na tela, 
possibilitando a comunicação.

## Passo 9

Adicione o laço ``||radio:ao receber rádio receivedNumber||``,
que pode ser encontrado na aba ``||radio:Rádio||``. Esse bloco executa tudo que
está dentro dele quando recebe um número de outro Micro:bit.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
	
})
```

## Passo 10

Feito isso, dentro do laço ``||radio:ao receber rádio receivedNumber||``, adicione
três laços condicionais ``||logic:se-então||``, que estão na aba ``||logic:Lógica||``. 

 **ATENÇÃO**: Certifique-se de posicionar os blocos um **abaixo** do outro, pois, se forem aninhados, o programa não funcionará corretamente.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (true) {
    	
    }
    if (true) {
    	
    }
    if (true) {
    	
    }
})
```

## Passo 11

Agora, adicione os comparadores lógicos aos laços ``||logic:se-então||``. 
Os blocos comparadores podem ser encontrados na aba ``||logic:Lógica||``. A primeira 
condição será ``||logic:receivedNumber = 0||``, e a segunda será 
``||logic:receivedNumber = 1||``. Para incluir o bloco ``||radio:receivedNumber||``, 
arraste *(clique sobre ele e mova o mouse)* a variável ``||variables:receivedNumber||`` do laço 
``||radio:ao receber rádio receivedNumber||``.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
    	
    }
    if (receivedNumber == 1) {
    	
    }
    if (receivedNumber == 2) {
    	
    }
})
```

## Passo 12

Em seguida, utilize a estrutura condicional para mostrar o símbolo (**ponto**, **traço** 
ou **seta**) na tela, de acordo com o número recebido. Se o número recebido ``||radio:receivedNumber||``   
for igual a **zero**, mostre o **ponto**, se for igual a **1**, mostre
o **traço**. Por fim, se não for nenhum dos dois, mostre a **seta**.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
    if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    }
    if (receivedNumber == 2) {
        basic.showLeds(`
            . . # . .
            . . . # .
            # # # # #
            . . . # .
            . . # . .
            `)
    }
})
```

## Passo 13

Finalmente, adicione os blocos de ``||basic:pausa||`` e 
``||basic:limpar tela||`` abaixo do último ``||logic:se-então||``, para ter 
tempo de ver o símbolo nos LEDs, e depois apagá-lo, para esperar o próximo.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
    if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    }
    if (receivedNumber == 2) {
        basic.showLeds(`
            . . # . .
            . . . # .
            # # # # #
            . . . # .
            . . # . .
            `)
    }
    basic.pause(100)
    basic.clearScreen()
})
```

## Passo 14

Mas, e se você apertar um botão errado por acidente? É preciso avisar a pessoa que recebeu
a mensagem sobre o erro, e então, começar a escrever a palavra novamente! Mas como 
você pode fazer isso?

## Passo 15

Da mesma forma que você pode escolher enviar um ponto, traço ou próxima palavra, 
você também pode enviar uma informação que signifique reiniciar palavra. Para 
isso, comece adicionando o laço ``||input:em agitar||``, localizado na 
categoria ``||input:input||``. Assim, sempre que quiser reiniciar a palavra, basta agitar o Micro:bit.

```blocks
input.onGesture(Gesture.Shake, function () {
	
})
```

## Passo 16

Em seguida, coloque os mesmos blocos que estão dentro de 
``||input:no botão A pressionado||``, dentro também do laço 
``||input:em agitar||``. Para facilitar, você pode fazer isso copiando e colando 
todo o laço, ou duplicando os blocos.

```blocks
input.onGesture(Gesture.Shake, function () {
	basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
    radio.sendNumber(0)
    basic.pause(100)
    basic.clearScreen()
})
```

## Passo 17

Agora, altere tanto o símbolo exibido, quanto o número enviado ao 
agitar o micro:bit. Dentro do laço ``||input:em agitar||``, modifique o bloco 
``||basic:mostrar leds||`` para exibir um **X**. Já no bloco 
``||radio:rádio envia número 0||``, troque o número **0** pelo número **3**.

```blocks
input.onGesture(Gesture.Shake, function () {
	basic.showLeds(`
        # . . . #
        . # . # .
        . . # . .
        . # . # .
        # . . . #
        `)
    radio.sendNumber(3)
    basic.pause(100)
    basic.clearScreen()
})
```

## Passo 18

Assim, você já finalizou a parte de enviar a mensagem para reiniciar a palavra. 
No entanto, ainda falta modificar o código responsável por receber essa informação.

## Passo 19

Dentro do laço ``||radio:ao receber rádio receivedNumber||``, adicione outro ``||logic:se-então||``
abaixo dos posicionados anteriormente.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
    if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    }
    if (receivedNumber == 2) {
        basic.showLeds(`
            . . # . .
            . . . # .
            # # # # #
            . . . # .
            . . # . .
            `)
    }
    if (true) {
    	
    }
    basic.pause(100)
    basic.clearScreen()
})
```

## Passo 20

Neste laço condicional que acabou de ser criado, coloque a condição 
``||logic:receivedNumber = 3||``. Por fim, dentro do ``||logic:então||`` 
desse laço, adicione o bloco ``||basic:mostrar leds||`` e desenhe um **X**.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
    if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    }
    if (receivedNumber == 2) {
        basic.showLeds(`
            . . # . .
            . . . # .
            # # # # #
            . . . # .
            . . # . .
            `)
    }
    if (receivedNumber == 3) {
        basic.showLeds(`
            # . . . #
            . # . # .
            . . # . .
            . # . # .
            # . . . #
            `)
    }
    basic.pause(100)
    basic.clearScreen()
})
```

## Passo 21

Pronto, agora você pode carregar esse programa para os dois micro:bits, e se 
comunicar via Código Morse! E então, será que você consegue manter uma conversa com um amigo usando apenas o Código Morse?
Se errar, não se esqueça de agitar o Micro:bit e recomeçar 
a palavra.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
    if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    }
    if (receivedNumber == 2) {
        basic.showLeds(`
            . . # . .
            . . . # .
            # # # # #
            . . . # .
            . . # . .
            `)
    }
    if (receivedNumber == 3) {
        basic.showLeds(`
            # . . . #
            . # . # .
            . . # . .
            . # . # .
            # . . . #
            `)
    }
    basic.pause(100)
    basic.clearScreen()
})
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
    radio.sendNumber(0)
    basic.pause(100)
    basic.clearScreen()
})
input.onGesture(Gesture.Shake, function () {
    basic.showLeds(`
        # . . . #
        . # . # .
        . . # . .
        . # . # .
        # . . . #
        `)
    radio.sendNumber(3)
    basic.pause(100)
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
    radio.sendNumber(2)
    basic.pause(100)
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
    radio.sendNumber(1)
    basic.pause(100)
    basic.clearScreen()
})
radio.setGroup(255)
```