# Primeiro Código

## Step 1
Neste tutorial, vamos criar o primeiro código. O Micro:bit exibirá uma carinha feliz
ao iniciar, e, ao pressionar o botão A, será exibida uma seta para a esquerda;
ao pressionar o botão B, aparecerá uma seta para a direita.

## Step 2
Primeiramente, acesse a aba ``||basic:Básico||``, selecione o comando 
``||basic:mostrar ícone||`` e arraste-o até o laço ``||basic:no iniciar||``.
Altere o ícone de coração por uma carinha feliz. 

```blocks
basic.showIcon(IconNames.Happy)
})
```

## Step 3
Acesse a categoria ``||input:Input||`` e adicione dois laços ``||input:no botão A pressionado||``.
Altere um destes laços de ``||input:botão A||`` para ``||input:botão B||``.

```blocks
basic.showIcon(IconNames.Happy)
input.onButtonPressed(Button.A, function () {
})
input.onButtonPressed(Button.B, function () {
})
```

## Step 4
Para os laços ``||input:no botão A pressionado||`` e ``||input:no botão B pressionado||``,
adicione o comando ``||basic:mostrar leds||`` em cada um deles.

```blocks
basic.showIcon(IconNames.Happy)
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
})
```

## Step 5
Para finalizar, desenhe uma seta em cada um dos paineis. No comando ``||basic:mostrar leds||``
que está dentro do laço ``||input:no botão A pressionado||`` faça a seta apontando para esquerda
e para o painel de LEDs do laço do ``||input:no botão B pressionado||`` faça uma seta direcionada 
para a direita. 

```blocks
basic.showIcon(IconNames.Happy)
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . # . .
        . # . . .
        # # # # #
        . # . . .
        . . # . .
        `)
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
})
```

## Step 6
Pronto! Você já pode carregar seu código para o micro:bit e testar o funcionamento do seu primeiro código!

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```