
# Cancela de estacionamento híbrida

``` template
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
        actuators.SetAngleServoKnob(135, OutputPorts.P16)
    }
})
```

## Passo 1

Neste tutorial, vamos combinar as lógicas das duas últimas atividades para programarmos uma cancela que pode ser operada manualmente, 
mas que também possa ser mantida em modo automático.

## Passo 2

Como de costume, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3

Feito isso, precisaremos de uma variável para armazenar o modo de operação da cancela. Portanto, acesse
a categoria ``||variables:Variáveis||`` e crie uma variável denominada ``||variables:Modo||``. Insira o bloco
``||variables:Definir Modo para 0||`` no laço ``||basic:no iniciar||``.

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
let Modo = 0
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
        actuators.SetAngleServoKnob(135, OutputPorts.P16)
    }
})
```

## Passo 4

Agora, vá até a aba ``||Input:Input||`` e adicione dois laços ``||Input:no botão A pressionado||``.
Altere o parâmetro do segundo laço de ``||Input:Botão A||`` para ``||Input:Botão B||``.   

```blocks
input.onButtonPressed(Button.A, function () {
	
})
input.onButtonPressed(Button.B, function () {
	
})
actuators.SetAngleServoKnob(135, OutputPorts.P16)
let Modo = 0
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
        actuators.SetAngleServoKnob(135, OutputPorts.P16)
    }
})
```

## Passo 5

Encaixe um bloco ``||variables:Definir Modo para 0||`` em cada laço de ``||Input:no botão pressionado||`` adicionado no passo anterior.
Modifique o valor de **0** para **1** dentro de ``||Input:no botão B pressionado||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
        actuators.SetAngleServoKnob(135, OutputPorts.P16)
    }
})
```

## Passo 6

Feito isso, adicione um laço ``||Logic:se <verdadeiro> então... senão||`` dentro do laço  ``||basic:sempre||``. Ele fica localizado na 
aba ``||Logic:Lógica||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (true) {
    	
    } else {
    	
    }
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
        actuators.SetAngleServoKnob(135, OutputPorts.P16)
    }
})
```

## Passo 7

Retorne à aba ``||Logic:Lógica||`` e adicione um bloco comparador ``||Logic:0 = 0||`` no campo  ``||Logic:<verdadeiro>||`` do laço
adicionado anteriormente. Altere o primeiro **0** para a variável  ``||variables:Modo||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
    	
    } else {
    	
    }
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
        actuators.SetAngleServoKnob(135, OutputPorts.P16)
    }
})
```

## Passo 8

Agora, mova todo o laço ``||Logic:Se||`` que contém ``||sensors:Valor do sensor infravermelho na porta P2||`` ``||Logic:> 250 então||``
para dentro do ``||Logic:Então||`` do novo laço adicionado. Assim, teremos um ``||Logic:Se||`` dentro de outro, ou seja, condições aninhadas.

Isso significa que a segunda condição será verificada apenas se a primeira já tiver sido atendida.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
        if (sensors.infraredValue(InputPorts.P2) > 250) {
            actuators.SetAngleServoKnob(450, OutputPorts.P16)
            basic.pause(5000)
            actuators.SetAngleServoKnob(135, OutputPorts.P16)
        }
    } else {
    	
    }
})
```

## Passo 9

Dessa forma, quando pressionarmos o ``||input:botão A||``, o ``||variables:Modo||`` será igual a **0**, e a cancela entrará em operação automática.
Entretanto, ainda precisamos programar a operação manual...

## Passo 10

Para isso, aproveitaremos o código da atividade da cancela manual e o posicionaremos dentro do laço ``||Logic:senão||``. Então, acesse
a categoria ``||actuators:Atuadores||`` e selecione o bloco ``||actuators:servo motor, definir ângulo 0 do servo na porta P8 no modo knob||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
        if (sensors.infraredValue(InputPorts.P2) > 250) {
            actuators.SetAngleServoKnob(450, OutputPorts.P16)
            basic.pause(5000)
            actuators.SetAngleServoKnob(135, OutputPorts.P16)
        }
    } else {
        actuators.SetAngleServoKnob(0, OutputPorts.P8)
    }
})
```

