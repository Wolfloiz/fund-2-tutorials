# Esteira Transportadora - Acionamento

## Passo 1: Exibindo um Ícone Inicial
Vamos exibir um ícone de coração para indicar que o micro:bit está pronto para o funcionamento da esteira.

Vá até a aba ``||Basic:Básico||``, arraste o bloco ``||Basic: mostrar ícone||`` e escolha o ícone de coração.
Adicione um  ``||Basic:pausar (ms) 100||`` logo abaixo e ajuste o valor para 1 segundo.

Por fim, insira um ``||Basic:limpar tela||`` para apagar o ícone.

```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
```

## Passo 2: Criando a Variável Ligado

Antes de controlar a esteira transportadora, precisamos criar uma variável chamada Ligado. Essa variável ajudará a armazenar se a esteira está ligada ou desligada.

Na aba ``||Variables:Variáveis||`` , clique em Fazer uma variável e nomeie-a como Ligado.
No bloco ``||Basic:no iniciar||`` , arraste o bloco  ``||Variables:definir Ligado para||`` e coloque o valor  ``||Logic:falso||``, retirado da aba ``||Logic:lógica||``, assim garantimos que a esteira iniciará desligada.
```blocks
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
let Ligado = false```

## Passo 3: Criando o Evento do Botão A
Agora, precisamos configurar o botão A para ativar e desativar a esteira transportadora.

Acesse a aba ``||Input:Entrada||``, arraste o bloco ``||Input:no botão A pressionado||`` para o editor.

```blocks
input.onButtonPressed(Button.A, function () {
	
})
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
let Ligado = false
```

## Passo 4: Alternando o Estado da Esteira
Queremos que, ao pressionar o botão A, o estado da esteira mude de ligado para desligado e vice-versa.

Vá até a aba ``||Variables:Variáveis||`` e arraste o bloco ``||Variables:definir Ligado para||`` dentro do bloco do botão A pressionado.
Busque no menu ``||Logic:Lógica||`` o inversor ``||Logic:não||`` e substitua o valor 0 para inverter o valor da variável.

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

## Passo 5: Baixar biblioteca Fuzzy
Importe a biblioteca da Fuzzy para habilitar as abas ``||Actuators:Atuadores||`` 
e ``||sensors:Sensores||``. Para isso, clique na aba **+ Extensões**, insira o endereço 
https://github.com/FuzzyMakers/pxt-fuzzyMakers no campo de pesquisa e selecione a biblioteca.


## Passo 6: Ligando e Desligando a Esteira
Agora, vamos adicionar a lógica para ligar e desligar a esteira de acordo com o valor da variável Ligado.

Na aba ``||Logic:Lógica||`` arraste um bloco ``||Logic:se então senão||``.
Acesse a aba  ``||Variables:Variáveis||`` e arraste  ``||Variables:Ligado||`` para dentro da condição do bloco ``||Logic:se então senão||``..

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


## Passo 7: Ligando e Desligando a Esteira

Abaixo do ``||Logic:então||`` adicione um bloco ``||Actuators:Motor CC, definir velocidade 0 do motor na porta P8||`` que pode ser retirado do menu ``||Actuators:Atuadores||``.
Altere P8 para P16 (ou outra porta conectada ao motor da esteira) e a velocidade para 450.

No bloco ``||Logic:senão||``, adicione um bloco ``||Actuators:Motor CC, parar motor na porta P8||`` que pode ser retirado do menu ``||Actuators:Atuadores||``, altere o valor de P8 para P16.

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
## Passo 8: Testando o Código
Agora seu código está pronto! 🛠️

Baixe o código para o micro:bit.
Conecte a esteira à porta P16 do micro:bit (ou outra porta digital correspondente).
Pressione o botão A para ligar a esteira.
Pressione novamente o botão A para desligar a esteira.
Observe que a esteira liga e desliga alternadamente a cada toque no botão.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```