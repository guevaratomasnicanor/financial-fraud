🛡️ Financial Fraud Detection: PaySim Analysis
📌 Project Overview
Este proyecto desarrolla un modelo de clasificación binaria para predecir transacciones fraudulentas en un sistema de pagos móviles. Utilizando el dataset sintético PaySim, el objetivo fue identificar patrones de comportamiento criminal en un mar de millones de transacciones legítimas.

The Challenge
El fraude financiero es un problema de "aguja en un pajar". En este dataset, las transacciones fraudulentas representan menos del 0.1% del total, lo que requiere un manejo cuidadoso del desbalance de clases y una selección precisa de variables.

🔍 Key Insights & Discovery
A través de un Análisis Exploratorio de Datos (EDA) profundo, identificamos tres pilares que definen el fraude en este sistema:

Filtro de Canales: El 100% de los casos de fraude ocurren exclusivamente en los tipos TRANSFER y CASH_OUT. Las transacciones de tipo Payment o Debit no mostraron actividad maliciosa.

Correlación de Riesgo: Se observó que a mayor valor de la variable amount y en pasos temporales (step) más avanzados, la probabilidad de fraude aumenta.

El Patrón "Zero Balance": Nuestro hallazgo más crítico. En prácticamente todas las transacciones fraudulentas, el saldo de la cuenta de origen (oldbalanceOrg) se transfiere íntegramente, dejando un newbalanceOrig de 0. Este comportamiento es extremadamente inusual en usuarios legítimos.

📊 Performance Metrics
Gracias a la ingeniería de características basada en el vaciado de cuentas, logramos resultados operativos de alta eficiencia:

Métrica	Resultado	Significado
Recall (Sensibilidad)	98%	Capturamos casi la totalidad del fraude existente.
Precisión	75%	Solo 1 de cada 4 alertas es un falso positivo, optimizando el tiempo de los analistas.
🛠️ Data Dictionary
El modelo analiza el flujo de dinero entre cuentas mediante las siguientes variables:

step: Unidad de tiempo (1 step = 1 hora de simulación).

type: Tipo de transacción (CASH-IN, CASH-OUT, DEBIT, PAYMENT, TRANSFER).

amount: Monto de la transacción en moneda local.

oldbalanceOrg / newbalanceOrig: Saldo antes y después de la transacción (Origen).

oldbalanceDest / newbalanceDest: Saldo antes y después de la transacción (Destino).

isFraud: Nuestra variable objetivo (Agente fraudulento tomando el control de la cuenta).

🚀 Key Takeaway
La lógica del fraude detectada es simple pero letal: El atacante intenta vaciar la cuenta de la víctima mediante una transferencia a una cuenta puente y luego realiza un Cash-out para liquidar los fondos. El modelo captura esta secuencia con una precisión superior a los sistemas de reglas tradicionales.

¿Te gustaría que redacte también una sección sobre cómo manejar el desbalance de datos (como el uso de SMOTE o sub-sampling) para completar la parte técnica del README?
