# Misturador de substâncias

## Step 1
Neste tutorial, vamos criar um misturador de substâncias que utiliza o potenciômetro para
controlar a velocidade de um motor.

## Step 2
Primeiro, importe a biblioteca da Fuzzy para habilitar as abas ``||Actuators:Atuadores||`` e ``||sensors:Sensores||``.
Para isso, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Step 3
Agora, acesse a aba ``||actuators:Atuadores||``, selecione o comando ``||actuators:Motor CC, definir velocidade 0 do motor na porta P8||`` e
posicione-o dentro do laço ``||basic:sempre||``. Esse comando permite ajustar a velocidade do motor conforme o valor captado
pelo potenciômetro.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(0, OutputPorts.P8)
})
```
## Step 4
Na aba ``||sensors:Sensores||``, selecione o comando ``||sensors:valor do potenciômetro na porta P2||`` e substitua o **0** que está
dentro do espaço circular do comando ``||actuators:Motor CC, definir velocidade 0 do motor na porta P8||``.

```blocks
basic.forever(function () {
    actuators.SetSpeedMotor(sensors.dimmerValue(InputPorts.P2), OutputPorts.P8)
})
```
## step 5
Pronto! Você já pode carregar seu código para o Micro:bit e testá-lo no projeto.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```