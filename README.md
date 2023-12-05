# FÓRMULAS DAX (POWER BI)

## Soma do Saldo Devedor por CPF:

### Descrição
Esta fórmula DAX calcula a soma do saldo devedor considerando apenas o primeiro registro de cada CPF na tabela.

#### Fórmula DAX

```DAX
SomaSaldoDevedor = 
SUMX (
    VALUES ( TABELA1[CPF] ),
    CALCULATE (
        FIRSTNONBLANK ( TABELA1[CPF], 1 ),
        FILTER (
            TABELA1,
            TABELA1[CPF] = EARLIER ( TABELA1[CPF] )
        )
    )
)
```

## Converter Hora em Minuto:

### Descrição
Esta fórmula calcula o tempo falado em minutos com base na coluna [TEMPO_FALANDO]. Ela utiliza as funções HOUR e MINUTE para extrair a parte da hora e a parte dos minutos da coluna [TEMPO_FALANDO], respectivamente. Em seguida, multiplica a parte da hora por 60 e adiciona a parte dos minutos para obter o tempo total em minutos.

### Fórmula

```DAX
.tempo_falado_minuto = HOUR([TEMPO_FALANDO]) * 60 + MINUTE([TEMPO_FALANDO])
```

## Máximo de horas logado:

### Descrição
Esta fórmula calcula a máxima quantidade de horas logadas em um determinado mês. Ela utiliza a função CALCULATE para modificar o contexto de avaliação das funções dentro dela. A função MAXX é usada para calcular o máximo da coluna [.tempo_logado_hora] no contexto de mes_atual. Além disso, a função FILTER é empregada para garantir que a avaliação seja realizada apenas para as linhas onde a coluna DATA em mes_atual não está vazia.

#### Fórmula

```DAX
.max_logado_hora = 
    CALCULATE(
        MAXX(mes_atual, [.tempo_logado_hora]),
        FILTER(mes_atual, mes_atual[DATA])
    )
```
