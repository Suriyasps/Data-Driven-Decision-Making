# Data Driven Decision Making

## Project
**Project By**: Suriya Subbiah Perumal  
 

---

## Table of Contents

1. [ApTx-nova - Customized Automotive Tech](#1-aptx-nova---customized-automotive-tech)
2. [Teranikx - AI Chip](#2-teranikx---ai-chip)
3. [Make-to-Stock Chemotherapy Drugs](#3-make-to-stock-chemotherapy-drugs)

---

## 1) ApTx-nova - Customized Automotive Tech

ApTx-nova aims to determine optimal plant-product allocations to maximize production while respecting capacity and compatibility constraints.

### 1.1 Decision Variables
- Let `x_ij` be a binary variable:  
  `x_ij = 1` if product `i` is produced in plant `j`; otherwise `x_ij = 0`.

### 1.2 Objective Function
- Maximize:  
  `Z = Σ Σ c_ij * x_ij` for `i = 1 to 5`, `j = 1 to 4`

### 1.3 Constraints
- **Plant Capacity**: Each plant handles at most one product:  
  `Σ x_ij ≤ 1 for all i`
- **Product Production**: Each product must be produced in exactly one plant:  
  `Σ x_ij = 1 for all j`
- **Product-Plant Compatibility**:  
  - Product 2 cannot be made in plants 1, 3, 4:  
    `x_2,1 = x_2,3 = x_2,4 = 0`  
  - Product 3 cannot be made in plant 4:  
    `x_3,4 = 0`

### 1.4 Solution & Implementation in R
- Implemented using `ompr`, `ROI`, `GLPK`
- Output:  
Plant 1 → Product 1
Plant 2 → Product 2
Plant 4 → Product 4
Plant 5 → Product 3




---

## 2) Teranikx - AI Chip

Aims to optimize chip allocation from two fabs to four customers to maximize profit.

### 2.1 Data Summary
- **Fab A** capacity: 50M chips; production cost: ₰1150
- **Fab B** capacity: 42M chips; production cost: ₰1250
- **Customer demands & prices vary**
- **Delivery costs differ per Fab and customer**

### 2.2 Decision Variables
- `x_ij`: Chips from Fab `i` to Customer `j`

### 2.3 Objective Function
- Maximize:  
`Σ Σ (Price_j - ProdCost_i - DeliveryCost_ij) * x_ij`

### 2.4 Constraints
- Production capacity and customer demand must not be exceeded.

### 2.5 Solution
- Implemented in R (`ompr`)
- Optimal allocations:
Fab A → 36M to Customer 1, 14M to Customer 2
Fab B → 31M to Customer 2, 11M to Customer 3
Total Profit: ₰35,350M



---

## 3) Make-to-Stock Chemotherapy Drugs

Optimize drug mix using EU and US constituents to maximize profit and meet quality standards.

### 3.1 Decision Variables
- `x1, x2`: Chemo-1 & Chemo-2 with EU  
- `x3, x4`: Chemo-1 & Chemo-2 with US

### 3.2 Objective Function
- Maximize:  
`Z = 1200*(x1+x3) + 1400*(x2+x4) - (800*(x1+x2) + 1500*(x3+x4))`

### 3.3 Constraints
- Demand, inventory, D-metric ≤ 23, P-metric ≥ thresholds

### 3.4 Optimal Plan
- Chemo-1: 100,000 vials (75,455 EU + 24,545 US)  
- Chemo-2: 10,000 vials (4,545 EU + 5,455 US)  
- Monthly profit: €25 million  
- D-metrics: 22.54 (Chemo-1), 20 (Chemo-2)  
- P-metrics: 89.7 (Chemo-1), 93 (Chemo-2)

---

## Tools Used
- R, `ompr`, `ROI`, `GLPK`
- Optimization Modeling & Linear Programming

