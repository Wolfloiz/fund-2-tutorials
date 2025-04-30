### @diffs true

# Aquecimento Global

## Passo 1
Neste projeto, vamos simular o processo de aquecimento global usando o sensor de temperatura
do Micro:bit para acionar um Servo Motor. O movimento deste servo ilustra o derretimento de uma geleira
na estrutura criada na etapa anterior da atividade.

## Passo 2
Para começar, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3
Vamos começar configurando a inicialização do Micro:bit em nosso código. Para isso, acesse a 
aba ``||Basic:Básico||`` e insira o bloco ``||Basic:mostrar número||`` dentro do laço ``||Basic:no iniciar||``. 

```blocks
basic.showNumber(0)
```

## Passo 4
Em seguida, acesse a categoria ``||input:Input||`` e arraste o bloco redondo ``||input:temperatura (°C)||`` 
para dentro do comando ``||Basic:mostrar número||``. Isso vai garantir que, ao iniciar, o Micro:bit exiba 
a temperatura do ambiente naquele momento, servindo de base para ajustarmos as condições que adicionaremos posteriormente.

```blocks
basic.showNumber(input.temperature())
```

## Passo 5
Agora, vamos garantir que a estrutura seja inicializada com a geleira em sua altura máxima. Para isso, 
acesse a categoria ``||actuators:Atuadores||`` e adicione o comando ``||actuators:Servo, definir posição 0 na porta P8 modo knob||``
dentro do laço ``||Basic:no iniciar||``. 

**Atenção**: Altere o valor da posição de ``||actuators:0||`` para ``||actuators:1023||`` e a porta de ``||actuators:P8||`` para ``||actuators:P16||``.

```blocks
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
```

## Passo 6
Para finalizar o laço ``||Basic:no iniciar||``, acesse a aba ``||Basic:Básico||`` e adicione o comando ``||Basic:limpar tela||``.

```blocks
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
```

## Passo 7
Antes de seguirmos para a lógica principal do código, vamos implementar uma funcionalidade para 
mostrar a temperatura quando pressionarmos o ``||input:botão A||``. Isso será útil para ajustarmos 
a temperatura limite no laço condicional posteriormente.

Então, acesse a categoria ``||input:Input||`` e selecione o laço ``||Input:no botão A pressionado||``.

```blocks
input.onButtonPressed(Button.A, function () {
	
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
```

## Passo 8
Dentro deste novo laço, adicionaremos os comandos de ``||Basic:limpar tela||`` seguido de ``||Basic:mostrar número||``. 
Ambos estão localizados na aba ``||Basic:Básico||`` ou podem ser copiados do laço ``||Basic:no iniciar||``.

Lembre-se de inserir o dado de ``||input:temperatura (°C)||`` no comando ``||Basic:mostrar número||``. 

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
```

## Passo 9
Feito isso, começaremos a lógica central do programa. Acesse a aba ``||Basic:Básico||`` e 
adicione um laço ``||Basic:sempre||`` ao seu código. Em seguida, vá à categoria ``||Logic:Lógica||`` 
e insira o laço condicional ``||Logic:Se verdadeiro então... senão||`` dentro de ``||Basic:sempre||``. 

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (true) {
    	
    } else {
    	
    }
})
```

## Passo 10
Retorne à categoria ``||Logic:Lógica||`` e adicione o comparador ``||Logic:0 < 0||`` substituindo 
o ``||Logic:verdadeiro||`` do laço ``||Logic:Se verdadeiro então... senão||``.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (0 < 0) {
    	
    } else {
    	
    }
})
```

## Passo 11
Em seguida, modifique o operador de **<** para **>=** e o primeiro campo do ``||Logic:comparador||`` de **0** para o valor de ``||input:temperatura (°C)||``
localizado na aba ``||input:Input||``. 

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 0) {
    	
    } else {
    	
    }
})
```

