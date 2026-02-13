# financial-fraud
the goal is to predict fruadulent transactions
#variables
step, type, amount, oldbalanceOrg, newbalanceOrig, oldbalanceDest, newbalanceDest, isFraud, isFlaggedFraud
#insights
-Type of payment: Cashout an transfer are the only transaction types with fraud
- A mayor step hay mas posibilidades de que sea fraude
- A mayor monto mayor probabilidad de fraude
- 
Detectamos el 98% del fraude con un 75% de precisión. Esto gracias a que encontramos un patrón importante: Todas las cuentas que cometían fraude, vaciaban la cuenta. En el caso de las personas inocentes, ninguno realizaba este acto sospechoso. 
