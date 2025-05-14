### @diffs true
# Separador de Alimentos

## Passo 1
Neste tutorial, vamos programar o Micro:bit para receber a resposta da rede neural treinada no Teachable Machine via comunicação serial.
Essa resposta será usada para acionar o Servo Motor do Separador de Alimentos que direcionará qual recipiente receberá a esfera de isopor (ou outro objeto)
reconhecida. 
## Passo 2
Para começar, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3
Clique no menu ``||Advanced:Avançado||``, acesse ``||serial:Serial||`` e adicione o comando ``||serial:serial redirecionar para USB||``
dentro do laço ``||basic:no iniciar||``. Se esse laço ``||basic:no iniciar||`` não estiver em seu código ainda, encontre-o na aba 
``||basic:Básico||``.

 Esse código vai configurar o Micro:bit para utilizar a comunicação serial através de sua conexão USB com o computador.

```blocks
serial.redirectToUSB()
```

## Passo 4 
Novamente, acesse o menu ``||basic:Básico||`` e adicione o laço ``||basic:sempre||`` ao seu código. Em seguida, 
insira o comando ``||actuators:Servo, definir posição 0 porta P8 modo knob||``. Altere a posição de **0** para **455** e a 
porta de ``||actuators:P8||`` para ``||actuators:P16||``. 

```blocks
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
})
```

## Passo 5
Acesse o menu ``||variables:Variáveis||``, clique em **"Fazer uma variável"** e nomeie-a como ``||variables:Alimento||``.
Depois de criada, inclua o seu bloco de definição ``||variables:definir Alimento para 0||`` no laço ``||basic:sempre||``.

```blocks
let Alimento = 0
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = 0
})
```

## Passo 6
Volte em ``||Advanced:Avançado||``, acesse ``||serial:Serial||`` e escolha o bloco de bordas arredondadas
``||serial:serial ler até new line()||``. 

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
})
```  

## Passo 7
Em seguida, clique no menu ``||logic:Lógica||`` e adicione o laço condicional ``||logic:se verdadeiro então||``.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (true) {
    	
    }
})
```

## Passo 8
Retorne ao menu ``||logic:Lógica||`` e selecione o bloco comparador ``||logic:0 = 0||`` para substituir o ``||logic:verdadeiro||`` do 
laço ``||logic:se verdadeiro então||``.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (0 == 0) {
    	
    }
})
```

## Passo 9
Agora, vamos preencher os campos do comparador. Primeiramente, acesse o menu ``||variables:Variáveis||`` e use o bloco de bordas
redondas ``||variables:Alimento||`` no primeiro campo do comparador. Para o segundo valor, precisamos transformar o campo em ``||text:Texto||``.
Para isso, volte em ``||Advanced:Avançado||`` e coloque o bloco de aspas duplas ``||text:" "||`` no comparador.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "") {
    	
    }
})
```

## Passo 10
Clique entre as aspas duplas e digite a palavra ``||text:maduro||``.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
    	
    }
})
```

## Passo 11
Dentro do laço ``||logic:então||``, adicione uma ``||basic:pausa (ms)||`` localizada na aba ``||basic:Básico||``.   
Altere sua duração de **100ms** para **1000ms** (1 segundo).

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
        basic.pause(1000)
    }
})
```

## Passo 12
Com o botão direito do mouse, duplique o bloco ``||actuators:Servo, definir posição 455 porta P16 modo knob||`` que adicionamos 
no início do laço ``||basic:sempre||``. Coloque o bloco duplicado abaixo da ``||basic:pausa (ms)||``, ainda dentro do laço ``||logic:então||``.
Modifique o valor da posição de **455** para **1023**.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
    }
})
```

## Passo 13
Finalize esse ``||logic:então||`` com outra ``||basic:pausa (ms)||`` de 1 segundo (1000 ms).

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
        basic.pause(1000)
    }
})
```

## Passo 14
Agora, vamos replicar a lógica para quando a rede neural identificar um alimento verde.
Portanto, clique com o botão direito do mouse sobre o laço ``||logic:se então||`` inteiro e duplique-o, posicionando-o 
exatamente abaixo do anterior, não dentro.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
        basic.pause(1000)
    }
    if (Alimento == "maduro") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
        basic.pause(1000)
    }
})
```

## Passo 15
Clique entre as aspas e substitua a palavra ``||text:maduro||`` por ``||text:verde||``.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
        basic.pause(1000)
    }
    if (Alimento == "verde") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
        basic.pause(1000)
    }
})
```

## Passo 16
Por fim, modifique o valor da posição do  ``||actuators:servo||`` de **1023** para **0**.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
        basic.pause(1000)
    }
    if (Alimento == "verde") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(0, OutputPorts.P16)
        basic.pause(1000)
    }
})
```

## Passo 17
Agora seu código está pronto! Baixe-o para o micro:bit, teste a identificação do Teachable Machine e, 
posteriormente, o acionamento do servo de acordo com o objeto identificado. Se necessário,
refine o treinamento da rede neural para tornar a identificação mais robusta.

```blocks
```

## Passo 18
Se necessário, confira o seu código clicando na lâmpada de dica.

```blocks
let Alimento = ""
serial.redirectToUSB()
basic.forever(function () {
    actuators.SetAngleServoKnob(455, OutputPorts.P16)
    Alimento = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    if (Alimento == "maduro") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
        basic.pause(1000)
    }
    if (Alimento == "verde") {
        basic.pause(1000)
        actuators.SetAngleServoKnob(0, OutputPorts.P16)
        basic.pause(1000)
    }
})
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```