## Passo 12
O segundo campo do ``||Logic:comparador||`` será a temperatura limite para desencadear o movimento do 
servo motor. **Ela deve ser ajustada de acordo com o seu ambiente!**

Recomendamos que ela seja estabelecida como **3°C** acima da temperatura medida quando o Micro:bit foi iniciado.
Isso permite que você consiga aquecer a placa e alcançar a temperatura limite posicionando as palmas de suas mãos sobre o Micro:bit. 

## Passo 13
Por exemplo, se a temperatura medida inicialmente foi de **25°C**, alteraremos o segundo número do 
``||Logic:comparador||`` para **28** (25+3).

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 28) {
    	
    } else {
    	
    }
})
```

## Passo 14
Agora, vamos determinar o que acontece quando essa condição é atendida, ou seja, a temperatura é maior ou igual que 28°C.
Para isso, acesse a categoria ``||Basic:Básico||`` e inclua o bloco ``||Basic:mostrar ícone X||`` dentro do ``||Logic:então||``
para indicar que a temperatura crítica foi atingida e a geleira derreterá.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 28) {
        basic.showIcon(IconNames.No)
    } else {
    	
    }
})
```

## Passo 15
Além disso, precisamos mover o servo motor para ilustrar o derretimento da geleira. Portanto, 
acesse a categoria ``||actuators:Atuadores||`` e adicione o comando ``||actuators:Servo, definir posição 0 na porta P8 modo knob||``
abaixo do bloco ``||Basic:mostrar ícone X||`` ainda dentro do ``||Logic:então||``.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 28) {
        basic.showIcon(IconNames.No)
        actuators.SetAngleServoKnob(0, OutputPorts.P8)
    } else {
    	
    }
})
```

## Passo 16
Altere a porta de ``||actuators:P8||`` para ``||actuators:P16||``.  

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 28) {
        basic.showIcon(IconNames.No)
        actuators.SetAngleServoKnob(0, OutputPorts.P16)
    } else {
    	
    }
})
```

## Passo 17
Por fim, dentro do ``||Logic:senão||``, devemos fazer o oposto, para quando a temperatura crítica ainda não tenha sido atingida.
Portanto, adicione o comando de ``||Basic:mostrar ícone||`` para exibir um *check*, indicando que está dentro do limite por enquanto.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 28) {
        basic.showIcon(IconNames.No)
        actuators.SetAngleServoKnob(0, OutputPorts.P16)
    } else {
        basic.showIcon(IconNames.Yes)
    }
})
```

## Passo 18
Também devemos manter o servo na posição inicial, com a geleira acima do nível do mar.
Para isso, adicione o bloco ``||actuators:Servo, definir posição 1023 na porta P16 modo knob||``.

**Atenção:** Certifique-se de que a posição seja ``||actuators:1023||`` e a porta ``||actuators:P16||``. 

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 28) {
        basic.showIcon(IconNames.No)
        actuators.SetAngleServoKnob(0, OutputPorts.P16)
    } else {
        basic.showIcon(IconNames.Yes)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
    }
})
```

## Passo 19

Pronto! Agora teste sua maquete observando se a temperatura crítica está sendo alcançada.
Para verificar a temperatura a qualquer momento, pressione o ``||input:botão A||``. Se necessário, 
faça ajustes nessa condição para se adequar ao seu ambiente.

```blocks
```

## Passo 20
Confira o seu código clicando na lâmpada de dica.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.showNumber(input.temperature())
})
basic.showNumber(input.temperature())
actuators.SetAngleServoKnob(1023, OutputPorts.P16)
basic.clearScreen()
basic.forever(function () {
    if (input.temperature() >= 28) {
        basic.showIcon(IconNames.No)
        actuators.SetAngleServoKnob(0, OutputPorts.P16)
    } else {
        basic.showIcon(IconNames.Yes)
        actuators.SetAngleServoKnob(1023, OutputPorts.P16)
    }
})
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```