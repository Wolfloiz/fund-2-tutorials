# Monitoramento de Temperatura

## Passo 1 
Neste tutorial, você irá utilizar o Micro:Bit para registrar os dados de temperatura
e mostrá-los em um gráfico.

## Passo 2
Para começar, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3
Agora, acesse a aba ``||table:Registro de dados||``, selecione o comando ``||table: deletar registros||`` e
posicione-o dentro de um laço ``||input: no botão A+B pressionado||`` localizado na aba ``||input:Input||``. Esse comando vai apagar os registros salvos em seu Micro:bit ao pressionar os botões ``||input: botões A e B||`` simultaneamente. 
Recomendamos fazer isso sempre que for iniciar um novo teste para impedir que seus dados fiquem poluídos com informações de testes anteriores.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
```

## Passo 4
Acesse a aba ``||basic:Básico||`` e selecione o comando ``||basic:mostrar ícone||``.
Arraste-o para dentro do laço ``||basic:no iniciar||`` e altere o ícone para o sinal de "check".
Esse símbolo será exibido na matriz de LEDs e mostra que o Micro:Bit está em funcionamento.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
basic.showIcon(IconNames.Yes)
```

## Passo 5
Em seguida, adicione o comando ``||basic:pausar||`` no laço ``||basic:no iniciar||`` após o ícone de "check" e
defina o tempo de espera para 1000 milissegundos (1 segundo).

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
basic.showIcon(IconNames.Yes)
basic.pause(1000)
```

## Passo 6
Agora, acesse o comando ``||basic:limpar tela||`` e adicione-o também no laço ``||basic:no iniciar||`` para
que a tela seja apagado após a pausa.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
```

## Passo 7
Agora, vamos dar o nome à coluna que queremos registrar dados. Para isso, acesse a aba
``||table:Registro de Dados||``, selecione o comando ``||table:Adicionar colunas ao registro de dados " "||`` e posicione-o dentro do laço ``||basic:no iniciar||``, logo abaixo do comando ``||basic:limpar tela||``.

Dê o nome de **Temperatura** à coluna de dados.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
table.setColumnTitles("Temperatura")
```

## Passo 8
Primeiro, vá até a aba ``||basic:Básico||``e selecione o laço``||basic:Sempre||``, caso ele
não esteja na área de trabalho. Em seguida, retorne a aba``||basic:Básico||``, selecione o 
comando ``||basic: pausa (ms) 100||`` e adicione no laço. 

Altere o tempo de pausa para **2000** (2 segundos). Esse tempo é a frequência que o 
Micro:bit irá fazer a leitura da temperatura. 

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
table.setColumnTitles("Temperatura")
basic.forever(function () {
    basic.pause(2000)
})
```
## Passo 9
Acesse novamente a aba ``||table:Registro de Dados||``, selecione o comando 
``||table:Registrar dados coluna " " valor 0||`` e posicione-o abaixo da ``||basic:pausa||``, 
dentro do laço ``||basic:sempre||``.

Selecione **Temperatura** dentro do primeiro espaço circular, que faz referência à coluna. 

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
table.setColumnTitles("Temperatura")
basic.forever(function () {
    basic.pause(2000)
    table.log(table.createCell("Temperatura", 0))
})
```

## Passo 10
Pra finalizar, vá até a aba ``||input:Input||`` selecione a entrada ``||input:Temperatura (°C)||``
e posicione-o no segundo campo circular em frente a *valor*. 

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
basic.showIcon(IconNames.Yes)
basic.pause(1000)
basic.clearScreen()
table.setColumnTitles("Temperatura")
basic.forever(function () {
    basic.pause(2000)
    table.log(table.createCell("Temperatura", input.temperature()))
})
```
## Passo 11
Pronto! Agora você já pode baixar o código para o Micro:bit e testar seu código.

## Passo 12
Para visualizar os dados registrados, conecte o Micro:bit ao computador por meio de um cabo USB. 
O Micro:bit será exibido como uma unidade de armazenamento (pendrive). Em seguida, abra a pasta 
do Mircro:bit que irá aparecer, clique duas vezes em **MY_DATA.HTM**. Nessa pasta você pode visualizar 
os dados em uma tabela de duas colunas com a temperatura medida e o tempo correspondente.
Para ver esse dados em um gráfico, basta clicar em **Visual preview**.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```
