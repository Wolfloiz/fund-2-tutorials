# Monitoramento de Temperatura

## Step 1 
Neste tutorial, você irá utilizar o Micro:Bit para registrar os dados de temperatura
e mostrá-los em um gráfico.

## Step 2
Primeiro, importe a biblioteca **Datalogger** para habilitar sua aba. Para isso, 
clique na aba __+Extensões__, digite *Datalogger* no campo de pesquisa e selecione a biblioteca.

## Step 3
Acesse a aba ``||basic:Básico||`` e selecione o comando ``||basic:mostrar ícone||``.
Arraste-o para dentro do laço ``||basic:no iniciar||`` e altere o ícone para o sinal de "check" (✔).
Esse símbolo será exibido na matriz de LEDs e mostra que o Micro:Bit está em funcionamento.

```blocks
basic.showIcon(IconNames.Yes)
```

## Step 4
Em seguida, adicione o comando ``||basic:pausar||`` no laço ``||basic:no iniciar||`` após o ícone de "check" e
defina o tempo de espera para 1000 milissegundos (1 segundo).

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(1000)
```

## Step 5
Agora, acesse o comando ``||basic:limpar tela||`` e adicione-o também no laço ``||basic:no iniciar||`` para
que o display seja apagado após a pausa.

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
```

## Step 6
Agora, vamos dar o nome à coluna que queremos resgatar dados. Para isso, acesse a aba
``||datalogger:Data Logger||``, selecione o comando  ``||datalogger:set Columns " "||``e posicione-o dentro do laço ``||basic:no iniciar||``, logo abaixo do comando ``||basic:limpar tela||``.

Dê o nome de **Temperatura** à coluna de dados.

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
datalogger.setColumnTitles("Temperatura")
```

## Step 7
Primeiro, vá até a aba ``||basic:Básico||``e selecione o laço``||basic:Sempre||``, caso ele
não esteja na área de trabalho. Em seguida, retorne a aba``||basic:Básico||``, selecione o 
comando ``||basic: pausa (ms) 100||`` e adicione no laço. 

Altere o tempo de pausa para **2000** (2 segundos). Esse tempo é a frequência que o 
Micro:bit irá fazer a leitura da temperatura. 

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
datalogger.setColumnTitles("Temperatura")
basic.forever(function () {
    basic.pause(2000)
})
```
## Step 8
Acesse novamente a aba ``||datalogger:Data Logger||``, selecione o comando 
``||datalogger:log data column " " value 0||`` e posicione-o abaixo da ``||basic:pausa||``, 
dentro do laço ``||basic:sempre||``.

Selecione **Temperatura** dentro do primeiro espaço circular, que faz referência à coluna. 

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
datalogger.setColumnTitles("Temperatura")
basic.forever(function () {
    basic.pause(2000)
    datalogger.log(datalogger.createCV("Temperatura", 0))
})
```

## Step 9
Pra finalizar, vá até a aba ``||input:Input||`` selecione a entrada ``||input:Temperatura (°C)||``
e posicione-o no segundo campo circular em frente a *value*. 

```blocks
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
datalogger.setColumnTitles("Temperatura")
basic.forever(function () {
    basic.pause(2000)
    datalogger.log(datalogger.createCV("Temperatura", input.temperature()))
})
```
## Step 10
Pronto! Agora você já pode baixar o código para o Micro:bit e testar seu código.

## Step 11
Para visualizar os dados registrados, conecte o Micro:bit ao computador por meio de um cabo USB. 
O Micro:bit será exibido como uma unidade de armazenamento (pendrive). Em seguida,abra a pasta 
do Mircro:bit que irá aparecer, clique duas vezes em **MY_DATA.HTM** Nessa pasta você pode visualizar 
os dados em uma tabela de duas colunas com a temperatura medida e o tempo correspondente.
Para ver esse dados em um gráfico, basta clicar em **Visual preview**.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```