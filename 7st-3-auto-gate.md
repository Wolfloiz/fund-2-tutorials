# Cancela de estacionamento automática

## Step 1
Neste tutorial, você aprenderá a criar uma cancela de estacionamento automática, 
utilizando o sensor infravermelho para ativá-la.

## Step 2
Primeiro, importe a biblioteca da Fuzzy para habilitar as abas ``||Actuators:Atuadores||`` e 
``||sensors:Sensores||``. Para isso, clique na aba __+Extensões__, insira o endereço 
https://github.com/FuzzyMakers/pxt-fuzzyMakers no campo de pesquisa e selecione a biblioteca.

## Step 3
Agora, acesse a aba ``||actuators:Atuadores||``, selecione o comando ``||actuators:Servo motor, definir ângulo 0 do servo motor na porta P8 no modo Knob||`` e
posicione-o dentro do laço ``||basic:no iniciar||``. Esse comando permite ajustar o ângulo do
servo motor conforme o valor captado pela entrada da porta definida. Altere a porta de saída de
**P8** para **P16** e o **0**, do campo circular, para **135**, que é o valor para a cancela fechada em 0º.

**ATENÇÃO:** Note que há dois comandos parecidos para o servo motor, **Knob** e **Sweep**, selecioce o **KNOB**. 

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
```
## Step 4
Em seguida, vá até a aba ``||basic:Básico||``e selecione o laço``||basic:sempre||``, caso ele
não esteja na área de trabalho.

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    
})
```

## Step 5
Na aba ``||logic:Lógica||`` e selecione o bloco condicional ``||logic:se-então||``
e posicione-o dentro do laço ``||basic:sempre||``.

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    if (true) {

    }
})
```

## Step 6
Retorne à aba ``||logic:Lógica||`` e selecione o bloco comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do laço 
``||logic:se-então||``, substituindo a palavra ``||logic:verdadeiro||``.

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    if (0 == 0) {
    	
    }
})
```

## Step 7
Agora, acesse a aba ``||sensors:Sensores||``, clique em ``||sensors:Valor do sensor infravermelho na porta P2||`` e
use-o substiruir o primeiro **0**.

Altere o segundo **0** para **250**.

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
    	
    }
})
```

## Step 8
Retorne à aba ``||actuators:Atuadores||``, selecione o comando ``||actuators:Servo motor, definir ângulo 0 do servo motor na porta P8 no modo Knob||`` e
posicione-o dentro do laço ``||logic:se-então||``.

Altere a porta de saída de **P8** para **P16** e o **0**, do campo circular, para **450**, que indica a cancela aberta em 90º.

**ATENÇÃO:** Note que há dois comandos parecidos para o servo motor, **Knob** e **Sweep**, selecioce o **KNOB**. 

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
    }
})
```

## Step 9
Vá até a aba ``||basic:Básico||``, selecione o bloco ``||basic:pausa (ms) 100||`` 
e posicione-o abaixo do bloco ``||actuators:Servo motor||`` ainda dentro laço ``||logic:se-então||``.

Ajuste o tempo para **5000 ms**, esse é tempo que a cancela ficará aberta para a passagem
dos veículos.

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
    }
})
```

## Step 10
Na aba ``||actuators:Atuadores||``, selecione o comando ``||actuators:Servo motor, definir ângulo 0 do servo motor na porta P8 no modo Knob||`` e
posicione-o dentro do laço ``||logic:se-então||`` abaixo do bloco ``||basic:pausa (ms) 100||``.

Altere a porta de saída de **P8** para **P16** e o **0**, do campo circular, para **135**.

**ATENÇÃO:** Note que há dois comandos parecidos para o servo motor, **Knob** e **Sweep**, selecioce o **KNOB**. 

```blocks
actuators.SetAngleServoKnob(135, OutputPorts.P16)
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P2) > 250) {
        actuators.SetAngleServoKnob(450, OutputPorts.P16)
        basic.pause(5000)
        actuators.SetAngleServoKnob(135, OutputPorts.P16)
    }
})
```
## Step 11
Pronto! Você já pode carregar seu código para o Micro:bit e testá-lo no projeto.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```