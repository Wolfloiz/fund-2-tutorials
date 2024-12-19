# Trator Autônomo

## Step 1
Neste tutorial, você aprenderá a programar um Trator para percorrer um percurso 
determinado. Ele deve repetir a sequência de movimentos abaixo por 3 vezes:

1. andar pra frente por 3 segundos.
2. virar à esquerda.
3. andar pra frente por 1 segundo.
4. virar à esquerda.
5. andar para frente por 3 segundos.
6. virar à direita.
7. andar para frente por 1 segundo.
8. virar à direita.

## Step 2
Primeiro, importe a biblioteca da Fuzzy para habilitar as abas ``||Actuators:Atuadores||`` 
e ``||sensors:Sensores||``. Para isso, clique na aba **+ Extensões**, insira o endereço 
https://github.com/FuzzyMakers/pxt-fuzzyMakers no campo de pesquisa e selecione a biblioteca.


## Step 3
Em seguida, acesse a aba ``||input:Input||`` e selecione o laço ``||input:no botão A pressionado||``. 
Altere para o **botão B**.

```blocks
input.onButtonPressed(Button.B, function () {
})
```

## Step 4
Acesse a aba ``||loops:Loops||`` e selecione o bloco ``||loops:repetir 4 vezes-executar||``. 
Coloque-o dentro do bloco ``||input:no botão B pressionado||`` e substitua o número **4** por **3**.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
    }
})
```

## Step 5
Vá até a aba ``||actuators:Atuadores||``, selecione o bloco ``||actuators:Motor CC, definir velocidade 0 do motor na porta P8||`` 
e posicione-o dentro do laço. Ajuste a velocidade de **0** para **500**.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
    }
)}
```
## Step 6
Na aba ``||actuators:Atuadores||``, selecione o bloco ``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8 ||`` 
e posicione-o abaixo do bloco que define a velocidade. Duplique-o e altere a porta do segundo bloco para **P16**.

Esses blocos controlam o sentido de rotação dos motores. O primeiro movimento do Trator será em linha reta. Para isso, configure 
direções opostas para os giros dos motores: horário para o motor na porta **P8** e **anti-horário** para o motor na porta **P16**.

**OBS.:** *Se o Trator andar para trás, basta inverter as portas **P8** e **P16** para que ele se mova para frente.*

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
    }
)}    
```

## Step 7
Vá até a aba ``||basic:Básico||``, selecione o bloco ``||basic:pausa (ms) 100||`` 
e posicione-o abaixo dos blocos de direção dos motores. Ajuste o tempo para **3000 ms**.

Isso conclui o primeiro movimento, em que o Trator avançará por 3 segundos.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        basic.pause(3000)
})
```

## Step 8
Ainda dentro do laço ``||Input:no botão B pressionado||``, duplique os dois blocos
``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8 ||`` e a 
``||Basic:pausa (ms) 100||`` para programar um movimento de curva para a esquerda.
Após duplicá-los, deixe o sentido de giro de ambos os comandos para o sentido **anti-horário**. 
Ajuste o tempo da ``||Basic:pausa||`` para **625 ms**.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
})
```

## Step 9
Agora, para que ele se movimente em linha reta novamente, duplique os blocos 
``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8||``
*da primeira parte do movimento*, quando os sentidos de direção eram diferentes entre si. 
Modifique a ``||Basic:pausa||`` para **1000 ms**.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
})
```

## Step 10
Agora, vamos repetir os comandos de curva à esquerda. Para isso, duplique os blocos de 
``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8 ||``
da segunda parte do movimento, quando o sentido de direção dos motores eram iguais. 
O valor da ``||Basic:pausa||`` deve ser mantido em **625 ms**.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
})
```
## Step 11
Novamente, adicionaremos um movimento em linha reta por 3 segundos (3000 ms). 
Neste caso, duplique os blocos de ``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8||``
que estão com sentidos de rotação distintos, **anti-horário** na porta **P16** e **horário** na **P8**, e determine uma 
``||Basic:pausa||`` de **3000 ms**.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
})
```

## Step 12
Feito isso, devemos configurar o movimento de curva à direita. Como ele é 
oposto do movimento de curva à esquerda, duplique os dois blocos de 
``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8||`` 
e o bloco de ``||Basic:pausa`` da segunda parte do código. Após duplicá-los, 
deixe o sentido de giro de ambos os comandos como **horário** e mantenha a 
``||Basic:pausa||`` em **625 ms**.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(625)
})
```

## Step 13
Agora, repita a parte do código responsável pelo movimento retilíneo de 1 segundo (1000 ms). Novamente, utilize os 
comandos os dois ``||actuators:Motor CC, definir direção do motor para o sentido horário na porta P8 ||`` e a
``||Basic:pausa||``. Configure os sentidos em **anti-horário** para a porta **P16** e **horário** para a porta **P8**. 
Ajuste o tempo da ``||Basic:pausa||`` para **1000 ms**.  

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
})
```

## Step 14

Essa sequência de movimentos será repetida por 3 vezes e em seguida o código segue para fora 
do  ``||loops: repetir 3 vezes-executar||``. Dessa forma, nosso próximo passo é parar os motores.
Conseguimos fazer isso acessando a aba ``||actuators:Atuadores||`` e selecionando o comando 
``||actuators:Motor CC, parar motor na porta P8||``. Modifique a porta de saída para **P12**.
Posicione esse comando logo após o ``||loops:loop||`` porém ainda dentro do laço ``||input:no botão B pressionado||``.

```blocks
input.onButtonPressed(Button.B, function () {
    for (let index = 0; index < 3; index++) {
        actuators.SetSpeedMotor(500, OutputPorts.P12)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(3000)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(625)
        actuators.SetDirectionMotor(MotorDirection.antiClockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(1000)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P16)
        actuators.SetDirectionMotor(MotorDirection.clockwise, OutputPorts.P8)
        basic.pause(625)
    }
    actuators.StopMotor(OutputPorts.P12)
})
```

## Step 15
Pronto! Agora, teste o código no Trator e explore diferentes trajetórias, ajustando o sentido
de rotação dos motores e os tempos de pausa.

```package
fuzzyBot=github:Wolfloiz/pxt-fuzzyMakers
```