## Passo 11

Altere de porta ``||actuators:P8||`` para ``||actuators:P16||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
        if (sensors.infraredValue(InputPorts.P2) > 250) {
            actuators.SetAngleServoKnob(450, OutputPorts.P16)
            basic.pause(5000)
            actuators.SetAngleServoKnob(135, OutputPorts.P16)
        }
    } else {
        actuators.SetAngleServoKnob(0, OutputPorts.P16)
    }
})
```

## Passo 12

Modifique o valor **0** deste bloco pelo comando ``||math:map 0 from low 0 high 1023 to low 0 high 4||`` localizado na 
categoria ``||math:Matemática||``. Esses valores representam os ângulos mínimos e máximos da cancela, garantindo que ela se mova corretamente.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
        if (sensors.infraredValue(InputPorts.P2) > 250) {
            actuators.SetAngleServoKnob(450, OutputPorts.P16)
            basic.pause(5000)
            actuators.SetAngleServoKnob(135, OutputPorts.P16)
        }
    } else {
        actuators.SetAngleServoKnob(Math.map(0, 0, 1023, 0, 4), OutputPorts.P16)
    }
})
```

## Passo 13

Agora, acesse a aba ``||sensors:Sensores||`` e selecione o bloco ``||sensors:Valor do potenciômetro na porta P2||``. 
Ele deve ser encaixado no primeiro **0** do comando ``||math:map||``. Em seguida, altere a porta de ``||sensors:P2||`` para ``||sensors:P1||``

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
        if (sensors.infraredValue(InputPorts.P2) > 250) {
            actuators.SetAngleServoKnob(450, OutputPorts.P16)
            basic.pause(5000)
            actuators.SetAngleServoKnob(135, OutputPorts.P16)
        }
    } else {
        actuators.SetAngleServoKnob(Math.map(sensors.dimmerValue(InputPorts.P1), 0, 1023, 0, 4), OutputPorts.P16)
    }
})
```

## Passo 14

Por fim, modifique os dois últimos valores do bloco ``||math:map||`` de **0** e **4** para **135** e **450**.

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
        if (sensors.infraredValue(InputPorts.P2) > 250) {
            actuators.SetAngleServoKnob(450, OutputPorts.P16)
            basic.pause(5000)
            actuators.SetAngleServoKnob(135, OutputPorts.P16)
        }
    } else {
        actuators.SetAngleServoKnob(Math.map(sensors.dimmerValue(InputPorts.P1), 0, 1023, 135, 450), OutputPorts.P16)
    }
})
```

## Passo 15

Agora, sua cancela está completa! Ao pressionar o ``||input:botão A||``, ela funcionará automaticamente. 
Já ao pressionar o ``||input:botão B||``, você poderá operá-la manualmente. 
Faça seus testes e explore novas formas de aprimorar seu projeto com outras funcionalidades!"

```blocks
input.onButtonPressed(Button.A, function () {
    Modo = 0
})
input.onButtonPressed(Button.B, function () {
    Modo = 1
})
let Modo = 0
actuators.SetAngleServoKnob(135, OutputPorts.P16)
Modo = 0
basic.forever(function () {
    if (Modo == 0) {
        if (sensors.infraredValue(InputPorts.P2) > 250) {
            actuators.SetAngleServoKnob(450, OutputPorts.P16)
            basic.pause(5000)
            actuators.SetAngleServoKnob(135, OutputPorts.P16)
        }
    } else {
        actuators.SetAngleServoKnob(Math.map(sensors.dimmerValue(InputPorts.P1), 0, 1023, 135, 450), OutputPorts.P16)
    }
})
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```
