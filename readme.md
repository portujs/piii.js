# Piii.js

> Um avançado filtro de palavrões.

[![Build Status](https://travis-ci.org/theuves/piii.js.svg?branch=master)](https://travis-ci.org/theuves/piii.js)

## Características

- ignora o uso de qualquer tipo acentuação
- ignora se as palavras estão em caixa alta ou baixa
- ignora números que possam substituir letras
- ignora letras repetidas

## Instalação

Instale-o via linha de comando com:

- [*bower*](http://bower.io/) ― `bower install --save piii.js`.
- [*npm*](https://npmjs.com/) ― `npm install --save piii`.

## Sintaxe

```
piii(string[, censura[, exceções]])
```

### Parâmetros

- `string` ― A *string* que será filtrada.
- `censura` (*opcional*) ― Uma *string* para substituir cada palavrão, ou uma função para processar o palavrão antes de substituí-lo na *string*. Por padrão `censura` é um `*` (asterisco).
- `exceções` (*opcional*) ― Uma array com uma lista dos palavrões que não devem ser filtrados.

#### O Parâmetro `censura` Como Uma Função

Este parâmetro pode ser uma função que recebe como único parâmetro uma *string* com o palavrão que está sendo filtrado no momento e deve retornar uma *string*, que substituirá aquele determinado palavrão.

Veja um exemplo (que adiciona a *tag HTML* `<del>` entre os palavrões):

```js
piii("Que porra é essa?", function (palavrao) {
  return "<del>" + palavrao + "</del>";
});

// Retorna "Que <del>porra</del> é essa?".
```

#### As Exceções

Nem todos os palavrões são vistos como impróprios, ofensivos ou obsenos por todas as pessoas, portanto é possível definir palavras que não devem ser filtrados na *string*.

Veja abaixo a lista de palavrões podem ser usados:

- `bilau`
- `boceta` (e `buceta` ― [com *u*](http://pseudolinguista.blogspot.com.br/2014/04/como-e-que-se-escreve-buceta-ou-boceta.html))
- `caralho`
- `cu`
- `merda`
- `pepeca`
- `pinto`
- `piroca`
- `porra` (e `poha`)
- `punheta` (e `ponheta`)
- `puta`
- `foder` (e `fuder` com toda a sua conjugação ― exceto no presente do indicativo e subjuntivo)

A letra *C* também é aceita como *K* em `caralho`, `cu`, e `piroca`.

Veja um exemplo (que desconsidera *merda* como um palavrão):

```js
piii("Que porra é essa? Que merda. Vá se foder!", undefined, [
  "merda"
]);

// Retorna "Que * é essa? Que merda. Vá se *!".
```

**Obs.**: com isto, é desconsiderado todas as formas de se escrever o palavrão (como no exemplo acima, seria desconsiderado, tanto *merda* quanto *merdinha*, *merrrda*, *m3rd4*, etc.).

## Exemplos

Veja alguns exemplos abaixo com diferentes tentativas de burlá-lo.

```js
piii("Vá tomar no cú!"); // Retorna "Vá tomar no *!".
piii("Vá se ⓕⓞⓓⓔⓡ!"); // Retorna "Vá se *!".
piii("Que m3rd4."); // Retorna "Que *.".
piii("Filho da ᵽṻțặ!"); // Retorna "Filho da *!".
piii("Que porrrrra é essa?"); // Retorna "Que * é essa?".
```

## Licença

MIT ([veja o arquivo](https://github.com/theuves/piii.js/blob/master/license))
