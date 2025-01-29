# Caça ao Tesouro

## Passo 1

Nesse tutorial, você vai aprender a programar dois Micro:bits, um deles será o **Tesouro** e enviará sinais de rádio para o outro, que será o **Caçador** e irá funcionar como um radar. Comece programando o **Tesouro**.

## Passo 2

Vá até a aba ``||radio:Rádio||`` e arraste o bloco ``||radio:definir grupo do rádio (1)||`` para dentro do laço ``||basic:no iniciar||``. Altere o número de **1** para **255**, ou algum grupo próximo de 255. 
 
 **ATENÇÃO:** Certifique-se de que o número seja diferente dos outros grupos da sua sala de aula.

```blocks
radio.setGroup(255)
```

## Passo 3

Ainda na categoria ``||radio:Rádio||``, clique na seção ``||radio:mais||`` logo abaixo dela e arraste o bloco ``||radio:conjunto de rádio transmite energia (7)||`` para dentro do laço ``||basic:no iniciar||``. 
Esse bloco vai definir a potência e, consequentemente, o alcance do sinal transmitido pelo Tesouro.

```blocks
radio.setGroup(255)
radio.setTransmitPower(7)
```

## Passo 4

Retorne à aba ``||radio:Rádio||``, e arraste o bloco ``||radio:rádio envia número (0)||`` para dentro do laço ``||basic:sempre||``. 
Isso envia um número qualquer para o outro Micro:bit Caçador para que os Micro:bits 
se comuniquem constantemente.

```blocks
radio.setGroup(255)
radio.setTransmitPower(7)
basic.forever(function () {
    radio.sendNumber(0)
})
```

## Passo 5

Pronto! Agora que você já finalizou a programação do Micro:bit Tesouro, faça o download e siga para a programação do seu Micro:bit **Caçador**.

## Passo 6

No código do **Caçador**, vá até a aba ``||radio:Rádio||``, e arraste o bloco ``||radio:definir grupo do rádio (1)||`` para dentro do laço ``||basic:no iniciar||``. Altere o número de **1** para **255**. 

 **ATENÇÃO:** Tenha certeza de que esse número seja igual ao colocado no **Tesouro**, para que eles se comuniquem entre si.

```blocks
radio.setGroup(255)
```

## Passo 7

