
# Select

---

- [Select](#select)
    - [Exemplo básico](#exemplo-básico)
    - [Adicionando condição de saída](#adicionando-condição-de-saída)
    - [Personalizando a pergunta ao usuário](#personalizando-a-pergunta-ao-usuário)

>Esta aula é um complemento para a aula 10 (For)
Fazendo os exercícios das aulas anteriores, você deve ter notado que montar um menu para o usuário escolher um valor não é uma tarefa muito simples.

## Exemplo básico

Para resolver este problema de uma forma simples, podemos usar o laço de repetição select. Este laço permite que o usuário escolha valores para selecionar elementos de uma lista de variáveis. Veja o exemplo abaixo:

```shell
frutas="maca banana morango mamao melao uva abacaxi tamarindo pera"
select fruta in $frutas; do
    echo "Fruta escolhida: $fruta"
done
```

Se você executar o exemplo acima, verá que o que é solicitado ao usuário após a listagens dos dados é:

``` text
1) maca	      3) morango    5) melao	  7) abacaxi	9) pera
2) banana     4) mamao	    6) uva	  8) tamarindo
#?
```

perceba que este laço de repetiçõ é infinito. Toda vez que um elemento for escolhido, a pergunta folta a ser feita ao usuário.

## Adicionando condição de saída

Para resolver o problema do exemplo básico (acima), adicione a opção de saída na lista, e implemente a condição de saída dentro do loop:

```shell
frutas="maca banana morango mamao melao uva abacaxi tamarindo pera sair"
select fruta in $frutas; do
    if [[ $fruta == "sair"]]; then
        break
    fi
    echo "Fruta escolhida: $fruta"
done
```

Dessa forma, quando o usuário escolher a opção "sair", o comando _break_ fará a saída do loop _select_.

## Personalizando a pergunta ao usuário

A pergunta feita ao usuário não é muito intuitiva:
> #?

A melhor forma de alterar a pergunta feita ao usuário é alterando a variável que o interpretador usa para armazenar a pergunta. No bash, esta variável é _PS3_. Você pode alterá-la dentro do script, antes de usar o comando select:

```shell
PS3="Escolha uma fruta:"
frutas="maca banana morango mamao melao uva abacaxi tamarindo pera sair"
select fruta in $frutas; do
    if [[ $fruta == "sair"]]; then
        break
    fi
    echo "Fruta escolhida: $fruta"
done
```

O resultado será:

``` text
1) maca	        3) morango     5) melao	      7) abacaxi     9) pera
2) banana       4) mamao       6) uva	      8) tamarindo  10) sair
Escolha uma fruta:
```
