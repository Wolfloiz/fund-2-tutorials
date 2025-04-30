### @diffs true
# Terceira Revolução Industrial - Automação

## Passo 1
Nesta atividade, vamos incrementar o programa de acionamento da esteira adicionando um sensor infravermelho que será responsável por contar e medir peças que passem sobre a esteira.
Certifique-se de utilizar o código construído na atividade anterior para começarmos.

```template
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

## Passo 2

Como de costume, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3

Antes de começarmos, precisamos criar algumas variáveis para armazenar informações sobre a esteira e as peças.

**O que essas variáveis fazem?**

**Bits** → Conta quantas peças passaram pela esteira com tamanho dentro do padrão.

**Descarte** → Conta quantas peças foram descartadas.

**Entrada** → Armazena o tempo de entrada da peça no sensor.

**Saída** → Armazena o tempo de saída da peça do sensor.

**Tempo** → Mede a duração da passagem da peça para determinar seu tamanho.

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

## Passo 4
Para criar a primeira variável acesse a aba ``||Variables:Variáveis||``, clique em **Criar uma variável** e nomeie-a como ``||Variables:Bits||``.
Repita o processo para criar as variáveis ``||Variables:Descarte||``, ``||Variables:Entrada||``, ``||Variables:Saída||`` e ``||Variables:Tempo||``.
 
 No laço ``||Basic:no iniciar||``, defina os valores iniciais das variáveis ``||Variables:Bits||`` e ``||Variables:Descarte||`` para 0,
através do bloco ``||Variables:definir variável para 0||``.

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
let Descarte = 0
let Bits = 0

```

## Passo 5

Agora, programamos o sensor infravermelho para contar e testar peças.

Então, acesse o menu ``||Basic:Básico||`` e adicione um laço ``||Basic:sempre||``. Dentro dele, arraste um laço ``||Logic:se então||``, 
localizado na aba ``||Logic:Lógica||``. 

```blocks
basic.forever(function () {
    if (true) {
    	
    }
})
```

## Passo 6

Substitua a condição ``||Logic:verdadeiro||`` pelo bloco de comparação ``||Logic:0=0||``. Atualize o sinal de **"="** para **">="**.

Altere o primeiro **0** para a leitura do sensor ``||sensors:Valor do sensor infravermelho na porta P2||``, localizado na aba ``||Sensors:Sensores||``.
Altere a porta de ``||Sensors:P2||`` para ``||Sensors:P1||`` e o segundo **0** do comparador para **120**.

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
    	
    }
})
```

## Passo 7

Dentro do laço ``||Logic:então||`` vamos adicionar o bloco ``||Variables:definir variável para 0||``.
Selecione a variável ``||Variables:Entrada||`` e substitua o valor **0** por ``||input:tempo de execução (ms)||``,
que é encontrado no menu ``||input:Input||``, no submenu ``||input:mais||``.
Assim, armazenaremos o instante em que a peça entra no campo de detecção do sensor.

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
    }
})
```

## Passo 8
Adicione um laço ``||Loops:enquanto||`` abaixo da definição anterior. Ele está localizado na aba ``||Loops:Loops||``.

Copie e cole (ctrl+C e ctrl+V), ou duplique com o botão direito do mouse, a condição feita anteriormente para o sensor, 
``||Sensors:Valor do sensor infravermelho P1 >= 120||`` e posicione-a no lugar da condição ``||Logic:falso||``
do laço ``||Loops:enquanto||``.

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
        	
        }
    }
})
```

## Passo 9

Feito isso, acesse a aba ``||Music:Música||`` e pegue o bloco ``||Music:play tone C Médio for 1 batida until done||``.
Encaixe-o dentro de ``||Loops:executar||``. Essa ação determina que, enquanto a peça estiver na área de detecção do sensor, um bip será tocado.

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
    }
})
```

## Passo 10

