# Estação Meteorológica

## Step 1
Neste tutorial, vamos criar uma estação meteorológica simples no Micro:bit! Ao iniciar, a placa
mostrará um ícone de "check" por alguns segundos. Em seguida, ao pressionar o botão A, o dispositivo
exibirá o nível de luminosidade, e ao pressionar o botão B, exibirá a temperatura.

## Step 2
Primeiro, acesse a aba ``||basic:Básico||`` e selecione o comando ``||basic:mostrar ícone||``.
Arraste-o para dentro do laço ``||basic:no iniciar||`` e altere o ícone para o sinal de "check" (✔).
Esse símbolo será exibido na matriz de LEDs e mostra que o Micro:Bit está em funcionamento.

```blocks
basic.showIcon(IconNames.Yes)
```
## Step 3
Em seguida, adicione o comando ``||basic:pausar||`` no laço ``||basic:no iniciar||`` após o ícone de "check" e
defina o tempo de espera para **2000 milissegundos** (2 segundos).

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(2000)
```
## Step 4
Agora, acesse o comando ``||basic:limpar tela||`` e adicione-o também no laço ``||basic:no iniciar||`` para
que o display seja apagado após a pausa.

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(2000)
basic.clearScreen()
```
## Step 5
Acesse a aba ``||input:Input||`` e adicione dois laços ``||input:no botão A pressionado||``. Em seguida, 
altere um deles de botão A para botão B.

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(2000)
basic.clearScreen()
input.onButtonPressed(Button.A, function () {
})
input.onButtonPressed(Button.B, function () {
})
```
## Step 6
Vá até a aba ``||basic: Básico||`` e selecione o comando ``||basic:mostrar número||``.
Duplique o comando e insira um no laço ``||input:no botão A pressionado||`` e outro 
no ``||input:no botão B pressionado||``.

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(2000)
basic.clearScreen()
input.onButtonPressed(Button.A, function () {
    basic.showNumber(0)
})
input.onButtonPressed(Button.B, function () {
    basic.showNumber(0)
})
```
## Step 7
Em seguida, precisamos pegar o valor da luminosidade. O Micro:bit utiliza a próprima
matriz de LEDS como sensor de luz. Para utilizá-lo, vá até a aba ``||input:Input||``,
selecione o bloco ``||input:nível de luz||`` e posicione-o dentro do espaço circular
do comando ``||basic:mostrar número||``.

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(2000)
basic.clearScreen()
input.onButtonPressed(Button.A, function () {
    basic.showNumber(input.lightLevel())
})
input.onButtonPressed(Button.B, function () {
    basic.showNumber(0)
})
```
## Step 8
Agora, precisamos pegar o valor da temperatura. A boa notícia é que o próprio Micro:bit 
já possui um sensor de temperatura integrado. Para utilizá-lo, vá até a aba 
``||input:Input||``, selecione o bloco circular ``||input:temperatura||`` e posicione-o 
dentro do espaço circular do comando ``||basic:mostrar número||``, substituindo o número **0**.

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(2000)
basic.clearScreen()
input.onButtonPressed(Button.A, function () {
    basic.showNumber(input.lightLevel())
})
input.onButtonPressed(Button.B, function () {
    basic.showNumber(input.temperature())
})
```
## Step 9
Pronto! Você já pode carregar seu código para o micro:bit e testar a Estação Meteorológica!

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```