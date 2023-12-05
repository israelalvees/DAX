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

