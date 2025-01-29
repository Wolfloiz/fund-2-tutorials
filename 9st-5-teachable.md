# Teachable Machine + Micro:bit

## Passo 1
Agora que temos nossa rede neural treinada e pronta para uso, 
vamos aprender a conectá-la ao Micro:bit para aproveitar essa inteligência em nossos projetos.

## Passo 2

Para realizar essa conexão com o Micro:bit, usaremos a comunicação serial através da porta USB da placa
com o seu computador. Portanto, lembre-se de conectar a plaquinha a alguma entrada USB de seu dispositivo.

## Passo 3

Clique na aba **Avançado** para abrir novas categorias de blocos. Procure a seção ``||Serial:Serial||`` e adicione 
o comando ``||Serial:serial redirecionar para USB||`` dentro do laço ``||Basic:no iniciar||``.

```blocks
serial.redirectToUSB()
basic.forever(function () {
	
})
```

## Passo 4

Em seguida, acesse a categoria ``||Variables:Variáveis||`` e crie uma variável denominada ``||Variables:Letra||``.
Adicione o comando ``||Variables:Definir Letra para 0||`` dentro do laço ``||Basic:sempre||``.

```blocks
let Letra = 0
serial.redirectToUSB()
basic.forever(function () {
    Letra = 0
})
```

## Passo 5

Feito isso, devemos definir o valor da variável ``||Variables:Letra||`` como o que o Micro:bit está recebendo 
ao ler a porta serial. Para isso, retorne à categoria ``||Serial:Serial||`` e insira o bloco circular ``||Serial:serial ler até (new line ())||``. 

**Dica:** O delimitador "new line" (nova linha) é utilizado para indicar o final de uma mensagem ou comando enviado pela porta serial. 
Isso ajuda o Micro:bit a saber onde termina a informação que está sendo recebida. 
No código, ele garante que cada mensagem seja processada separadamente, sem misturar os dados recebidos.

```blocks
let Letra = ""
serial.redirectToUSB()
basic.forever(function () {
    Letra = serial.readUntil(serial.delimiters(Delimiters.NewLine))
})
```

## Passo 6

Por fim, devemos exibir a letra recebida na tela do Micro:bit. Então, adicione o bloco ``||Basic:mostrar string||`` localizado na aba ``||Basic:Básico||``.

```blocks
let Letra = ""
serial.redirectToUSB()
basic.forever(function () {
    Letra = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    basic.showString("Hello!")
})
```

## Passo 7

Altere a string que será exibida de **"Hello!"** para a variável ``||Variables:Letra||``.

```blocks
let Letra = ""
serial.redirectToUSB()
basic.forever(function () {
    Letra = serial.readUntil(serial.delimiters(Delimiters.NewLine))
    basic.showString(Letra)
})
```

## Passo 8

Agora, teste sua rede neural fazendo os gestos das letras como você fez em seu treinamento e verifique
se o Micro:bit está exibindo os caracteres corretos. Faça gestos diferentes e letras não treinadas para 
observar como ele vai se comportar.

Reflita sobre os resultados, experimente novas ideias de treinamento para sua rede neural e explore incrementos no código do Micro:bit.