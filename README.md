# FÓRMULAS DAX (POWER BI)

## Soma do Saldo Devedor por CPF

### Descrição
Esta fórmula DAX calcula a soma do saldo devedor considerando apenas o primeiro registro de cada CPF na tabela BASE_HISTORICA.

#### Fórmula DAX

```DAX
SomaSaldoDevedor = 
SUMX (
    VALUES ( BASE_HISTORICA[BAS_CPF_CNPJ] ),
    CALCULATE (
        FIRSTNONBLANK ( BASE_HISTORICA[BAS_SALDO_DEVEDOR], 1 ),
        FILTER (
            BASE_HISTORICA,
            BASE_HISTORICA[BAS_CPF_CNPJ] = EARLIER ( BASE_HISTORICA[BAS_CPF_CNPJ] )
        )
    )
)
