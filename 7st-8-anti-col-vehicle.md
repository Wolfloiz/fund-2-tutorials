### @diffs true

# Veículo Anti-Colisão

## Passo 1
Nessa atividade, vamos programar um veículo capaz de evitar colisões. A ideia é
que ele fique andando para frente até que seja identificado um obstáculo. Quando 
isso acontecer, ele vai parar, dar ré, virar e reiniciar o movimento para frente.

## Passo 2
Para começar, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3
Vamos começar configurando a inicialização do Micro:bit em nosso código. Para isso, acesse a 
aba ``||Basic:Básico||`` e insira o bloco ``||Basic:mostrar ícone||`` dentro do laço ``||Basic:no iniciar||``.

Mantivemos o ícone de coração apenas para indicar que o Micro:bit ligou, mas fique à vontade para alterar para um 
ícone a sua escolha.

```blocks
basic.showIcon(IconNames.Heart)
```

## Passo 4
Retorne à categoria ``||Basic:Básico||`` e adicione os blocos ``||Basic:pausa (ms)||`` e ``||Basic:limpar tela||`` dentro do laço ``||Basic:no iniciar||``.

Altere a duração da ``||Basic:pausa||`` de **100ms** para **1000ms** (1 segundo). 

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
```

## Passo 5
Feito isso, adicione um laço ``||Basic:sempre||`` localizado na aba ``||Basic:Básico||`` para programar a lógica principal do código.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
	
})
```

## Passo 6
Acesse a categoria ``||actuators:Atuadores||`` e adicione **dois** blocos ``||actuators:Motor CC, definir direção sentido horário porta P8||`` seguidos do comando
``||actuators:Motor CC, definir velocidade 0 porta P8||``.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(0, OutputPorts.P8)
})
```

## Passo 7
Agora, vamos editar os parâmetros desses blocos para garantir que o veículo se movimente para frente.
 
 No primeiro comando, altere para:
 ``||actuators:Sentido horário||`` e ``||actuators:Porta P16||``;
 
 No segundo comando, altere para:
 ``||actuators:Sentido anti-horário||`` e ``||actuators:Porta P8||``;
 
 E no terceiro bloco, de velocidade, altere para:
 ``||actuators:512||`` e ``||actuators:Porta P12||``;

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
})
```

## Passo 8
Caso seu veículo não esteja andando para frente ao inicializar o Micro:bit, retorne aos blocos anteriores 
e verifique seus parâmetros. Se necessário, inverta os sentidos de rotação dos motores nas porta ``||actuators:Porta P8||`` e ``||actuators:Porta P16||``,
certificando-se sempre de que os sentidos de rotação dos motores sejam opostos um ao outro.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
})
```

## Passo 9
Agora, vamos criar o teste condicional do sensor de obstáculos. Para isso, acesse a categoria 
``||logic:Lógica||`` e insira o laço ``||logic:se verdadeiro então||`` abaixo dos blocos anteriores.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (true) {
    	
    }
})
```

## Passo 10
Retorne à aba ``||logic:Lógica||`` e use o comparador ``||logic:0 < 0||`` para substituir o ``||logic:verdadeiro||``
no laço ``||logic:se verdadeiro então||``.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (0 < 0) {
    	
    }
})
```

## Passo 11
Agora, acesse a categoria ``||sensors:Sensores||`` e selecione o bloco ``||sensors:Valor do sensor infravermelho na porta P2||``. 
Altere a porta de ``||sensors:P2||`` para  ``||sensors:P1||``. 

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) < 0) {
    	
    }
})
```

## Passo 12
Modifique o operador de **<** para **>** e o valor de **0** para **75**.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) > 75) {
    	
    }
})
```

## Passo 13
Dentro do ``||logic:então||``, devemos programar o comportamento do veículo ao identificar um obstáculo.
A primeira ação é parar os motores com o bloco ``||actuators:Motor CC, parar motor na porta P8||``, localizado
na aba ``||actuators:Atuadores||``. Altere a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) > 75) {
        actuators.StopMotor(OutputPorts.P12)
    }
})
```

## Passo 14
Agora, precisamos programar a ré do veículo. Para isso, vamos duplicar os três comandos de movimento 
que definimos no início desse laço ``||basic:sempre||``. Entretanto, vamos inverter as direções de rotação das portas ``||actuators:P16||`` e ``||actuators:P8||``.

 Assim, teremos:
 
 No primeiro comando:
 ``||actuators:Sentido anti-horário||`` e ``||actuators:Porta P16||``;
 
 No segundo comando:
 ``||actuators:Sentido horário||`` e ``||actuators:Porta P8||``;
 
 E no terceiro bloco, de velocidade:
 ``||actuators:512||`` e ``||actuators:Porta P12||``;

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) > 75) {
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
    }
})
```

## Passo 15
Acesse a categoria ``||basic:Básico||`` e adicione uma ``||basic:pausa (ms)||`` de **1000ms** (1 segundo)
para determinar a duração do movimento de ré.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) > 75) {
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
        basic.pause(1000)
    }
})
```

## Passo 16
Em seguida, duplicaremos os três blocos de comando dos motores novamente para determinar o movimento
rotacional do veículo. Agora, os motores devem girar para o mesmo sentido fazendo que o veículo gire sobre seu próprio eixo.
 
 No primeiro comando:
 ``||actuators:Sentido horário||`` e ``||actuators:Porta P16||``;
 
 No segundo comando:
 ``||actuators:Sentido horário||`` e ``||actuators:Porta P8||``;
 
 E no terceiro bloco, de velocidade:
 ``||actuators:512||`` e ``||actuators:Porta P12||``;

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) > 75) {
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
    }
})
```

## Passo 17
Por fim, adicione uma ``||basic:pausa (ms)||`` de **480ms** para definir a duração do movimento de rotação do veículo.
Para ajustar o ângulo de rotação do veículo, altere o tempo desta ``||basic:pausa (ms)||``.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) > 75) {
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
        basic.pause(480)
    }
})
```

## Passo 18
Agora, teste seu veículo observando os movimentos e identificação de obstáculos. Se necessário,
ajuste os sentidos de rotação dos motores ou as durações das pausas em cada movimento.

```blocks

```

## Passo 19 
Confira o seu código clicando na lâmpada de dica.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
basic.forever(function () {
    actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
    actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
    actuators.SetSpeedMotor(512, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P1) > 75) {
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(512, OutputPorts.P12)
        basic.pause(480)
    }
})
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```