Abaixo do laço ``||Loops:enquanto||``, mas ainda dentro do laço ``||Logic:se então||``, copie e cole a definição da variável entrada, ``||Variables:definir entrada para tempo de execução (ms)||``. 
Altere ``||Variables:Entrada||`` para ``||Variables:Saída||``. Assim, armazenaremos o instante em que a peça sai do campo de detecção do sensor.

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
        Saída = input.runningTime()
    }
})
```
## Passo 11

Agora, vamos calcular a variável ``||Variables:tempo||``.
Então, abaixo da última definição, adicione o comando ``||Variables:definir tempo para 0||``.
Acesse o menu ``||Math:Matemática||``, selecione o bloco ``||Math:0-0||`` e posicione-o no lugar do **0** da definição da variável.

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
        Saída = input.runningTime()
        Tempo = 0 - 0
    }
})
```
## Passo 12
Substitua os números **0** da expressão matemática pelas variáveis ``||Variables:Saída||`` e ``||Variables:Entrada||``. 
Esse cálculo indica que ``||Variables:tempo||`` é a duração da permanência total da peça dentro do campo de detecção do sensor.

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
        Saída = input.runningTime()
        Tempo = Saída - Entrada
    }
})
```

## Passo 13
Agora, clique no menu ``||Advanced:Avançado||``, acesse ``||Functions:Funções||`` e clique em **Fazer uma função...**.
Crie uma função chamada ``||Functions:Teste||``. Um novo laço referente à função criada é adicionado automaticamente ao código.
Retorne ao menu de ``||Functions:Funções||`` e insira o comando ``||functions:Ligar Teste||`` no fim do laço condicional ``||logic:se então||``.

```blocks
function Teste () {
	
}
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
        Saída = input.runningTime()
        Tempo = Saída - Entrada
        Teste()
    }
})
```

## Passo 14

Dentro do laço da função ``||Functions:Teste||`` adicione um laço ``||Logic:se então senão||`` localizado na aba ``||Logic:Lógica||``. 

```blocks
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
        Saída = input.runningTime()
        Tempo = Saída - Entrada
        Teste()
    }
})
function Teste () {
    if (true) {
    	
    } else {
    	
    }
}
```

## Passo 15
Retorne à aba ``||Logic:Lógica||`` e selecione o operador Booleano ``||Logic:ou||``.
Substitua o valor ``||Logic:verdadeiro||`` do laço ``||Logic:se então senão||`` por esse operador.

```blocks
function Teste () {
    if (false || false) {
    	
    } else {
    	
    }
}
```

## Passo 16
Em cada um dos campos do operador ``||Logic:ou||``, insira blocos de comparação ``||Logic: 0 < 0||``. 

```blocks
function Teste () {
    if (0 < 0 || 0 < 0) {
    	
    } else {
    	
    }
}
```

## Passo 17
Se a peça estiver com o tamanho adequado o tempo total para ela percorrer o campo de detecção será entre 250ms e 750ms.

Então, preencha esses comparadores com os dados a seguir. **ATENÇÃO**: verifique o sinal das comparações.

 Na primeira comparação verificaremos se ``||Variables:Tempo < 250||``;
 
 Na segunda comparação verificaremos se ``||Variables:Tempo > 750||``.

A variável ``||Variables:Tempo||`` é encontrada no menu de ``||Variables:Variáveis||``.

```blocks
function Teste () {
    if (Tempo < 250 || Tempo > 750) {
    	
    } else {
    	
    }
```

## Passo 18

Agora, adicionaremos as consequências para quando as peças se encontrem ou não dentro do padrão estabelecido.

Se estiverem fora do padrão, somaremos 1 unidade à variável  ``||Variables:Descarte||`` e chamaremos uma função denominada ``||Functions:Erro||``. 
Para criar essa função, clique no menu ``||Advanced:Avançado||``, acesse ``||Functions:Funções||`` e clique em **Fazer uma função...**.

```blocks
function Erro () {
	
}
```


## Passo 19

Voltando ao laço da função ``||Functions:Teste||``, inclua o bloco ``||Variables:alterar Descarte por 1||`` dentro do ``||Logic:então||``. 
Esse comando de alteração pode ser encontrado na aba ``||Variables:Variáveis||``. *(Certifique-se de alterar para a variável Descarte se necessário)*. 
Abaixo desse bloco, acrescente um ``||Functions:ligar Erro||``.

```blocks
function Erro () {
	
}
function Teste () {
    if (Tempo < 250 || Tempo > 750) {
        Descarte += 1
        Erro()
    } else {
    	
    }
}
```

## Passo 20

Dentro do ``||Logic:senão||``, se as peças estiverem dentro do padrão, apenas incrementaremos a variável ``||Variables:Bits||``, que guarda o total de peças avaliadas. 
Copie o bloco ``||Variables:alterar Descarte por 1||``, posicione dentro de ``||Logic:senão||`` e altere ``||Variables:Descarte||`` para ``||Variables:Bits||``

```blocks
function Erro () {
	
}
function Teste () {
    if (Tempo < 250 || Tempo > 750) {
        Descarte += 1
        Erro()
    } else {
        Bits += 1
    }
}
```
## Passo 21

Agora, vamos implementar a função ``||Functions:Erro||``. Caso uma peça esteja fora do padrão, ela deve ser rejeitada e o sistema precisa indicar esse erro.
Acesse a aba ``||Actuators:Atuadores||``, selecione o bloco ``||Actuators: Motor CC, parar na porta P8||`` e coloque-o dentro do laço da função ``||Functions:Erro||``. 
Altere a porta de ``||Actuators:P8||`` para ``||Actuators:P16||``.
Assim, o motor irá parar sempre que uma peça estiver fora do padrão.

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
}
```

## Passo 22

Em seguida, vá até a aba ``||Basic:Básico||`` e selecione o bloco ``||Basic:Mostrar ícone||`` depois do comando para parar o motor. 
Escolha o ícone **X** para que a matriz de leds indique o erro.

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
}
```

## Passo 23

Ainda na função ``||Functions:Erro||``, adicione um laço ``||Loops:Enquanto||``, localizado no menu ``||Loops:Loops||``.

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
    while (false) {
    	
    }
}
```


