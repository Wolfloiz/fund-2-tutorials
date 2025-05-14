### @diffs true
# Coleta de Lixo Automatizada

## Passo 1
Neste tutorial, vamos evoluir o projeto do caminhão de lixo para que ele possa realizar a coleta das lixeiras
automaticamente utilizando a haste conectada ao Servo Motor. Nesse novo código, o caminhão deve:

 - No início, colocamos o coletor de lixo (servo) para cima (posição 445);

 - O caminhão anda para frente com uma velocidade de 350;

 - Se o infravermelho identificar uma lixeira próxima:

 - Caminhão para de andar por 1 segundo;

 - Coletor desce até ficar paralelo ao chão (posição 115) e o caminhão anda lentamente (velocidade de 150) por 2 segundos, para que o coletor encaixe na tampa da lixeira;

 - Caminhão para de andar e uma variável chamada "posição" é criada para armazenar a posição do servo. Como a posição atual é de 115, o valor inicial de posição será 115;

 - Um loop é criado para aumentar o valor da posição de 2 em 2 sucessivamente até chegar à posição 445. Dessa forma, o coletor leva a lixeira até a caçamba lentamente;

 - O lixo é descartado na caçamba por 2 segundos;

 - Um outro loop é criado para diminuir o valor da posição de 2 em 2 até chegar à posição 115. Assim, o coletor leva a lixeira de volta ao chão lentamente;

 - Depois de 1 segundo, o caminhão volta a andar lentamente para trás por 2 segundos, para desencaixar o coletor da lixeira;

 - O caminhão para e o coletor sobe para sua posição inicial (445);

 - Caminhão volta a andar (velocidade 350) para frente até encontrar outra lixeira.

```template
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 2
Como de costume, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3
O primeiro objetivo será configurar a posição inicial da haste coletora. Para isso, acesse o menu ``||basic:Básico||`` e insira um laço ``||basic:no iniciar||`` 
caso ele ainda não esteja em sua área de trabalho.
Em seguida, vá até a aba ``||actuators:Atuadores||`` e selecione o comando ``||actuators:Servo, definir posição 0 na porta P8 modo knob||``.

```blocks
actuators.SetAngleServoKnob(0, OutputPorts.P8)
```

## Passo 4 
Altere o valor da posição de **0** para **445** e a porta de ``||actuators:P8||`` para ``||actuators:P16||``.

```blocks
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 5 
Agora, vamos realizar as alterações dentro do laço principal ``||basic:sempre||``. Acesse o menu
``||variables:Variáveis||`` e clique em **"Fazer uma variável"** e nomeie-a como "Posicao".
Feito isso, volte ao menu ``||variables:Variáveis||`` e posicione o bloco ``||variables:definir posicao para 0||`` após a primeira
``||basic:pausa (ms) 1000||`` de 1000(ms) do laço ``||basic:sempre||``.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 0
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 6
Certifique-se de alterar o valor de definição da ``||variables:Posicao||`` de **0** para **115**. 

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 7
Retorne à aba ``||actuators:Atuadores||`` e encaixe o comando ``||actuators:Servo, definir posição 0 porta P8 modo knob||`` abaixo do bloco
de definição da variável do passo anterior. Altere o valor de **0** para o valor da variável ``||variables:Posicao||``.
Esse bloco é encontrado na aba ``||variables:Variáveis||`` e possui as bordas redondas. Por fim, modifique a porta de ``||actuators:P8||`` para ``||actuators:P16||``.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 8
Feito isso, acesse o menu ``||loops:Loops||`` e adicione um laço ``||loops:enquanto falso executar||`` abaixo do bloco
``||actuators:Motor CC, para motor na porta P12||`` que já estava no código antigo do caminhão. 

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (false) {
        	
        }
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 9
Acesse o menu ``||Logic:Lógica||`` e selecione o bloco comparador, de bordas triangulares, ``||logic:0 < 0||``.
Substitua o campo ``||loops:falso||`` do laço ``||loops:enquanto||``.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (0 < 0) {
        	
        }
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 10
Preencha esse comparador com a variável ``||variables:Posicao||`` no primeiro campo e o valor **445** no segundo campo.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
        	
        }
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 11
Retorne ao menu ``||variables:Variáveis||`` e adicione o bloco ``||variables:alterar Posicao por 1||`` dentro do
laço ``||loops:executar||``. Altere o valor do bloco de **1** para **2**.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
        }
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 12
Com o botão direito do mouse, duplique o bloco ``||actuators:Servo, definir posição||`` ``||variables:Posicao||`` ``||actuators:porta P16 modo knob||``,
que adicionamos no **passo 7**, e posicione-o dentro do laço ``||loops:executar||``. Em seguida, abaixo desse comando,
adicione um bloco ``||basic:pausa (ms)||`` alterando seu valor para **10ms**.  

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(5000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 13
Agora, fora do laço ``||loops:executar||``, modifique o valor da ``||basic:pausa (ms)||`` que já estava no código antigo
de **5000 ms** para **2000 ms** (2 segundos).

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 14
Com o botão direito do mouse, duplique todo o laço ``||loops:enquanto||`` que configuramos anteriormente e posicione-o 
**exatamente** abaixo dessa ``||basic:pausa (ms)||`` de 2 segundos. Modifique o sinal do comparador de ``||logic:<||`` para ``||logic:>||``
e o valor de **445** para **115**.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 15
Dentro desse novo laço ``||loops:executar||``, edite o valor de alteração do bloco ``||variables:alterar Posicao por 2||`` de
**2** para **-2** (negativo).

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 16
Após esse laço ``||loops:executar||``, adicione uma  ``||basic:pausa (ms)||`` de 500ms. 

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 17
Neste momento, o caminhão já posicionou a lixeira na calçada novamente e deve andar para trás, para desacoplar a haste coletora.
Para isso, acesse o menu ``||actuators:Atuadores||`` e posicione o bloco ``||actuators:Motor CC, definir direção para sentido horário na porta P8||`` abaixo da 
``||basic:pausa (ms)||`` adicionada no passo anterior. Modifique o sentido de  ``||actuators:horário||`` para ``||actuators:anti-horário||``. 

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 18
Edite a velocidade do bloco ``||actuators:Motor CC, definir velocidade 350 na porta P12||`` que herdamos da atividade anterior de 
**350** para **150**.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
    }
})
```

## Passo 19
Adicione outra  ``||basic:pausa (ms)||`` de **2 segundos** (2000 ms).

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
    }
})
```

