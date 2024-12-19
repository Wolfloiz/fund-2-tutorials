# Rotação e Translação

## Step 1
Neste tutorial, vamos desenvolver um código para representar a mudança das estações.
Para isso, usaremos a matriz de LEDs para exibir a primeira letra de cada estação
quando o projeto "Rotação e translação" completa 1/4 de volta.

## Step 2
Primeiro, importe a biblioteca da Fuzzy para habilitar as abas ``||Actuators:Atuadores||`` e ``||sensors:Sensores||``.
Para isso, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Step 3
Em seguida, vá até a aba ``||basic:Básico||``e selecione o laço``||basic:sempre||``, 
caso ele não esteja na área de trabalho.

```blocks
basic.forever(function () {
    }
})
```

## Step 4
Agora, dentro da aba ``||loops:Loops||``, selecione ``||loops:enquanto-executar||`` 
e o encaixe dentro do laço ``||basic:sempre||``.

```blocks
basic.forever(function () {
    while (false) {
    })
```

## step 5
Vá à aba ``||logic:Lógica||`` e selecione o bloco triangular comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do loop 
``||loops:enquanto-executar||``, substituindo a palavra **falso**.

```blocks
basic.forever(function () {
    while (0 == 0) {
    })
```

## Step 6
Agora, acesse a aba ``||sensors:Sensores||``, selecione ``||sensors:valor do botão na porta P2||``
e use-o para substituir o primeiro **0** do comparador. Em seguida, mude o segundo **0**
para **1**.

```blocks
basic.forever(function () {
    while (sensors.buttonValue(InputPorts.P1) == 1) {
        
})
```

## Step 7
Acesse a aba ``||actuators:Atuadores||``, selecione o bloco ``||actuators:Motor CC,definir velocidade 0 do motor na porta P8||``.
Em seguida, altere a velocidade do motor para **500** e a porta de **P8** para **P12**

```blocks
basic.forever(function () {
    while (sensors.buttonValue(InputPorts.P1) == 1) {
    actuators.SetSpeedMotor(500, OutputPorts.P12)}
)}
```

## Step 8
Vá até a aba ``||basic:Básico||`` e pegue o bloco ``||basic:mostrar string "Hello!"||``.
Então, posicione-o dentro do loop ``||loops:enquanto-executar||``, logo abaixo
do bloco ``||actuators:Motor CC,definir velocidade 500 do motor na porta P12||``. 
Para representar o outono, substitua a palavra **Hello!** pela letra **"O"**.

```blocks
basic.forever(function () {
    while (sensors.buttonValue(InputPorts.P2) == 1) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        basic.showString("O")
    }
})
```

## Step 9
Na aba ``||basic:Básico||`` selecione o bloco ``||basic:pausa (ms) 100||`` e posicione-o após
o bloco ``||basic:mostrar leds||``. Altere o tempo para **2 segundos** (2000 milisegundos).

```blocks
basic.forever(function () {
    while (sensors.buttonValue(InputPorts.P2) == 1) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        basic.showString("O")
        basic.pause(2000)
    }
})
```

## Step 10
Da mesma forma que usamos os LEDs para representar o outono, repita os passos 8 e 9
alterando a palavra **Hello!** pela a letra **I**.
Vá até a aba ``||basic:Básico||``, pegue outro bloco ``||basic:mostrar leds||`` e
posicione-o no loop. Por fim, adicione outro comando ``||basic:pausa (ms) 100||``
e altere o tempo para **2 segundos**.

```blocks
basic.forever(function () {
    while (sensors.buttonValue(InputPorts.P2) == 1) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        basic.showString("O")
        basic.pause(2000)
        basic.showString("I")
        basic.pause(2000)
    }
})
```

## Step 11
Refaça alterando a palavra para a letra **P** e o tempo para **2 segundos**.

```blocks
basic.forever(function () {
    while (sensors.buttonValue(InputPorts.P2) == 1) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        basic.showString("O")
        basic.pause(2000)
        basic.showString("I")
        basic.pause(2000)
        basic.showString("P")
        basic.pause(2000)
    }
})
```
## Step 12
Por fim, faça para a letra  **V** mantendo o mesmo tempo.

```blocks
basic.forever(function () {
    while (sensors.buttonValue(InputPorts.P2) == 1) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        basic.showString("O")
        basic.pause(2000)
        basic.showString("I")
        basic.pause(2000)
        basic.showString("P")
        basic.pause(2000)
        basic.showString("V")
        basic.pause(2000)
    }
})

```
## Step 13
Pronto! Você já pode carregar seu código para o Micro:bit e testá-lo no projeto.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```