## Passo 24

Altere a condição de ``||Logic:falso||`` para o inversor lógico ``||Logic:não||``, encontrado na aba ``||Logic:Lógica||``.

Em seguida, acesse o menu ``||Input:Input||``, selecione o bloco com bordas triangulares ``||Input:botão A é pressionado||`` e posicione-o dentro do campo do inversor lógico ``||Logic:não||``.

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
    while (!(input.buttonIsPressed(Button.A))) {
    	
    }
}
```

## Passo 25
Agora, acesse o menu ``||Music:Música||``, selecione o bloco ``||Music:play tone C Médio for 1 batida until done||`` e posicione-o dentro de ``||Loops:executar||``, 
para garantirmos que um alarme é soado até alguém intervir apertando o botão A e verificando o erro.

Altere o tom desse bloco de ``||Music:C Médio||`` para ``||Music:B agudo||`` para diferenciarmos o som de erro. 
Essa nota é a última tecla à direita do teclado. 

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
    while (!(input.buttonIsPressed(Button.A))) {
        music.play(music.tonePlayable(988, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
}
```

## Passo 26

Por fim, vá até ``||Basic:Básico||``, escolha o comando ``||Basic:limpar tela||`` e coloque-o no fim da função ``||Functions:erro||``, 
para que a tela seja apagada após verificação do erro.

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
    while (!(input.buttonIsPressed(Button.A))) {
        music.play(music.tonePlayable(988, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
    basic.clearScreen()
}
```

## Passo 27

Agora, queremos que o micro:bit exiba o número de peças aceitas e descartadas ao tocarmos no seu logotipo.

Para isso, acesse a aba ``||Input:Input||`` e adicione um laço ``||Input:no logotipo pressionado||`` ao código.

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
    while (!(input.buttonIsPressed(Button.A))) {
        music.play(music.tonePlayable(988, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
    basic.clearScreen()
}
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
	
})
```
## Passo 28

Depois, no menu ``||Basic:Básico||``, adicione dois blocos ``||Basic:mostrar número||``.
Um será usado para exibir a variável ``||Variables:Bits||`` e outro para a variável ``||Variables:Descarte||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showNumber(0)
    basic.showNumber(0)
})
```

## Passo 29
Busque essas variáveis no menu ``||Variables:Variáveis||`` e depois substitua os números **0** de cada bloco ``||Basic:mostrar número||``. 
Finalize com ``||Basic:limpar tela||``.

```blocks
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showNumber(Bits)
    basic.showNumber(Descarte)
    basic.clearScreen()
})
```

## Passo 30
Parabéns! Esse foi um tutorial muito avançado! Se você chegou até aqui:

✅ Baixe o código para o micro:bit.

✅ Conecte o motor CC da esteira na porta P16 e o sensor infravermelho na porta P1.

✅ Pressione o botão A para ligar a esteira.

✅ Coloque peças na esteira e observe a contagem.

✅ Se uma peça for muito pequena ou muito grande, o sistema para e alerta o erro.

✅ Toque no logo do micro:bit para ver o número de peças aceitas e descartadas.

```blocks

```

## Passo 31

Se necessário, confira todo o seu código clicando na lâmpada de dica.

```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
    while (!(input.buttonIsPressed(Button.A))) {
        music.play(music.tonePlayable(988, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
    basic.clearScreen()
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
function Teste () {
    if (Tempo < 250 || Tempo > 750) {
        Descarte += 1
        Erro()
    } else {
        Bits += 1
    }
}
let Saída = 0
let Entrada = 0
let Tempo = 0
let Descarte = 0
let Bits = 0
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P1) >= 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P1) >= 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
        Saída = input.runningTime()
        Tempo = Saída - Entrada
        Teste()
    }
})
```

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```
