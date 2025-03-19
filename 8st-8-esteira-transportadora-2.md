# Esteira Transportadora - Automação

## Passo 1 Importando o Código do Projeto Anterior
Nesta atividade, vamos continuar a evolução do sistema da esteira transportadora, adicionando:

✅ Um mecanismo de descarte com servo motor para peças fora do padrão.

✅ Uma função de erro para detectar vibrações na esteira.

✅ O registro de variáveis em uma tabela, permitindo armazenar os dados de contagem de peças e descartes.

ertifique-se de utilizar o código construído na atividade anterior para começarmos.

```template
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
    while (!(input.buttonIsPressed(Button.A))) {
        music.play(music.tonePlayable(988, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
    basic.clearScreen()
}
function teste () {
    if (tempo < 250 || tempo < 750) {
        Descarte += 1
        Erro()
    } else {
        Bits += 1
    }
}
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showNumber(Bits)
    basic.showNumber(Descarte)
    basic.clearScreen()
})
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
        actuators.SetSpeedMotor(450, OutputPorts.P16)
    } else {
        actuators.StopMotor(OutputPorts.P16)
    }
})
let Saida = 0
let Entrada = 0
let tempo = 0
let Bits = 0
let Descarte = 0
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
Descarte = 0
Bits = 0
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P0) == 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P0) == 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
        Saida = input.runningTime()
        tempo = Saida - Entrada
        teste()
    }
})
```

## Passo 2 Baixar biblioteca Fuzzy

Como de costume, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3: Ajustando a Função no iniciar

Agora, precisamos garantir que a posição inicial do servo motor e a tabela de registros estejam corretamente configuradas no início do código.

**O que estamos adicionando?**

🔹 Configuração inicial do servo motor → Precisamos garantir que o servo motor esteja na posição correta antes do sistema começar a operar. A posição inicial será 125 graus, que manterá o mecanismo de descarte na posição neutra.

🔹 Criação das colunas na tabela de registros → Vamos estruturar a tabela de dados para armazenar o número de peças aceitas (Bits) e peças descartadas (Descarte).

**Como fazer isso?**

1️⃣ Vá até ``||Actuators:Atuadores||`` e adicione o bloco ``||Actuators:Servo motor, definir ângulo 0 do servo motor na porta P8 no modo Knob||``.
Defina o ângulo para 125.

2️⃣ Vá até ``||Table:Registro de dados||`` e adicione o bloco ``||Table:Adicionar colunas ao registro de dados||``.
Nomeie as colunas: "Bits" e "Descarte".


```blocks
actuators.SetAngleServoKnob(125, OutputPorts.P8)

table.setColumnTitles(
"Bits",
"Descarte"
)

basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()

```

## Passo 4: Ajustando a Função Teste

Agora, precisamos modificar a função Teste para que:

🔹 O servo motor entre em ação sempre que uma peça for detectada fora do padrão.

🔹 Os dados de Bits e Descarte sejam registrados na tabela.

**Como funciona essa função?**

📌 Se a peça estiver fora do padrão (tempo < 250 ou tempo > 750):

✔️ O servo motor será acionado para 1023 graus (posição de descarte).

✔️ Após 500ms, o servo retornará à posição inicial (125 graus).

✔️ O contador de Descarte será incrementado.

📌 Se a peça estiver dentro do padrão:

✔️ Apenas incrementamos o contador de Bits.

📌 Os dados serão registrados na tabela, independentemente do resultado.



## Passo 5: Ajustando a Função Teste

📌 Para o descarte de peças:

1️⃣ Vá até ``||Actuators:Atuadores||`` e adicione o bloco ``||Actuators:Definir ângulo 0 do servo motor na porta P8 no modo Knob||``:
Ajuste o ângulo para 1023 (posição de descarte). 

2️⃣ Adicione uma ``||Basic:pausa(ms)||`` de 500ms retirada da aba ``||Basic:Básico||``

3️⃣ Volte o mecanismo para a posição original copiando o bloco de configuração do servo do início.

4️⃣ Exclua a chamada da função ``||Functions:erro||``, pois não será mais necessário parar a esteira, já que a peça fora do padrão é desviada.

```blocks
function Teste () {
    if (Tempo < 250 || Tempo > 750) {
        actuators.SetAngleServoKnob(1023, OutputPorts.P8)
        basic.pause(500)
        actuators.SetAngleServoKnob(125, OutputPorts.P8)
        Descarte += 1
    } else {
        Bits += 1
    }
}
```

