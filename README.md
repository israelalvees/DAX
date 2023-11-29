# FÓRMULAS DAX (POWER BI)

## Soma do Saldo Devedor por CPF

### Descrição
Esta fórmula DAX calcula a soma do saldo devedor considerando apenas o primeiro registro de cada CPF na tabela BASE_HISTORICA.

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
