# Esteira Transportadora - Contagem

## Passo 1 Importando o código 
Nesta atividade, vamos incrementar o programa de acionamento da esteira para adicionar um sensor infravermelho que será responsável por contar e medir peças que passem sobre a esteira.
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

## Passo 2 Baixar biblioteca Fuzzy

Como de costume, verifique se a biblioteca da Fuzzy Makers já está importada em seu MakeCode.
Se não estiver, clique na aba **+ Extensões**, copie o endereço "https://github.com/FuzzyMakers/pxt-fuzzyMakers",
cole-o no campo de pesquisa da janela que se abriu e selecione a biblioteca.

## Passo 3: Criando as Variáveis

Antes de começarmos, precisamos criar algumas variáveis para armazenar informações sobre a esteira e as peças.

**O que essas variáveis fazem?**

**Bits** → Conta quantas peças passaram pela esteira com tamanho dentro do padrão.

**Descarte** → Conta quantas peças foram descartadas.

**Entrada** → Armazena o tempo de entrada da peça no sensor.

**Saída** → Armazena o tempo de saída da peça do sensor.

**Tempo** → Mede a duração da passagem da peça para determinar seu tamanho.

**Como criar as variáveis?**

Vá até a aba ``||Variables:Variáveis||``, clique em Criar uma variável e nomeie-a como Bits.
Repita o processo para criar as variáveis Descarte, Entrada, Saída e Tempo.
No bloco ``||Basic:no iniciar||``, defina os valores iniciais das variáveis ``||Variables:Bits||`` e ``||Variables:Descarte||`` para 0,
arrastando o bloco ``||Variables:definir variavel para 0||``.



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

## Passo 4: Detectando peças com o sensor infravermelho

Agora, programamos o sensor infravermelho para contar e testar peças.

Adicione um bloco ``||Basic:sempre||`` e dentro dele um bloco ``||Logic:se então||``.

Substitua a condição ``||Logic:verdadeiro||``  pelo bloco de comparação ``||Logic:0=0||``. Atualize o sinal de "=" para ">=".

Altere o primeiro 0 para a leitura do sensor ``||Sensors:Valor do sensor infravermelho P1||`` retirado da aba ``||Sensors:Sensores||``.
 Altere o segundo 0 para 120, esse valor determina a sensibilidade do sensor infravermelho.

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
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P0) == 120) {
    	
    }
})
```

## Passo 5: Detectando peças com o sensor infravermelho

Dentro do bloco ``||Logic:então||`` vamos adicionar o bloco ``||Variables:definir variavel para 0||``,
selecione a variável ``||Variables:Entrada||`` e substitua o valor 0 por ``||input:tempo de execução (ms)||``,
 que é encontrada no menu ``||input:input||``,``||input:mais||``.
Assim armazenaremos o instante em que a peça entra no campo de detecção do sensor.

```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
        actuators.SetSpeedMotor(450, OutputPorts.P16)
    } else {
        actuators.StopMotor(OutputPorts.P16)
    }
})
let Entrada = 0
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
let Descarte = 0
let Bits = 0
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P0) == 120) {
        Entrada = input.runningTime()
    }
})
```

## Passo 6: Detectando peças com o sensor infravermelho
Adicione um ``||Loops:Loop Enquanto||`` abaixo da definição anterior.

Copie e cole (ctrl+C e ctrl+V) a condição feita anteriormente para o sensor, ``||Sensors:Valor do sensor infravermelho P1 >= 120||`, posicione no lugar da condição ``||Logic:falso||``.

Acesse a aba ``||Music:Música||`` e pegue o bloco ``||Music:play tone C Médio for 1 batida untill done||``, coloque o bloco dentro de ``||Loops:executar||``. Essa ação determina que enquanto a peça estiver na área de detecção do sensor um bip será tocado.


```blocks
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
        actuators.SetSpeedMotor(450, OutputPorts.P16)
    } else {
        actuators.StopMotor(OutputPorts.P16)
    }
})
let Entrada = 0
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
let Descarte = 0
let Bits = 0
basic.forever(function () {
    if (sensors.infraredValue(InputPorts.P0) == 120) {
        Entrada = input.runningTime()
        while (sensors.infraredValue(InputPorts.P0) == 120) {
            music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
        }
    }
})

```

## Passo 7: Detectando peças com o sensor infravermelho

Abaixo do laço ``||Loops:enquanto||`` copie e cole a definição da variável entrada, ``||Variables:definir entrada para tempo de execução (ms)||``, altere ``||Variables:entrada||`` para ``||Variables:saída||``. Assim armazenaremos o instante em que a peça sai do campo de detecção do sensor.

O próximo passo é a definição da variável ``||Variables:tempo||``, abaixo da última definição adicione ``||Variables:definir tempo para 0||``, 
no menu ``||Math:Matemática||`` use o bloco ``||Math:0-0||`` e posicione-o no lugar do 0 da definição da variável.
Substitua os números 0 da expressão matemática pelas variáveis ``||Variables:Saida||`` e ``||Variables:Entrada||``. Esse cálculo indica que ``||Variables:tempo||`` é a permanência total da peça dentro do campo de detecção do sensor.

Por fim no menu ``||Advanced:Avançado||`` vá até ``||Functions:Funções||``, Fazer uma função..., crie uma função chamada ``||Functions:teste||``. Adicione a função criada no código e no fim da condição ``||logic: se então||`` chame a função ``||functions:Ligar Teste||``
retirada de ``||Functions:Funções||``.