## Passo 6: Ajustando a Função Teste

📌 Para o registro dos dados na tabela:

1️⃣ Vá até ``||Table:Registro de dados||`` e adicione o bloco ``||Table:Registrar dados coluna " " valor 0||``.

2️⃣ Crie dois registros:

"Bits" → Com o valor da variável ``||Variables:Bits||``.

"Descarte" → Com o valor da variável ``||Variables:Descarte||``.

```blocks
function Teste () {
    if (Tempo <250  || Tempo > 750) {
        actuators.SetAngleServoKnob(1023, OutputPorts.P8)
        basic.pause(500)
        actuators.SetAngleServoKnob(125, OutputPorts.P8)
        Descarte += 1
    } else {
        Bits += 1
    }
    table.log(
    table.createCell("Bits", Bits),
    table.createCell("Descarte", Descarte)
    )
}
```

## Passo 7: Detectando Vibrações na Esteira

📌 Se a esteira vibrar, o sistema interrompe o funcionamento e exibe um alerta de erro.

**Como funciona essa função?**

✔️ Quando a esteira sofrer uma vibração, o sensor de movimento do micro:bit acionará a função de erro.

✔️ A função ``||Functions:Error||`` interrompe a esteira, exibe um ícone de "X" e toca um som de alerta até que o botão A seja pressionado.

Como adicionar a detecção de vibração?

1️⃣ Vá até ``||Input:Entrada||`` e adicione o bloco ``||Input:em agitar||``.

2️⃣ Dentro dele, vá até ``||Functions:Funções||`` e adicione ``||Functions:ligar Error||``.

```blocks
input.onGesture(Gesture.Shake, function () {
    Error()
})
```
## Passo 8: Criando a Função para Limpar os Registros de Dados

Agora, precisamos criar um método de reset que permita limpar os registros de contagem da tabela de dados.

📌 **O que essa função fará?**

✔️ Apaga todos os registros da tabela, removendo os valores de Bits e Descarte.

✔️ Zera as variáveis de contagem, reiniciando o contador de peças processadas.

✔️ Exibe um ícone de "casa" na matriz de LEDs para indicar que o sistema foi reiniciado.

✔️ Após 1 segundo, limpa a tela e o sistema volta ao funcionamento normal.

## Passo 9: Criando a Função para Limpar os Registros de Dados

1️⃣ Vá até ``||Input:Entrada||`` e adicione o bloco ``||Input:no botão B pressionado||``.

2️⃣ Vá até ``||Basic:Básico||`` e adicione o bloco ``||Basic:mostrar ícone||``.
Escolha o ícone de casa 🏠.

3️⃣ Vá até ``||Table:Registro de dados||`` e adicione o bloco ``||Table:Deletar registros||``. Clique no símbolo "+" e selecione a opção "completo".

4️⃣ Vá até ``||Variables:Variáveis||`` e adicione ``||Variables:definir Bits para 0||`` e ``||Variables:definir Descarte para 0||``.

5️⃣ Vá até ``||Basic:Básico||`` e adicione o bloco ``||Basic:pausar (ms)||`` com o valor 1000 (1 segundo).

6️⃣ Vá até ``||Basic:Básico||`` e adicione o bloco ``||Basic:limpar tela||``.

```blocks
input.onButtonPressed(Button.B, function () {
    basic.showIcon(IconNames.House)
    table.deleteLog(table.DeleteType.Full)
    Bits = 0
    Descarte = 0
    basic.pause(1000)
    basic.clearScreen()
})
```

## Passo 10: Testando e Concluindo o Projeto

Agora que todas as funcionalidades foram implementadas, é hora de testar o código completo e garantir que tudo funcione corretamente.

📌 **O que devemos testar?**

✅ Ligar e desligar a esteira pressionando o botão A.

✅ Registrar a passagem das peças pelo sensor infravermelho.

✅ Desviar peças fora do padrão com o servo motor.

✅ Registrar os dados na tabela (número de peças aceitas e descartadas).

✅ Detectar vibrações na esteira e exibir o alerta de erro.

✅ Limpar os registros de dados pressionando o botão B.

✅ Exibir os valores de Bits e Descarte tocando no logotipo do micro:bit.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```