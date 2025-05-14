### @diffs true
# Caminhão de Lixo Autônomo

## Passo 1
Neste tutorial, vamos criar um programa para tornar um caminhão de lixo um veículo autônomo, capaz de identificar lixeiras
e parar seu movimento para que elas possam ser coletadas por agentes. Nessa primeira etapa, o caminhão deverá:

 - Andar para frente com uma velocidade de 350;

 - Se o infravermelho identificar uma lixeira próxima, então:

 - Caminhão para de andar por 1 segundo;

 - O caminhão volta a andar lentamente (velocidade de 150) por 2 segundos, para que a caçamba do caminhão fique mais próxima da lixeira;

 - Caminhão para de andar novamente e aguarda 5 segundos para que os coletores peguem a lixeira;

 - Caminhão volta a andar para frente até encontrar outra lixeira.

## Passo 2
Para começar, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3
Acesse o menu ``||basic:Básico||`` e insira um laço ``||basic:sempre||`` caso ele ainda não esteja em sua área de trabalho.
Em seguida, vá até a aba ``||actuators:Atuadores||`` e selecione o comando ``||actuators:Motor CC, definir velocidade 0 na porta P8||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(0, OutputPorts.P8)
})
```

## Passo 4 
Altere o valor da velocidade de **0** para **350** e a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
})
```

## Passo 5 
Acesse a aba ``||logic:Lógica||`` e inclua o laço ``||logic:Se verdadeiro então||`` dentro do laço ``||basic:sempre||``. 
Retorne à ``||logic:Lógica||`` e selecione o bloco triangular comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do laço 
``||logic:se-então||``, substituindo a palavra ``||logic:verdadeiro||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (0 == 0) {
    	
    }
})
```

## Passo 6
Agora, acesse a aba ``||sensors:Sensores||`` e adicione o bloco ``||sensors:Valor do sensor infravermelho na porta P2||`` e
use-o para substituir o primeiro **0**.
Altere o segundo **0** para **300** e o sinal de ``||logic:=||`` para ``||logic:>||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
    	
    }
})
```

## Passo 7
Nesse momento, vamos programar o comportamento do caminhão ao identificar uma lixeira, posicionando os blocos
dentro do ``||logic:então||`` do laço de lógica condicional. Comece retornando à ``||actuators:Atuadores||`` e 
selecionando o comando ``||actuators:Motor CC, parar na porta P8||``. Altere a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
    }
})
```

## Passo 8
Acesse o menu ``||basic:Básico||`` e insira um bloco ``||basic:pausa (ms)||``. Modifique sua duração para **1 segundo** (1000 ms).

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
    }
})
```

## Passo 9
Novamente no menu ``||actuators:Atuadores||``, adicione o bloco ``||actuators:Motor CC, definir velocidade 0 na porta P8||``. 
Modifique a velocidade de **0** para **150** e a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
    }
})
```

## Passo 10
Volte ao menu ``||basic:Básico||`` e adicione um bloco ``||basic:pausa (ms)||``. Modifique sua duração para **2 segundos** (2000 ms).
Assim, o caminhão se aproximará lentamente da lixeira.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
    }
})
```

## Passo 11
Volte à ``||actuators:Atuadores||`` e selecione o comando ``||actuators:Motor CC, parar na porta P8||``. 
Altere a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
    }
})
```

## Passo 12
Adicione outra ``||basic:pausa (ms)||``. Modifique sua duração para **5 segundos** (5000 ms).

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(350, OutputPorts.P12)
    if (sensors.infraredValue(InputPorts.P2) > 300) {
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(1000)
        actuators.SetSpeedMotor(150, OutputPorts.P12)
        basic.pause(2000)
        actuators.StopMotor(OutputPorts.P12)
        basic.pause(5000)
    }
})
```

## Passo 13
Por fim, no menu ``||actuators:Atuadores||``, adicione o bloco ``||actuators:Motor CC, definir velocidade 0 na porta P8||``. 
Modifique a velocidade de **0** para **350** e a porta de ``||actuators:P8||`` para ``||actuators:P12||``.

```blocks
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

## Passo 14
Agora seu código está pronto! Baixe-o para o micro:bit.
 
 Encaixe o conector Speed do Motor CC na porta P12 e teste o movimento e identificação
 das lixeiras pelo caminhão. Se necessário, ajuste as pausas e velocidades de cada trecho do movimento.
```blocks
```

## Passo 15
Se necessário, confira o seu código clicando na lâmpada de dica.

```blocks
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

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```