Na aba ``||radio:Rádio||``, arraste o laço ``||radio:ao receber rádio (receivedNumber)||`` para dentro do código. 
Esse laço será executado sempre que o Micro:bit receber um número via rádio. 
Ou seja, neste caso, quando ele receber o número **0** que o Micro:bit Tesouro enviou.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
	
})
radio.setGroup(255)
```
## Passo 8

Agora, para procurarmos o Tesouro, vamos nos basear na distância entre os Micro:bits. 
Para estimarmos essa distância, usamos a potência do sinal. Quanto mais longe eles estiverem
um do outro, mais fraco será o sinal. Se estiverem perto, o sinal de rádio estará mais forte.

## Passo 9

Portanto, crie uma variável para receber a intensidade do sinal do Tesouro. Vá até a aba ``||variables:Variáveis||``, clique em **Fazer uma variável...** e, em seguida, dê o nome **Sinal** para a variável.
Na mesma aba, arraste o bloco ``||variables:definir [Sinal] para (0)||`` para dentro do laço ``||radio:ao receber rádio (receivedNumber)||``.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = 0
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 10

Na aba ``||radio:Rádio||``, arraste o bloco ``||radio:received packet (intensidade do sinal)||`` até o número **0** do bloco ``||variables:definir [Sinal] para (0)||``. Agora a intensidade do sinal emitido pelo Tesouro será salva na variável **Sinal**.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 11

A intensidade do sinal é medida em dBm (decibel miliwatt). Nessa atividade, um sinal **maior ou igual a -50dBm** é um sinal **forte**, um sinal **entre -50 e -80** é um sinal intermediário, e um sinal **menor ou igual a -80dBm** é um sinal **fraco**. 
Quanto mais **forte** o sinal captado, mais **próximo** um Micro:bit está do outro.

 **ATENÇÃO**: Estamos trabalhando com valores negativos, portanto, um sinal mais intenso terá um valor mais próximo de 0, enquanto um sinal mais fraco será mais negativo... 

## Passo 12

Para indicar a distância entre Caçador e Tesouro, vamos criar algumas condições. 
Acesse a aba ``||logic:Lógica||`` e adicione **3** blocos ``||logic:se <verdadeiro> então||`` ao laço ``||radio:ao receber rádio (receivedNumber)||``. 
No canto inferior esquerdo do último bloco, clique no sinal de **+** para adicionar um bloco ``||logic:senão||``.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (true) {
    	
    }
    if (true) {
    	
    }
    if (true) {
    	
    } else {
    	
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 13

Para a condição de um sinal **fraco**, acesse a categoria ``||logic:Lógica||``, arraste o bloco operador ``||logic:0 < 0||`` para dentro do campo <**verdadeiro**> do primeiro bloco ``||logic:se <verdadeiro> então||``. 
Em seguida, volte à aba ``||variables:Variáveis||`` e substitua o primeiro **0** pelo bloco ``||variables:(Sinal)||``. 
Feito isso, altere o segundo **0** por **-80** e altere o operador de comparação de **<** para **≤**.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (Sinal <= -80) {
    	
    }
    if (true) {
    	
    }
    if (true) {
    	
    } else {
    	
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 14

Para a condição do sinal **intermediário**, precisaremos de um operador diferente. Volte à ``||logic:Lógica||`` e arraste o bloco ``||logic:< > e < >||`` para dentro do <**verdadeiro**> do segundo bloco ``||logic:se <verdadeiro> então||``.
Com ele, determinamos duas condições que devem ser satisfeitas simultaneamente para que o bloco seja executado.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (Sinal <= -80) {
    	
    }
    if (false && false) {
    	
    }
    if (true) {
    	
    } else {
    	
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 15

Volte à categoria ``||logic:Lógica||``, arraste o bloco operador ``||logic:0 < 0||`` para o primeiro espaço vazio do bloco ``||logic:< > e < >||`` e altere seu sinal de **<** para **>**. 

 Em ``||variables:Variáveis||``, selecione o bloco ``||variables:(Sinal)||`` e substitua o primeiro **0** deste operador. Já o segundo **0** deve ser alterado para **-80**.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (Sinal <= -80) {
    	
    }
    if (Sinal > -80 && false) {
    	
    }
    if (true) {
    	
    } else {
    	
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 16

No segundo espaço vazio do bloco ``||logic:< > e < >||``, arraste outro bloco operador ``||logic:0 < 0||``, sem mudar o sinal. 
Abra a aba ``||variables:Variáveis||`` e substitua o primeiro **0** pelo bloco ``||variables:(Sinal)||``. Modifique o segundo **0** por **-50**.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (Sinal <= -80) {
    	
    }
    if (Sinal > -80 && Sinal < -50) {
    	
    }
    if (true) {
    	
    } else {
    	
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 17

Para a condição de um sinal **forte**, retorne à categoria ``||logic:Lógica||``, mova o bloco operador ``||logic:0 < 0||`` para dentro de <**verdadeiro**> do último laço ``||logic:se <verdadeiro> então||`` e modifique seu sinal de **<** para **≥**. 
Retorne à ``||variables:Variáveis||`` e substitua o primeiro **0** pelo bloco ``||variables:(Sinal)||``. Altere o segundo **0** para **-50**.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (Sinal <= -80) {
    	
    }
    if (Sinal > -80 && Sinal < -50) {
    	
    }
    if (Sinal >= -50) {
    	
    } else {
    	
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 18

Por fim, para que o Micro:bit nos indique se o Tesouro está perto ou longe, 
precisamos que ele nos mostre algo visual na tela. Para isso, vamos adicionar o bloco 
``||basic:mostrar ícone||`` dentro de cada um dos laços ``||logic:se-então||``. 
Escolha o ícone de diamante pequeno para indicar que o Tesouro está distante, 
o ícone de diamante maior para uma distância intermediária, e o ícone de quadrado para indicar proximidade.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (Sinal <= -80) {
        basic.showIcon(IconNames.SmallDiamond)
    }
    if (Sinal > -80 && Sinal < -50) {
        basic.showIcon(IconNames.Diamond)
    }
    if (Sinal >= -50) {
        basic.showIcon(IconNames.Square)
    } else {
    	
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 19

Para finalizar, retorne à ``||basic:Básico||`` e arraste o bloco ``||basic:limpar tela||`` para dentro do bloco ``||logic:senão||``, para limpar a tela caso o Tesouro não esteja enviando sinais..

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    Sinal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (Sinal <= -80) {
        basic.showIcon(IconNames.SmallDiamond)
    }
    if (Sinal > -80 && Sinal < -50) {
        basic.showIcon(IconNames.Diamond)
    }
    if (Sinal >= -50) {
        basic.showIcon(IconNames.Square)
    } else {
        basic.clearScreen()
    }
})
let Sinal = 0
radio.setGroup(255)
```

## Passo 20

Pronto! Agora que você já tem o Tesouro e o Caçador, peça para alguém esconder o Tesouro e divirta-se com a caça! 
Mas não pare por aí, experimente explorar outras funcionalidades como sons, outros ícones e outras condições!

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```