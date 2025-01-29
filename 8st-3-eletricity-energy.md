# Consumo de Energia

## Passo 1
Nesta atividade, vamos incrementar o programa de geração de energia para considerar o consumo da carga armazenada
ao ligarmos o ventilador que construímos. Certifique-se de utilizar o código construído na atividade anterior para começarmos.

```template
let Carga = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 2

Como de costume, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3

A primeira alteração do nosso programa será a criação de uma nova variável ``||Variables:Consumo||``. Acesse a aba 
``||Variables:Variáveis||`` para criá-la. Insira o bloco ``||Variables:definir Consumo para 0||`` na primeira posição dentro 
do laço ``||Basic:Sempre||``. 

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = 0
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 4

Vá aos blocos de ``||Math:Matemática||`` e adicione o comando ``||Math:arredonda 0||`` substituindo o **0** do bloco ``||Variables:definir Consumo para 0||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(0)
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 5

Retorne à aba ``||Math:Matemática||`` e insira o bloco de divisão ``||Math:0 / 0||`` dentro do ``||Math:arredonda 0||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(0 / 0)
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 6

No primeiro campo desta divisão, posicione o bloco ``||sensors:Valor do potenciômetro na porta P2||`` localizado na aba ``||sensors:Sensores||``. 
No segundo espaço, altere o valor de **0** para **6**. Este número determina o valor do consumo em relação à posição do Potenciômetro conectado na porta P2.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 7

Abaixo destes blocos, insira um laço ``||Logic:Se verdadeiro então   senão||``, localizado na aba ``||Logic:Lógica||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (true) {
    	
    } else {
    	
    }
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 8

Retorne à ``||Logic:Lógica||`` e substitua o campo ``||Logic:verdadeiro||`` por um bloco comparador ``||Logic:0 < 0||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (0 < 0) {
    	
    } else {
    	
    }
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 9

Altere os campos deste comparador para as variáveis ``||Variables:Carga||`` e ``||Variables:Consumo||``, chegando à comparação
``||Variables:Carga||`` ``||Logic:<||`` ``||Variables:Consumo||``. 

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
    	
    } else {
    	
    }
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 10

Dentro do laço ``||Logic:então||``, ou seja, quando a carga for menor que consumo, adicione o bloco ``||actuators:Motor CC, parar motor na porta P8||``,
localizado na aba ``||actuators:Atuadores||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
    } else {
    	
    }
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 11

Abaixo deste comando, ainda dentro do laço ``||Logic:então||``, inclua o bloco para ``||Variables:definir Consumo para 0||``, presente na 
seção de ``||Variables:Variáveis||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
    	
    }
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 12

Agora, dentro do laço ``||Logic:senão||``, vamos determinar que o Motor gire com a velocidade definida pelo Potenciômetro.
Para isso, inclua o bloco ``||actuators:Motor CC, definir velocidade 0 do motor na porta P8||``. Substitua o **0** pelo ``||sensors:Valor do potenciômetro na porta P2||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
        actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
    }
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 13

Feito isso, acesse a aba ``||Math:Matemática||`` e selecione o bloco de subtração ``||Math:0 - 0||``. Posicione-o dentro do 
bloco ``||Math:constrain Carga + Nível de Luz||`` substituindo o valor ``||Input:nível de luz||`` temporariamente. 

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
        actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
    }
    Carga = Math.constrain(Carga + (0 - 0), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 14

Volte com o valor ``||Input:nível de luz||`` substituindo o primeiro **0** para termos ``||Math:constrain Carga + Nível de Luz - 0||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
        actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
    }
    Carga = Math.constrain(Carga + (input.lightLevel() - 0), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 15

No último **0** da subtração, insira a variável ``||Variables:Consumo|``. Assim, garantimos que a carga seja drenada pelo valor de consumo do ventilador.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
        actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
    }
    Carga = Math.constrain(Carga + (input.lightLevel() - Consumo), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga)
    )
    basic.pause(2000)
})
```

## Passo 16

Agora, vamos ajustar as tabelas de ``||table:Registro de dados||``. Dentro do laço ``||Basic:no iniciar|``, clique no sinal de **+** para adicionar a 
coluna **"Consumo"**.

```blocks
table.setColumnTitles(
"Luz",
"Carga",
"Consumo"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
```

## Passo 17

Em seguida, no bloco ``||table:Registrar dados coluna...||``, inserido no laço ``||Basic:sempre|``, clique no sinal de **+** para adicionar 
mais uma coluna na tabela. Retorne à aba ``||table:Registro de dados||`` e inclua o bloco redondo ``||table:coluna " " valor 0||``.

 **Atenção:** Se você não fizer este último passo, não conseguirá alterar os valores da nova coluna.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga",
"Consumo"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
        actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
    }
    Carga = Math.constrain(Carga + (input.lightLevel() - Consumo), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga),
    table.createCell("", 0)
    )
    basic.pause(2000)
})
```

## Passo 18
Por fim, altere o nome da coluna para ``||table:Consumo||`` e o respectivo valor da variável ``||Variables:Consumo||``.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga",
"Consumo"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
        actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
    }
    Carga = Math.constrain(Carga + (input.lightLevel() - Consumo), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga),
    table.createCell("Consumo", Consumo)
    )
    basic.pause(2000)
})
```

## Passo 19

Legal! Finalmente, seu código pode ser testado. Passe para o Micro:bit, deixe a luz carregar o armazenamento e, em seguida, ligue o ventilador.
 
 Depois disso, impeça que a luz chegue nos LEDs do Micro:bit para a carga ser drenada pelo ventilador. Observe se este vai parar quando a carga se esgotar.

```blocks
let Carga = 0
let Consumo = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
table.setColumnTitles(
"Luz",
"Carga",
"Consumo"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Consumo = Math.round(sensors.dimmerValue(InputPorts.P2) / 6)
    if (Carga < Consumo) {
        actuators.StopMotor(OutputPorts.P8)
        Consumo = 0
    } else {
        actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
    }
    Carga = Math.constrain(Carga + (input.lightLevel() - Consumo), 0, 4000)
    led.plotBarGraph(
    Carga,
    4000
    )
    table.log(
    table.createCell("Luz", input.lightLevel()),
    table.createCell("Carga", Carga),
    table.createCell("Consumo", Consumo)
    )
    basic.pause(2000)
})
```

## Passo 20

Para visualizar os dados registrados, conecte o Micro:bit ao computador por meio de um cabo USB. 
O Micro:bit será exibido como uma unidade de armazenamento (pendrive). Em seguida, abra a pasta 
do Mircro:bit que irá aparecer, clique duas vezes em **MY_DATA.HTM**.
Para ver esse dados em um gráfico, basta clicar em **Visual preview**.


```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```