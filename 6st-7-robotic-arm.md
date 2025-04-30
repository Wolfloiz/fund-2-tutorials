### @diffs true

# Braço Robótico

## Passo 1
Nessa atividade, vamos programar os movimentos de um braço robótico controlados pelo Bit Potenciômetro
e pelo acelerômetro do Micro:bit. O objetivo é usar o acelerômetro para girar a base do manipulador e o 
Potenciômetro para controlar o servo motor na junta do "cotovelo" do braço robótico.

## Passo 2
Para começar, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abrirá e selecione a biblioteca.

## Passo 3
Nesse projeto, todo o código ficará dentro do laço ``||Basic:sempre||``, localizado na aba ``||Basic:Básico||``.

```blocks
basic.forever(function () {
	
})
```

## Passo 4
Acesse a categoria ``||actuators:Atuadores||`` e adicione o bloco ``||actuators:Motor CC, parar motor na porta P8||``.
Altere a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
})
```

## Passo 5
Feito isso, retorne à aba ``||actuators:Atuadores||`` e adicione um comando ``||actuators:Servo Motor, definir posição 0 porta P8 modo knob||``. Modifique
a porta para ``||actuators:P16||``. 

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(0, OutputPorts.P16)
})
```

## Passo 6
Para controlar a posição desse servo motor, utilizaremos o Bit Potenciômetro. Portanto,
acesse a categoria ``||sensors:Sensores||`` e selecione o bloco ``||sensors:Valor do potenciômetro na porta P2||`` para 
substituir o valor **0** da posição do bloco do servo motor.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
})
```

## Passo 7
Agora, faremos o controle da rotação da base do braço robótico. Para isso, acesse a categoria
``||loops:Loops||`` e adicione o laço ``||loops:enquanto falso executar||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (false) {
    	
    }
})
```

## Passo 8
Feito isso, substitua o estado ``||logic:falso||`` pelo bloco de bordas triangulares ``||input:botão A é pressionado||`` localizado
na aba ``||input:Input||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
    	
    }
})
```

## Passo 9
Dentro do ``||loops:executar||`` utilizaremos o comando ``||actuators:Motor CC, definir velocidade 0 porta P8||``, localizado
na aba ``||actuators:Atuadores||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(0, OutputPorts.P8)
    }
})
```

## Passo 10
Modifique a velocidade para **100** e a porta para ``||actuators:P12||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
    }
})
```

## Passo 11
Agora, precisamos definir o sentido de rotação do motor CC na base. Para isso, adicione o laço de ``||logic:Lógica||``  
``||logic:se verdadeiro então||`` ainda dentro do laço ``||loops:executar||``. 

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (true) {
        	
        }
    }
})
```

## Passo 12
Retorne à categoria ``||logic:Lógica||`` e adicione o bloco comparador ``||logic:0 < 0||`` 
no lugar do ``||logic:verdadeiro||`` do teste condicional ``||logic:Se/Então||``.    

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (0 < 0) {
        	
        }
    }
})
```

## Passo 13
Feito isso, acesse a categoria ``||input:Input||`` e posicione o bloco de bordas redondas ``||input:aceleração (mg) x||``
no primeiro campo do ``||logic:comparador||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (input.acceleration(Dimension.X) < 0) {
        	
        }
    }
})
```

## Passo 14
Agora, dentro deste laço ``||logic:Se/Então||``, vamos definir o sentido de rotação do motor com o comando 
``||actuators:Motor CC, definir direção sentido horário porta P8||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (input.acceleration(Dimension.X) < 0) {
            actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        }
    }
})
```

## Passo 15
Altere o sentido para ``||actuators:anti-horário||``. Se, ao testar, seu braço estiver girando para o lado contrário
ao inclinar o Micro:bit, modifique o sentido neste bloco. 

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (input.acceleration(Dimension.X) < 0) {
            actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        }
    }
})
```

## Passo 16
Nesse momento, precisamos replicar a lógica para o motor girar no sentido inverso quando inclinarmos o Micro:bit 
para o outro lado. Para isso, com o botão direito do mouse, duplique todo o laço ``||logic:Se/Então||`` criado nos últimos passos, e 
o posicione **abaixo** do anterior, mas ainda dentro do laço ``||loops:executar||``.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (input.acceleration(Dimension.X) < 0) {
            actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        }
        if (input.acceleration(Dimension.X) < 0) {
            actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        }
    }
})
```

## Passo 17
Altere o sinal do ``||logic:comparador||`` de **<** para **>**.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (input.acceleration(Dimension.X) < 0) {
            actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        }
        if (input.acceleration(Dimension.X) > 0) {
            actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        }
    }
})
```

## Passo 18
Por fim, modifique o sentido do motor para ``||actuators:horário||``. Lembrando que, durante seus testes, se você alterar
do laço anterior, você deve alterar este também para que sejam sempre opostos um ao outro.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (input.acceleration(Dimension.X) < 0) {
            actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        }
        if (input.acceleration(Dimension.X) > 0) {
            actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        }
    }
})
```

## Passo 19
Agora é hora de testar! Ajuste a posição do Potenciômetro para controlar o cotovelo e incline o Micro:bit
**enquanto** pressiona o **botão A** do Micro:bit para girar a base. Se necessário, ajuste o sentido do motor nos 
laços condicionais.

```blocks
basic.forever(function () {
	
})
```

## Passo 20
Confira o seu código clicando na lâmpada de dica.

```blocks
basic.forever(function () {
    actuators.StopMotor(OutputPorts.P12)
    actuators.SetAngleServoKnob(sensors.dimmerValue(InputPorts.P2), OutputPorts.P16)
    while (input.buttonIsPressed(Button.A)) {
        actuators.SetSpeedMotor(100, OutputPorts.P12)
        if (input.acceleration(Dimension.X) < 0) {
            actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        }
        if (input.acceleration(Dimension.X) > 0) {
            actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        }
    }
})
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```