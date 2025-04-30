### @diffs true
# Segunda Revolução Industrial - Eletrificação

## Passo 1
Nessa atividade, vamos programar o acionamento básico do Motor CC acoplado à esteira através do 
Botão A do Micro:bit.

## Passo 2
Para começar, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3
Vamos começar configurando a inicialização do Micro:bit em nosso código. Para isso, acesse a 
aba ``||Basic:Básico||`` e insira o bloco ``||Basic:mostrar ícone||`` dentro do laço ``||Basic:no iniciar||``.

Mantivemos o ícone de coração apenas para indicar que o Micro:bit ligou, mas fique à vontade para alterar para um 
ícone a sua escolha.

```blocks
basic.showIcon(IconNames.Heart)
```

## Passo 4
Retorne à categoria ``||Basic:Básico||`` e adicione os blocos ``||Basic:pausa (ms)||`` e ``||Basic:limpar tela||`` dentro do laço ``||Basic:no iniciar||``.

Altere a duração da ``||Basic:pausa||`` de **100ms** para **1000ms** (1 segundo). 

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
```

## Passo 5
Antes de controlar a esteira transportadora, precisamos criar uma variável chamada ``||Variables:Ligado||``. 
Essa variável ajudará a armazenar a informação sobre o estado da esteira, ou seja, se ela está se movimentando ou não.

Para isso, acesse a aba ``||Variables:Variáveis||``, clique em **Fazer uma variável** e nomeie-a como **Ligado**.
Em seguida, arraste o novo bloco ``||Variables:definir Ligado para 0||`` para dentro do laço ``||Basic:no iniciar||``. 

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
let Ligado = 0
```

## Passo 6
Feito isso, acesse a aba ``||Logic:Lógica||`` e selecione o bloco com bordas triangulares ``||Logic:falso||`` 
para substituir o valor **0** do comando ``||Variables:definir Ligado para 0||``. 
Assim, garantimos que a esteira iniciará desligada.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
let Ligado = false
```

## Passo 7
Agora, precisamos configurar o botão A do micro:bit para ativar e desativar a esteira transportadora.

Acesse a aba ``||Input:Input||``, e arraste o laço ``||Input:no botão A pressionado||`` para o editor.

```blocks
input.onButtonPressed(Button.A, function () {
	
})
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
let Ligado = false
```

## Passo 8
Queremos que, ao pressionar o botão A, o estado da esteira mude de ligado para desligado e vice-versa.

Então, retorne à aba ``||Variables:Variáveis||`` e arraste o bloco ``||Variables:definir Ligado para 0||`` para dentro do laço ``||Input:no botão A pressionado||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = 0
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

## Passo 9

Busque no menu ``||Logic:Lógica||`` o inversor lógico ``||Logic:não||`` e substitua o valor **0** do comando ``||Variables:definir Ligado para 0||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(false)
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

## Passo 10
Retorne à aba ``||Variables:Variáveis||`` e arraste o bloco de bordas redondas ``||Variables:Ligado||`` para dentro do campo
triangular do inversor lógico ``||Logic:não||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

## Passo 11
Agora, vamos adicionar a lógica para ligar e desligar a esteira de acordo com o valor da variável ``||Variables:Ligado||``.

Na aba ``||Logic:Lógica||`` arraste um laço ``||Logic:se então senão||`` para dentro do laço ``||Input:no botão A pressionado||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (true) {
    	
    } else {
    	
    }
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

## Passo 12
Volte à aba ``||Variables:Variáveis||`` e arraste o bloco redondo ``||Variables:Ligado||`` para dentro da condição do bloco ``||Logic:se então senão||``, substituindo o valor ``||Logic:verdadeiro||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
    	
    } else {
    	
    }
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

## Passo 13

Abaixo do ``||Logic:então||`` adicione um bloco ``||Actuators:Motor CC, definir velocidade 0 porta P8||`` localizado no menu ``||Actuators:Atuadores||``.
Altere ``||Actuators:P8||`` para ``||Actuators:P16||`` e a velocidade para **450**.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
        actuators.SetSpeedMotor(450, OutputPorts.P16)
    } else {
        
    }
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

## Passo 14

Já dentro do ``||Logic:senão||``, adicione um bloco ``||Actuators:Motor CC, parar motor na porta P8||``, também encontrado no menu ``||Actuators:Atuadores||``. 
Altere o valor de ``||Actuators:P8||`` para ``||Actuators:P16||``.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
        actuators.SetSpeedMotor(450, OutputPorts.P16)
    } else {
        actuators.StopMotor(OutputPorts.P16)
    }
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

## Passo 15
Agora seu código está pronto! Baixe-o para o micro:bit.
 
 Encaixe o conector Speed do Motor CC na porta P16.
 
 Pressione o botão A para ligar a esteira.
 
 Pressione novamente o botão A para desligar a esteira.
 
 Observe que a esteira liga e desliga alternadamente a cada toque no botão.

```blocks
```

## Passo 16
Se necessário, confira o seu código clicando na lâmpada de dica.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
        actuators.SetSpeedMotor(450, OutputPorts.P16)
    } else {
        actuators.StopMotor(OutputPorts.P16)
    }
})
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```