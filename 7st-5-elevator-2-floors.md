# Elevador 2 andares

## Step 1
Neste tutorial, você irá aprender a programar um elevador para uma estrutura de 2 andares. 

## Step 2
Primeiro, importe a biblioteca da Fuzzy para habilitar as abas ``||Actuators:Atuadores||`` e 
``||sensors:Sensores||``. Para isso, clique na aba __+Extensões__, insira o endereço 
https://github.com/FuzzyMakers/pxt-fuzzyMakers no campo de pesquisa e selecione a biblioteca.

## Step 3
Agora, acesse a aba ``||input:Input||`` e inclua o laço ``||input:no botão A pressionado||`` em seu programa. 
Esse input será utilizado como o comando para fazer o elevador **subir**.

```blocks
input.onButtonPressed(Button.A, function () {	
})
```

## Step 4
Em seguida, na aba ``||logic:Lógica||``, selecione o laço ``||logic:se-verdadeiro-então||``. 
Posicione-o dentro do laço ``||input:no botão A pressionado||``.

```blocks
input.onButtonPressed(Button.A, function () {
    if (true) {
    	
    }	
})
```

## Step 5
Retorne à aba ``||logic:Lógica||`` e selecione o bloco comparador
``||logic:0 = 0||``. Posicione-o dentro do espaço triangular do laço 
``||logic:se-verdadeiro-então||``, substituindo a palavra ``||logic:verdadeiro||``.

```blocks
input.onButtonPressed(Button.A, function () {
    if (0 == 0) {
    	
    }	
})
```

## Step 6
Agora, acesse a aba ``||variables:Variáveis||`` e clique em **Fazer uma variável...**.
Nomeie essa variável como ``||variables:Andar||``. 
Ela poderá ser igual a **0** ou **1**, e representa o andar no qual o elevador se encontra no momento.

## Step 7
Volte à aba ``||variables:Variáveis||`` e pegue o bloco redondo 
``||variables:Andar||``. Insira essa variável no primeiro espaço do bloco 
``||logic:0 = 0||``, substituindo o primeiro número **0**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
    	
    }	
})
```

## Step 8
Em seguida, acesse a aba ``||actuators:Atuadores||``, selecione o bloco ``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8 ||`` 
e posicione-o dentro do laço ``||logic:se-verdadeiro-então||``, substituindo a porta **P8** por **P12**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
    }
})
```

## Step 9
Vá até a aba ``||actuators:Atuadores||``, selecione o bloco ``||actuators:Motor CC, definir velocidade 0 do motor na porta P8||`` 
e posicione-o dentro do laço. 

Troque a porta **P8** pela porta **P16** e ajuste a velocidade de **0** para **512**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
    }
})
```

## Step 10
Acesse a aba ``||basic:Básico||``, selecione o bloco ``||basic:pausa(ms) 100||``, e o coloque 
abaixo do comando ``||actuators:Motor CC, definir velocidade 512 do motor na porta P16||``. Ajuste o valor da pausa, 
trocando o valor **100** por **4300**. 

Este valor é o tempo que o elevador leva para atingir o segundo andar.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
    }
})

```
## Step 11
Volte à categoria ``||actuators:Atuadores||``, selecione o bloco ``||actuators:Motor CC, parar motor na porta P8||`` 
e posicione-o dentro do laço, logo após a ``||basic:pausa(ms)100||``. 

Troque a porta para **P16**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
})
```

## Step 12
Retorne à aba ``||variables:Variáveis||``, selecione o bloco 
``||variables:definir Andar para 0||``, e o posicione dentro do laço 
``||logic:se-verdadeiro-então||``. Altere o valor de **0** para **1**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
```

## Step 13
Com isso, a parte do código que faz o elevador subir quando o botão A é pressionado 
e o mesmo se encontra no primeiro andar, está pronta. Porém, ainda nos resta fazer o código 
responsável pela descida do elevador.

## Step 14
Copie o laço ``||input:no botão A pressionado||`` (com todo seu conteúdo). Modifique a 
cópia para que ela se torne ``||input:no botão B pressionado||``, alterando de **A** para **B**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
input.onButtonPressed(Button.B, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
```

## Step 15
No laço ``||input:no botão B pressionado||``, altere a condição do teste 
``||logic:se-verdadeiro-então||``, de **Andar = 0** para **Andar = 1**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
input.onButtonPressed(Button.B, function () {
    if (Andar == 1) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
```

## Step 16
Ainda no laço ``||input:no botão B pressionado||``, altere o bloco 
``||actuators:Motor CC, definir direção do motor para sentido horário na porta P12||``,
trocando o sentido para **anti-horário**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
input.onButtonPressed(Button.B, function () {
    if (Andar == 1) {
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
```

## Step 17
Modifique o valor da ``||basic:pausa||`` para **4100**. O tempo de subida é maior que o de descida 
devido às variáveis físicas, como o peso do elevador, a gravidade, entre outros. 

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
input.onButtonPressed(Button.B, function () {
    if (Andar == 1) {
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4100)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
```

## Step 18
Por fim, ainda no laço ``||input:no botão B pressionado||``, altere o último bloco 
``||variables:definir Andar para 1||``, trocando o valor **1** por **0**.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Andar == 0) {
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4300)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 1
})
input.onButtonPressed(Button.B, function () {
    if (Andar == 1) {
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P12)
        actuators.SetSpeedMotor(512, OutputPorts.P16)
        basic.pause(4100)
        actuators.StopMotor(OutputPorts.P16)
    }
    Andar = 0
})
```

## Step 19
Pronto! Agora você já pode baixar o código para o Micro:bit e testar seu elevador. 
Após construir a estrutura, caso seja necessário, você pode efetuar modificações nos
tempos de subida e descida para que ele funcione perfeitamente.  

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```