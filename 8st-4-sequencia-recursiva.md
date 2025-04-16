# Fibonacci

## Passo 1

Neste tutorial, vamos programar a sequência de Fibonacci no Micro:bit! O botão A, será usado para carregar e exibir os 2 primeiros números da sequência. O botão B, quando pressionado, calculará e exibirá os próximos números. Vamos começar!


## Passo 2

Acesse a aba ``||Variables:Variáveis||`` e crie três novas variáveis: ``||Variables:atual||``, ``||Variables:ultimo||`` e ``||Variables:penultimo||``.

Em seguida, arraste para dentro do laço ``||Basic:no iniciar||`` a definição das 3 variáveis: ``||Variables:definir penultimo para 0||``, ``||Variables:definir ultimo para 1||``, ``||Variables:definir atual para 0||``.
Essa inicialização é importante para definir o começo da sequência.

```blocks
let penultimo = 0
let atual = 0
let ultimo = 1
```

## Passo 3

Agora, vamos configurar o botão A para exibir os primeiros números da sequência.
Vá até a aba ``||input:input||`` e adicione o bloco ``||Input:quando botão A for pressionado||``.
Dentro desse bloco, procure na aba ``||Logic:Lógica||`` o bloco ``||Logic:se verdadeiro então||`` e adicione dentro da ação do botão A. Ainda na mesma aba pegue o bloco comparador ``||Logic:0 < 0||`` e substitua a expressão ``||Logic:verdadeiro||``.
Nos campos "0" do comparador, insira a variável ``||Variables:atual||``, atualize o outro valor para 1 e o sinal para < (menor): ``||Logic:se atual < 1 então||``, assim o botão A terá a função de carregar os dois primeiros números da lista 0 e 1.

```blocks
input.onButtonPressed(Button.A, function () {
    if (atual < 1) {
    	
    }
})
let atual = 0
let penultimo = 0
atual = 0
let ultimo = 1
```


## Passo 4

Dentro do ``||Logic:se||``, adicione: ``||Basic:mostrar número 0||``. 
Troque o número 0 pela variável ``||Variables:atual||``. Isso garantirá a exibição do primeiro número da sequência, o 0.

Ainda dentro do ``||Logic:se||`` adicione o bloco ``||Variables:definir atual para 1||``. Assim na segunda vez que o botão for pressionado o Micro:bit exibirá o número 1 que é o segundo número da sequência.

```blocks
input.onButtonPressed(Button.A, function () {
    if (atual < 1) {
        basic.showNumber(atual)
        atual = 1
    }
})
let atual = 0
let penultimo = 0
atual = 0
let ultimo = 1
```

## Passo 5

Agora, configure o botão B para calcular e exibir o próximo número de Fibonacci. 

Vá até a aba ``||input:input||`` e adicione o bloco ``||Input:quando botão B for pressionado||``.

Pegue na seção ``||Logic:Lógica||``  um bloco ``||Logic:se verdadeiro então||`` e encaixe dentro da lógica do botão B. Ainda na mesma seção pegue o bloco comparador ``||Logic:0 < 0||`` e substitua a expressão ``||Logic:verdadeiro||``.

Nos campos "0" da comparação, insira a variável ``||Variables:atual||``, atualize o outro valor para 1 e o sinal para > (maior ou igual): ``||Logic:se atual >= então||``, assim o botão B terá a função de carregar os números subsequentes após o 0 e 1.

```blocks
input.onButtonPressed(Button.A, function () {
    if (atual < 1) {
        basic.showNumber(atual)
        atual = 1
    }
})
input.onButtonPressed(Button.B, function () {
    if (atual >= 1) {
    	
    }
})
let atual = 0
let penultimo = 0
atual = 0
let ultimo = 1
```

## Passo 6

Dentro do ``||Logic:se||`` do botão B, adicione um bloco ``||Variables:definir atual para 0||``, substitua o valor de 0 por uma expressão ``||Math: 0 + 0||`` do submenu ``||Math: Matemática||``, troque os valores de 0 para as variáveis ``||Variables:ultimo||`` e ``||Variables:penultimo||``.
Assim sempre que o botão B é pressionado ``||Variables:atual||`` é atualizada com os 2 últimos números da sequência.

Acrescente ``||Basic:mostrar número 0||`` para exibir o último valor da sequência atualizado. Troque o valor de 0 para ``||Variables:atual||``.

````blocks

input.onButtonPressed(Button.A, function () {
    if (atual < 1) {
        basic.showNumber(atual)
        atual = 1
    }
})
input.onButtonPressed(Button.B, function () {
    if (atual >= 1) {
        atual = ultimo + penultimo
        basic.showNumber(atual)
    }
})
let ultimo = 0
let atual = 0
let penultimo = 0
penultimo = 0
atual = 0
ultimo = 1

````

## Passo 7

Para finalizar, vamos atualizar os valores das variáveis ``||Variables:ultimo||`` e ``||Variables:penultimo||``.

Coloque no comando do botão B os seguintes blocos: ``||Variables:definir penultimo para ultimo||`` e ``||Variables:definir ultimo para atual||``.

Assim as variáveis são atualizadas de forma que na próxima ação do botão B, o próximo valor da série receba os 2 últimos valores somados.

```blocks
input.onButtonPressed(Button.A, function () {
    if (atual < 1) {
        basic.showNumber(atual)
        atual = 1
    }
})
input.onButtonPressed(Button.B, function () {
    if (atual >= 1) {
        atual = ultimo + penultimo
        basic.showNumber(atual)
        penultimo = ultimo
        ultimo += atual
    }
})
let ultimo = 0
let atual = 0
let penultimo = 0
penultimo = 0
atual = 0
ultimo = 1

```

## Passo 8

Teste seu código!

Pressione o botão A para iniciar a sequência. Após carregar os valores de 0 e 1, pressione o botão B para ver os próximos números.

Agora seu Micro:bit exibe a sequência de Fibonacci sempre que o botão for pressionado!