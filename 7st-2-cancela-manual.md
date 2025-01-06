# Cancela de estacionamento manual

## Step 1
Neste tutorial, vamos criar uma cancela de estacionamento operada manualmente, utilizando o
Potenciômetro para controlá-la.

## Step 2
Primeiro, importe a biblioteca da Fuzzy para habilitar as abas ``||Actuators:Atuadores||`` 
e ``||sensors:Sensores||``. Para isso, clique na aba **__+Extensões__**, insira o endereço 
https://github.com/FuzzyMakers/pxt-fuzzyMakers no campo de pesquisa e selecione a biblioteca.

## Step 3
Agora, acesse a aba ``||actuators:Atuadores||``, selecione o comando ``||actuators:Servo motor, definir ângulo 0 do servo motor na porta P8 no modo Knob||`` e
posicione-o dentro do laço ``||basic:sempre||``. Esse comando permite ajustar o ângulo do servo motor conforme o valor captado
pela entrada da porta definida. Altere a porta de saída de **P8** para **P16**.

**ATENÇÃO:** Note que há dois comandos parecidos para o servo motor, **Knob** e **Sweep**, selecioce o **KNOB**. 

```blocks
basic.forever(function () {
    actuators.SetAngleServoKnob(0, OutputPorts.P16)
})
```

## Step 4
Vá até aba ``||Math:Matemática||``, selecione o bloco ``||Math:map 0 from low 0 high 1023 to low 0 high 4||`` e 
use-o para substituir o número **0**.

O comando ``||Math:Map||`` faz a conversão de um intervalo de números para outro. 

```blocks
basic.forever(function () {
    actuators.SetAngleServoKnob(Math.map(0, 0, 1023, 0, 4), OutputPorts.P8)
})
```

## Step 5
Agora, vá até a aba ``||sensors:Sensores||``, selecione o bloco ``||sensors:Valor do potenciômetro na porta P2||`` e
use-o para substituir o primeiro **0** do comando ``||Math:Map||``.
Altere a porta de entrada de **P2** para **P1**.

```blocks
basic.forever(function () {
    actuators.SetAngleServoKnob(Math.map(sensors.dimmerValue(InputPorts.P1), 0, 1023, 0, 4), OutputPorts.P8)
})
```

## Step 6
Para finalizar, vamos configurar a conversão dos intervalos de valores do comando ``||Math:Map||``.

O potenciômetro varia de 0 a 1023, correspondendo a uma variação de 0º a 180º no servo motor. 
Porém, para que a cancela fique na posição horizontal quando fechada (0º) e na posição vertical
quando aberta (90º), é necessário ajustar o intervalo de variação do ângulo do servo motor. 
Assim, iremos converter o intervalo de 0 a 1023 para 135 a 450, que corresponde ao movimento de 0º a 90º.

Agora, basta modificar os valores no comando, 135 no lugar do último 0 e 450 substituindo o número 4, 
no último campo circular. 

```blocks
basic.forever(function () {
    actuators.SetAngleServoKnob(Math.map(sensors.dimmerValue(InputPorts.P1), 0, 1023, 135, 450), OutputPorts.P16)
})
```

## Step 7
Pronto! Você já pode carregar seu código para o Micro:bit e testá-lo no projeto.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```