## Passo 20
Volte à aba ``||actuators:Atuadores||`` e selecione o comando ``||actuators:Motor CC parar motor na porta P8||``. Altere a 
porta de ``||actuators:P8||`` para ``||actuators:P12||``.   

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
    }
})
```

## Passo 21
Agora, devemos retornar a haste coletora à sua posição inicial. Para isso, adicione o bloco 
``||actuators:Servo, definir posição 0 porta P8 modo knob||``. Altere a posição de **0** para **445** e
a porta de ``||actuators:P8||`` para ``||actuators:P16||``.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetAngleServoKnob(445, OutputPorts.P16)
    }
})
```

## Passo 22
Com o botão direito, duplique o bloco ``||actuators:Motor CC, definir direção para sentido anti-horário na porta P8||`` adicionado anteriormente 
no passo 17. Altere o sentido de ``||actuators:anti-horário||`` para ``||actuators:horário||``.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetAngleServoKnob(445, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
    }
})
```

## Passo 23
Por fim, adicione um bloco ``||actuators:Motor CC, definir velocidade 0 na porta P8||`` certificando-se de alterar
a velocidade de **0** para **350** e a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetAngleServoKnob(445, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

## Passo 24
Agora seu código está pronto! Baixe-o para o micro:bit.
 
 Encaixe o conector Speed do Motor CC na porta P12, o conector Dir na P8 e o servo na P16.
 Teste os movimentos e coleta das lixeiras pela haste. 
 Se necessário, ajuste as pausas, velocidades ou posições de cada trecho do movimento.
```blocks
```

## Passo 25
Se necessário, confira o seu código clicando na lâmpada de dica.

```blocks
let Posicao = 0
actuators.SetAngleServoKnob(445, OutputPorts.P16)
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        Posicao = 115
        actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        while (Posicao < 445) {
            Posicao += 2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(2000)
        while (Posicao > 115) {
            Posicao += -2
            actuators.SetAngleServoKnob(Posicao, OutputPorts.P16)
            basic.pause(10)
        }
        basic.pause(500)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        actuators.SetAngleServoKnob(445, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetSpeedMotor(350, OutputPorts.P12)
    }
})
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```