```blocks
function teste () {
	
}
input.onButtonPressed(Button.A, function () {
    Ligado = !(Ligado)
    if (Ligado) {
        actuators.SetSpeedMotor(450, OutputPorts.P16)
    } else {
        actuators.StopMotor(OutputPorts.P16)
    }
})
let tempo = 0
let Saida = 0
let Entrada = 0
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
let Descarte = 0
let Bits = 0
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
## Passo 8: Verificando o tamanho das peças

Dentro da função ``||Functions:Teste||`` adicione uma bloco ``||Logic:se então senão||``.
Troque a célula verdadeiro por uma célula ``||Logic:ou||``, que pode ser encontrada em ``||Logic:Lógica||``.
Posicione em cada um dos campos da célula ``||Logic:ou||`` uma comparação ``||Logic: 0 < 0||``. 
Na primeira comparação verificaremos se ``||Variables:Tempo < 250||``, na segunda comparaçao verificaremos se ``||Variables:Tempo > 750||``

Se a peça estiver com o tamanho adequado o tempo total pra ela percorrer o campo de detecção será entre 250ms e 750ms, já que a velocidade do motor é constante.

```blocks
function teste () {
    if (tempo < 250 || tempo < 750) {
    	
    } else {
    	
    }
}
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
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
let Descarte = 0
let Bits = 0
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

## Passo 9: Verificando o tamanho das peças

Adicionaremos agora as ações caso as peças se encontrem ou não dentro do padrão estabelecido.

Se estiverem fora do padrão, somaremos 1 unidade a ``||Variables:Descarte||`` e chmaremos a função ``||Functions:Erro||``.
Para incrementar a variavel use o bloco ``||Variables:alterar Descarte por 1||``. Na aba ``||Functions:Funções||``, clique em **Fazer uma função...**, nomeie-a erro e coloque-a no código.
Abaixo do último bloco adicionado acrescente um ``||Functions:ligar Erro||``, nos próximos passos implementaremos esta função.

Senão, se as peças estiverem dentro do padrão, apenas incrementaremos a variável ``||Variables:Bits||``, que guarda o total de peças avaliadas. 
Copie o bloco ``||Variables:alterar Descarte por 1||``, posicione dentro de ``||Logic:senão||`` e altere ``||Variables:Descarte||`` para ``||Variables:Bits||``

```blocks
function Erro () {
	
}
function teste () {
    if (tempo < 250 || tempo < 750) {
        Descarte += 1
        Erro()
    } else {
        Bits += 1
    }
}
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
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
let Descarte = 0
let Bits = 0
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

## Passo 10: Criando a função de erro

Caso uma peça esteja fora do padrão, ela deve ser rejeitada e o sistema precisa indicar o erro.

Acesse a aba ``||Actuators:Atuadores||``, pegue o bloco ``||Actuators: Motor CC, parar na porta P16||`` e coloque dentro da função erro. Assim o motor irá parar sempre que uma peça estiver fora do padrão.

Vá até a aba ``||Basic:Básico||`` e cloque o bloco ``||Basic:Mostrar ícone||`` depois do comendo para parar o motor, escolha o ícone **X** para que a matriz de leds indique o erro.
```blocks
function Erro () {
    actuators.StopMotor(OutputPorts.P16)
    basic.showIcon(IconNames.No)
}
function teste () {
    if (tempo < 250 || tempo < 750) {
        Descarte += 1
        Erro()
    } else {
        Bits += 1
    }
}
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
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
let Descarte = 0
let Bits = 0
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

## Passo 11: Criando a função de erro

Ainda na função erro, adicione um ``||Loops:Enquanto||``, altere a condição de ``||Logic:falso||`` para o inversor ``||Logic:não||``, que é encontrado na aba ``||Logic:Lógica||``.

No menu ``||Input:Input||``, use o bloco ``||Input:botão A é pressionado||`` e coleque-o dentro do campo vazio do inversor.
Em ``||Músic:Música||`` pegue o bloco ``||Music:play tone B Agudo for 1 batida untill done||`` e coloque dentro de ``||Loops:executar||``, 
daí garantimos que um alarme é soado até alguém intervir apertando o botão A e verificando o erro.

Por fim vá até ``||Basic:Básico||``, pegue o comando ``||Basic:limpar tela||`` e coloque no fim da função ``||Functions:erro||``, 
para que a tela seja limpa após verificação do erro.

```blocks
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
let Ligado = false
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
Ligado = false
let Descarte = 0
let Bits = 0
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

## Passo 12: Criando um evento para exibir os contadores

Queremos que o micro:bit exiba o número de peças aceitas e descartadas ao tocar no logo.

Vá até a aba ``||Input:Input||`` e adicione um bloco ``||Input:no logotipo pressionado||``.
Depois na aba ``||Basic:Básico||``, adicione dois blocos ``||Basic:mostrar número||``, um para ``||Variables:Bits||`` e outro para ``||Variables:Descarte||``.
Busque as variáveis em ``||Variables:Variáveis||`` e depois substirua os números 0.
Finalize com ``||Basic:limpar tela||``.

```blocks
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

## Passo 13: Testando o Código
Agora seu código está pronto! 🛠️

✅ Baixe o código para o micro:bit.

✅ Conecte a esteira à porta P16 e o sensor infravermelho à porta P1.

✅ Pressione o botão A para ligar a esteira.

✅ Coloque peças na esteira e observe a contagem.

✅ Se uma peça for muito pequena ou muito grande, o sistema para e alerta o erro.

✅ Toque no logo do micro:bit para ver o número de peças aceitas e descartadas.

```package
fuzzyBot=github:FuzzyMakers/pxt-fuzzyMakers
```
