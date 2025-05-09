### @diffs true
# Geração de Energia

## Passo 1
Neste tutorial, vamos criar um programa para simular o funcionamento de um painel solar, utilizando o Micro:bit para captar dados de luminosidade, 
calcular a carga armazenada e exibir essas informações de forma interativa.

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

Retorne à aba ``||table:Registro de dados||``, escolha o bloco ``||table:Adicionar colunas ao registro de dados " "||`` e
posicione-o dentro do laço ``||basic:no iniciar||``. Esse bloco cria a base da tabela onde registraremos os dados.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
table.setColumnTitles("")
basic.forever(function () {
	
})
```

## Passo 5
Precisamos nomear as colunas da nossa tabela. Para isso, clique no sinal de **+** dentro do bloco. 
Nomeie a primeira coluna como **"Luz"** e a segunda como **"Carga"**.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.forever(function () {
	
})
```
## Passo 6

Feito isso, vamos adicionar dois comandos para indicar ao usuário que nosso programa foi iniciado.
Vá até a aba ``||Basic:Básico||``, e selecione os blocos ``||Basic:mostrar ícone||`` e ``||Basic:pausa (ms)||``.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(100)
basic.forever(function () {
	
})
```

## Passo 7

Edite o ícone que você deseja exibir e altere a duração da pausa para determinar por quanto tempo ele será exibido
antes de iniciarmos a operação do Painel Solar. 

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
	
})
```

## Passo 8

Agora, vamos criar uma variável denominada ``||Variables:Carga||``. Acesse a seção ``||Variables:Variáveis||`` e clique em **Fazer uma variável**.
Depois de criada, retorne à ``||Variables:Variáveis||`` e adicione o bloco  ``||Variables:definir Carga para 0||`` dentro do laço ``||Basic:Sempre||``.

```blocks
let Carga = 0
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
})
table.setColumnTitles(
"Luz",
"Carga"
)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.forever(function () {
    Carga = 0
})
```

## Passo 9

Aproveite para também inserir o comando ``||Variables:definir Carga para 0||`` dentro do laço ``||input: no botão A+B pressionado||``,
onde apagamos os registro de dados. Assim, vamos garantir que o cálculo da carga também seja reiniciado.  

```blocks
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
    Carga = 0
})
```

## Passo 10

Essa variável ``||Variables:Carga||`` possui algumas características especiais. Primeiramente, ela nunca
poderá ser menor que zero. Ao mesmo tempo, queremos simular um caso em que a carga atinja um nível máximo, 
aproximando nosso protótipo de um Painel Solar conectado a uma bateria real e evitando os casos em que a carga
aumentaria até um valor alto demais para testarmos posteriormente.

## Passo 11

Para atender tais condições, podemos usar o bloco ``||Math:constrain 0 between 0 and 0||``, localizado na 
aba ``||Math:Matemática||``. Ele limita uma determinada variável em um intervalo definido pelos dois campos redondos do bloco.
Posicione-o dentro do campo de valor do comando ``||Variables:definir Cara para 0||``, substituindo este **0**.

```blocks
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
    Carga = Math.constrain(0, 0, 0)
})
```

## Passo 12

Agora, vamos preencher esse comando com seus parâmetros. No primeiro campo, insira o bloco de adição ``||Math:0 + 0||``, presente na aba ``||Math:Matemática||``.

```blocks
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
    Carga = Math.constrain(0 + 0, 0, 0)
})
```

## Passo 13

Na primeira parcela desta adição, vamos inserir a própria variável ``||Variables:Carga||``. Na segunda parcela, 
utilizaremos o valor ``||Input:Nível de Luz||`` localizado na aba ``||Input:Input||``. O valor deste nível de luz é medido 
pelo próprio Micro:bit e pode variar entre **0** e **255**.

```blocks
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
    Carga = Math.constrain(Carga + input.lightLevel(), 0, 0)
})
```

## Passo 14

Em seguida, vamos limitar o resultado dessa soma entre **0** e **4000** preenchendo os dois últimos campos de valores deste bloco.
Então, o que fizemos foi garantir que o valor de carga armazenado, mais o valor de luz medido naquela iteração será limitado entre 0 e 4000.

```blocks
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
})
```

## Passo 15

Agora, vamos usar a tela de LEDs do Micro:bit para ilustrar o nível de carga armazenado pelo Painel Solar.
Para isso, acesse a aba ``||Led:Led||`` e adicione o comando ``||Led:plot bar graph of 0 up to 0||`` no laço ``||Basic:Sempre||``.

```blocks
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
    0,
    0
    )
})
```

## Passo 16

Defina a variável ``||Variables:Carga||`` como o valor a ser plotado substituindo o primeiro **0** deste bloco e,
em seguida, altere o outro **0** para o valor limite de **4000** que estabelecemos anteriormente. 

```blocks
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
})
```

## Passo 17

Retorne à aba ``||table:Registro de Dados||`` e selecione o bloco ``||table:Registrar dados coluna " " valor 0||``. **Clique** no campo destinado ao 
nome da coluna e selecione a coluna ``||table:Luz||``. Para o valor, insira o dado ``||Input:Nível de Luz||`` localizado na aba ``||Input:Input||``.

```blocks
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
    table.log(table.createCell("Luz", input.lightLevel()))
})
```

## Passo 18

Clique no sinal de **+** para adicionar um segundo registro neste bloco. Clique no espaço do nome da coluna e 
escolha a coluna ``||table:Carga||``. Para o seu valor, insira a variável ``||Variables:Carga||``.

```blocks
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
})
```

## Passo 19

Para finalizarmos o laço ``||Basic:Sempre||``, adicione uma ``||Basic:pausa (ms)||`` de **2000ms** para definir o intervalo 
de tempo entre um registro e outro.

```blocks
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

## Passo 20

Parabéns! A lógica principal do nosso código está finalizada, e você já pode testá-lo!

 Sinta-se à vontade para incrementar o código
ajustando os valores limites ou o intervalo de atualização!

## Passo 21
Para visualizar os dados registrados, conecte o Micro:bit ao computador por meio de um cabo USB. 
O Micro:bit será exibido como uma unidade de armazenamento (pendrive). Em seguida, abra a pasta 
do Mircro:bit que irá aparecer, clique duas vezes em **MY_DATA.HTM**. Para ver esse dados em um gráfico, basta clicar em **Visual preview**.

```blocks
```

## Passo 22
Se necessário, confira o seu código clicando na lâmpada de dica.

```blocks
input.onButtonPressed(Button.AB, function () {
    table.deleteLog()
    Carga = 0
})
let Carga = 0
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


```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```