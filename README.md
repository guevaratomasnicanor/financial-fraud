# 🛡️ Financial Fraud Detection — PaySim Analysis

## 📌 Project Overview
Este proyecto desarrolla un **modelo de clasificación binaria** para detectar transacciones fraudulentas en un sistema de pagos móviles.  
Utilizando el dataset sintético **PaySim**, el objetivo es identificar patrones de fraude financiero en un entorno altamente desbalanceado, donde la gran mayoría de las transacciones son legítimas.

El enfoque combina **Análisis Exploratorio de Datos (EDA)**, **ingeniería de características basada en comportamiento** y **modelado supervisado**, priorizando métricas operativas relevantes para sistemas antifraude reales.

---

## ⚠️ The Challenge
El fraude financiero es un problema clásico de **“aguja en un pajar”**:

- Las transacciones fraudulentas representan **menos del 0.1%** del total  
- Un modelo naïve puede alcanzar alta accuracy ignorando el fraude  
- El principal desafío es **maximizar el recall sin disparar falsos positivos**

Esto requiere:
- Manejo cuidadoso del **desbalance de clases**
- Selección inteligente de variables
- Enfoque en **patrones de comportamiento**, no solo en montos

---

## 🔍 Key Insights & Discoveries
A partir de un **EDA exhaustivo**, se identificaron tres pilares fundamentales que definen el fraude en este sistema:

### 1️⃣ Channel Filtering
- **100% del fraude ocurre en `TRANSFER` y `CASH_OUT`**
- Tipos como `PAYMENT` y `DEBIT` no presentan actividad fraudulenta
- Permite reducir significativamente el espacio de búsqueda del modelo

### 2️⃣ Risk Correlation
- A mayor valor de `amount`, mayor probabilidad de fraude
- El riesgo aumenta en **steps temporales más avanzados**
- Sugiere un comportamiento progresivo del atacante

### 3️⃣ The “Zero Balance Pattern” (Hallazgo Clave)
- En casi todas las transacciones fraudulentas:
  - `oldbalanceOrg` se transfiere íntegramente
  - `newbalanceOrig = 0`
- Este **vaciado total de cuenta** es extremadamente inusual en usuarios legítimos
- Se convierte en la **señal predictiva más fuerte del modelo**

---

## 📊 Model Performance
Gracias a la ingeniería de características basada en el patrón de vaciado de cuentas, el modelo logra un desempeño altamente eficiente:

| Métrica | Resultado | Significado |
|------|---------|------------|
| **Recall (Sensibilidad)** | **98%** | Captura casi la totalidad del fraude existente |
| **Precisión** | **75%** | Solo 1 de cada 4 alertas es un falso positivo |

👉 Este balance es ideal para entornos reales, donde **perder fraude es más costoso que investigar alertas**.

---

## 🛠️ Data Dictionary
El modelo analiza el flujo de dinero entre cuentas utilizando las siguientes variables:

| Variable | Descripción |
|-------|------------|
| `step` | Unidad temporal (1 step = 1 hora de simulación) |
| `type` | Tipo de transacción (`CASH-IN`, `CASH-OUT`, `DEBIT`, `PAYMENT`, `TRANSFER`) |
| `amount` | Monto de la transacción |
| `oldbalanceOrg` | Saldo de la cuenta origen antes de la transacción |
| `newbalanceOrig` | Saldo de la cuenta origen después de la transacción |
| `oldbalanceDest` | Saldo de la cuenta destino antes de la transacción |
| `newbalanceDest` | Saldo de la cuenta destino después de la transacción |
| `isFraud` | Variable objetivo (1 = fraude, 0 = legítimo) |

---

## 🚀 Key Takeaway
La lógica del fraude detectada es **simple pero letal**:

> El atacante toma control de una cuenta, **la vacía completamente mediante una `TRANSFER`**, y luego ejecuta un **`CASH_OUT`** para liquidar los fondos.

El modelo captura esta secuencia con una **precisión superior a los sistemas basados únicamente en reglas**, demostrando el valor del **análisis de comportamiento financiero** frente a enfoques tradicionales.

---

