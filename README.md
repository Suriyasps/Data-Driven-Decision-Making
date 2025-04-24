# Data-Driven-Decision-Making

1
MGT7180 - Data Driven Decision Making
Assignment -1
Student Name : Suriya Subbiah Perumal
Student ID : 40423910
2
Table of Contents
1. ApTx-nova - Customized Automotive Tech …………………. 01
1.1 Assigning The Decision Variables ……………………………………….... 01
1.2 Objective Function …………………………………. ……………………... 01
1.3 Constraints ………………………………………………………………..… 02
1.3.1 Plant Capacity Constraint ………………………………………………. 02
1.3.2 Product Production Constraint …………………………………………. 02
1.3.3 Product-Plant Compatibility ………………………………………….… 03
1.4 Final Model …………………………………..……………………………. 03
1.5 Solving the Model ………………………………………………………..… 04
1.5.1 Implementation of Mathematical Model in R ………………………….. 04
1.5.2 R Output Solution …………………………………..………………….. 05
1.6 Managerial Statement …………………………………………………..….05
2. Teranikx - AI Chip …………………………………………………… 07
2.1 Given Data …………………………………………………………………. 07
2.2 Assigning The Decision Variables ………………………………….……..08
2.3 Objective Function …………………………………..……………………. 08
2.4 Constraints ……………………………………………………………….... 08
2.4.1 Production Capacity Constraint ………………………………………... 08
2.4.2 Demand Constraint ………………………………….…………………... 08
2.5 Final Model ………………………………….………………………….... 09
2.6 Solving the Model ………………………………….……………………... 09
2.6.1 Implementation of Mathematical Model in R ……………………….… 10
2.6.2 R Output Solution ………………………………….………………….. 10
2.7 Managerial Statement ………………………………….………………… 11
3. Make-to-Stock Chemotherapy Drugs …………………………… 12
3.1 Assigning The Decision Variables ………………………………………. 12
3.2 Objective Function ………………………………….……………………. 12
3.3 Constraints ………………………………….…………….………………. 12
3.3.1 Maximum Demand Constraints ……………………………………….. 12
3.3.2 Minimum Delivery Constraints ………………………………………... 13
3.3.3 Inventory Constraints ………………………………….……………….. 13
3.3.4 Maximum D-Metric Constraints ………………………………………. 13
3.3.5 Minimum P-Metric Constraints ………………………………………. 14
3.4 Final Model ………………………………….…………….……………... 14
3.5 Solving the Model ………………………………….…………………...… 16
3.5 .1 Implementation of Mathematical Model in R ……………………….. 16
3.5.2 R Output Solution ………………………………….………………….. 17
3.6 Managerial Statement ………………………………….…………………. 18
3
1) ApTx-nova - Customized Automotive Tech
ApTx-nova is tasked with deciding which of their five plants should produce each of
their four products to maximize total production, considering capacity constraints and
product-plant compatibility.
1.1 Assigning The Decision Variables :
Let xij be a binary decision variable where i corresponds to product (i= 1,2,3,4,5)
and j corresponds to plant ( j=1,2,3,4). xij = 1 if product i is manufactured in plant j,
and 0 otherwise. ( 𝑥𝑖𝑗 ∈ ℤ+ for 𝑖 = 1, 2,3,4,5 & j = 1,2,3,4 )
1.2 Objective Function :
The objective is to maximize the total production. Therefore, the objective function
can be written as:
𝑀𝑎𝑥𝑖𝑚𝑖𝑧𝑒 𝑍 = 𝑖=1
5
𝑗=1
Σ Σ4 (𝑐𝑖𝑗 ∗ 𝑥𝑖𝑗)
𝑖𝑗 0 for 𝑖 = 1,2,3,4,5 & j = 1,2,3,4
where,
 Z is the total number of batches manufactured during the production period
 c is the capacity of plant i for product j
1.3 Constraints :
1.3.1 Plant Capacity Constraint :
Each plant can be scheduled for at most one product.
𝑗=1
4
􀷍𝑥𝑖𝑗 ≤ 1, ∀𝑖 ∈ {1, 2, 3, 4,5}
1.3.2 Product Production Constraint :
Each product must be produced in exactly in one plant
𝑖=1
5
􀷍𝑥𝑖𝑗 = 1, ∀𝑗 ∈ {1, 2, 3, 4}
4
1.3.3 Product-Plant Compatibility :
Certain products are incompatible with specific plants for production. For instance,
products 2 cannot be produced by plants 1, 3, and 4, and similarly, product 3
cannot be manufactured by plant 4.
 For product 2 which cannot be manufactured in plants 1, 3, and 4:
𝑥1,2 = 𝑥3,2 = 𝑥4,2 = 0
 For product 3 which cannot be manufactured in plants 4:
𝑥4,3 = 0
Product 1 2 3 4
Plant-1 1200 600 1000
Plant-2 1400 1200 800 1000
Plant-3 600 200 600
Plant-4 800 1200
Plant-5 800 1400 1000 1600
The red-highlighted cells indicate the plant-product pairings that are incapable of
production, signifying that those specific plants cannot manufacture the corresponding
products.
1.4 Final Model :
𝑀𝑎𝑥𝑖𝑚𝑖𝑧𝑒 𝑍 =
𝑖=1
5
𝑗=1
4
􀷍􀷍(𝑐𝑖𝑗 ∗ 𝑥𝑖𝑗)
𝑖𝑗 0 for 𝑖 = 1,2,3,4,5 & j = 1,2,3,4
Subject to the following constraints :
Plant Capacity :
𝑖=1
5
􀷍𝑥𝑖𝑗 ≤ 1, ∀𝑗 ∈ {1, 2, 3, 4}
𝑖𝑗 0 for 𝑖 = 1,2,3,4,5 & j = 1,2,3,4
5
Product Production :
𝑗=1
4
􀷍𝑥𝑖𝑗 = 1, ∀𝑖 ∈ {1, 2, 3, 4,5}
Product-Plant Compatibility :
𝑥2,1 = 𝑥2,3 = 𝑥2,3 = 0
𝑥3,4 = 0
1.5 Solving the Model :
The mathematical model was crafted into an R script and executed using the `ompr`
package, supplemented by additional packages like `ROI`, the `ROI plugin`, and
`GLPK`, among others. This execution aimed to solve the mathematical model
efficiently, aiming to ascertain the optimal solution that maximizes the number of
batches produced while minimizing the company's expenditure.
1.5.1 Implementation of Mathematical Model in R :
6
1.5.2 R Output Solution :
1.6 Managerial Statement :
In order to maximize the production ApTx-nova should following allocation of plants
for the production of products
 Plant - 1 should be allocated for the production of product - 1
 Plant - 2 should be allocated for the production of product - 2
 Plant - 4 should be allocated for the production of product - 4
 Plant - 5 should be allocated for the production of product - 3
Product 1 2 3 4
Plant-1 1200 600 1000
Plant-2 1400 1200 800 1000
Plant-3 600 200 600
Plant-4 800 1200
Plant-5 800 1400 1000 1600
7
Plant-1
Product - 1
Plant-2
Product - 2
Plant-3
Product - 3
Plant-4
Product - 4
Plant-5
A total production target of 4,600 batches must be achieved within a given
production period.
8
2) Teranikx - AI Chip
Teranikx , a company known for its economical production of ASIC chips, this
analysis aims to determine the optimal production levels for two of their
manufacturing facilities. Considering the operational constraints and demand,
alongside the variable pricing and delivery charges from four distinct customers, this
solution seeks to strategize production to not only meet customer demands but also to
ensure maximization of profit. This involves a detailed evaluation of each facility's
production capabilities, costs, and the financial implications of servicing different
customer segments, including the provision of onsite support.
2.1 Given Data
Fab Capacities :
 The production capacities of Fab A is 50
 The production capacities of Fab B is42
Production Cost :
 The production cost of one chip at Fab A is ₰ 1150
 The production cost of one chip at Fab B is ₰ 1250
Demand :
 The maximum demand of customer - 1 is 36 million chips
 The maximum demand of customer - 2 is 46 million chips
 The maximum demand of customer - 3 is 11 million chips
 The maximum demand of customer - 4 is 35 million chips
Offered Prices :
 Price offered by customer - 1 for each chip is ₰ 1950
 Price offered by customer - 2 for each chip is ₰ 1850
 Price offered by customer - 3 for each chip is ₰ 2000
 Price offered by customer - 4 for each chip is ₰ 1800
Delivery Cost (Including Onsite Customer Support) :
From Fab - A :
 Cost of delivery to customer - 1 is ₰ 300
 Cost of delivery to customer - 2 is ₰ 400
 Cost of delivery to customer - 3 is ₰ 550
 Cost of delivery to customer - 4 is ₰ 450
From Fab - B :
 Cost of delivery to customer - 1 is ₰ 600
 Cost of delivery to customer - 2 is ₰ 300
 Cost of delivery to customer - 3 is ₰ 400
 Cost of delivery to customer - 4 is ₰ 250
9
2.2 Assigning Decision Variables :
Let xij be a binary decision variable where i corresponds to the Fab - A and Fab - B
(i= 1,2) and j corresponds to customers ( j=1,2,3,4). The decision is allocate the
chips produced at Fab - A and Fab - B to the customers optimally in order to
maximize the profit.
2.3 Objective Function :
𝑖=1
2
𝑗=1
4
𝑗 𝑖𝑗 𝑖 𝑖𝑗
𝑖𝑗
+ for 𝑖 = 1,2 & j = 1,2,3,4
Where ,
 P is the offered price by the customer.
 Dc is the delivery cost incurred for every chip produced based on the Fab ( i ) and
the customer ( j ).
 Pc is the production of every chip based on the Fab ( i ) in which it is produced.
2.4 Constraints :
2.4.1 Production Capacity Constraint:
The total chips shipped from each fab should not exceed its production capacity.
𝑗=1
4
𝑖𝑗 𝑖
Where ,
 C is the production capacity of each Fab in millions ( i ) .
2.4.2 Demand Constraint:
The total chips shipped to each customer should not exceed their maximum
demand.
𝑖=1
2
𝑖𝑗
10
Where,
 D is the maximum demand of chips by each customer in millions ( j ) .
2.5 Final Model :
𝑖=1
2
𝑗=1
4
𝑗 𝑖𝑗 𝑖 𝑖𝑗
𝑖𝑗
+ for 𝑖 = 1, 2,3,4,5 & j = 1,2,3,4
Subject to following Constraints :
Production Capacity Constraint:
𝑗=1
4
𝑖𝑗 𝑖
Demand Constraint:
𝑖=1
2
𝑖𝑗 𝑗
2.6 Solving the Model :
The mathematical model was crafted into an R script and executed using the `ompr`
package, supplemented by additional packages like `ROI`, the `ROI plugin`, and
`GLPK`, among others. This execution aimed to solve the mathematical model
efficiently, aiming to ascertain the optimal solution that maximizes profit to Teranikx.
11
2.6.1 Implementation of Mathematical Model in R :
2.6.2 R Output Solution :
12
2.7 Managerial Statement :
To maximize profits, Teranikx should adopt a strategy of selling the chip to its
various customers accordingly,
 36 million Chips from Fab - A should be delivered to customer -1
 14 million Chips from Fab - A should be delivered to customer -2
 31 million Chips from Fab - B should be delivered to customer -2
 11 million Chips from Fab - B should be delivered to customer -3
Customer 1 2 3 4
Fab - A 3600000 1400000 - -
Fab - B - 3100000 1100000 -
A
B
The highest possible profit from this deal would amount to ₰ 35,350 million.
13
3) Make-to-Stock Chemotherapy Drugs
Apotheeker Pharmaceuticals, a producer of two kinds of chemotherapy medications
named Chemo1 and Chemo2 for stock, aims to maximize its monthly earnings. To
achieve this, the company must figure out the best amounts of basic drugs, procured
from both the EU and the US, to mix into these two drug varieties. It must navigate
various limitations including stock levels, market demand, shipping concerns, and the
drugs' quality standards. Additionally, Apotheeker Pharmaceuticals has to determine
the drugs' D-metrics and P-metrics.
3.1 Assigning The Decision Variables :
Let x1 and x2 represent the quantities of Chemo-1 and Chemo-2 vials, respectively,
using the European Constituent.
Similarly x3 and x4 represent the quantities of Chemo-1 and Chemo-2 vials,
respectively, using the US Constituent.
𝟏 𝟐 𝟑 𝟒
+
3.2 Objective Function :
The goal is to increase the monthly earnings to their highest level, calculated as the
difference between the income generated from sales and the expenses associated with
producing the drugs and acquiring their components. This income is determined by
multiplying the selling price by the quantity sold for each drug, while the costs are
figured by multiplying the per-unit price of each ingredient (EU and US constituents)
by the amount used.
𝑴𝒂𝒙𝒊𝒎𝒊𝒛𝒆 𝒁
= (𝟏𝟐𝟎𝟎 ∗ (𝒙𝟏 + 𝒙𝟑) ) + (𝟏𝟒𝟎𝟎 ∗ (𝒙𝟐 + 𝒙𝟒))
− ( 𝟖𝟎𝟎 ∗ (𝒙𝟏 + 𝒙𝟐) ) + (𝟏𝟓𝟎𝟎 ∗ (𝒙𝟑 + 𝒙𝟒) )
1 2 3 4
+
3.3 Constraints :
3.3.1 Maximum Demand Constraints :
𝟏 𝟑
𝟐 𝟒
1 2 3 4
+
14
3.3.2 Minimum Delivery Constraints :
𝒙𝟏 + 𝒙𝟑 ≥ 𝟏𝟎𝟎𝟎𝟎𝟎
𝒙𝟐 + 𝒙𝟒 ≥ 𝟏𝟎𝟎𝟎𝟎
𝑥1, 𝑥2, 𝑥3, 𝑥4 ∈ ℤ+
3.3.3 Inventory Constraints :
𝒙𝟏 + 𝒙𝟐 ≤ 𝟖𝟎𝟎𝟎𝟎
𝒙𝟑 + 𝒙𝟒 ≤ 𝟏𝟐𝟎𝟎𝟎𝟎
𝑥1, 𝑥2, 𝑥3, 𝑥4 ∈ ℤ+
3.3.4 Maximum D-Metric Constraints :
Chemo -1
25𝑥1
𝑥1 + 𝑥3
+
15𝑥3
𝑥1 + 𝑥3
≤ 23
25𝑥1 + 15𝑥3
𝑥1 + 𝑥3
≤ 23
𝟐𝟓𝒙𝟏 + 𝟏𝟓𝒙𝟑 ≤ 𝟐𝟑 ∗ (𝒙𝟏 + 𝒙𝟑)
Chemo -2
25𝑥2
𝑥2 + 𝑥4
+
15𝑥4
𝑥2 + 𝑥4
≤ 23
25𝑥2 + 15𝑥4
𝑥2 + 𝑥4
≤ 23
𝟐𝟓𝒙𝟐 + 𝟏𝟓𝒙𝟒 ≤ 𝟐𝟑* (𝒙𝟐 + 𝒙𝟒)
15
3.3.5 Minimum P-Metric Constraints :
Chemo -1
87𝑥1
𝑥1 + 𝑥3
+
98𝑥3
𝑥1 + 𝑥3
≥ 88
87𝑥1 + 98𝑥3
𝑥1 + 𝑥3
≥ 88
𝟖𝟕𝒙𝟏 + 𝟗𝟖𝒙𝟑 ≥ 𝟖𝟖 ∗ (𝒙𝟏 + 𝒙𝟑)
Chemo -2
87𝑥2
𝑥2 + 𝑥4
+
98𝑥4
𝑥2 + 𝑥4
≥ 93
87𝑥2 + 98𝑥4
𝑥2 + 𝑥4
≥ 93
𝟖𝟕𝒙𝟐 + 𝟗𝟖𝒙𝟒 ≥ 𝟗𝟑 ∗ (𝒙𝟐 + 𝒙𝟒)
3.4 Final Model :
𝑴𝒂𝒙𝒊𝒎𝒊𝒛𝒆 𝒁
= (𝟏𝟐𝟎𝟎 ∗ (𝒙𝟏 + 𝒙𝟑) ) + (𝟏𝟒𝟎𝟎 ∗ (𝒙𝟐 + 𝒙𝟒))
− ( 𝟖𝟎𝟎 ∗ (𝒙𝟏 + 𝒙𝟐) ) + (𝟏𝟓𝟎𝟎 ∗ (𝒙𝟑 + 𝒙𝟒) )
1 2 3 4
+
16
Subject to following Constraints :
Maximum Demand Constraints :
𝑥1 + 𝑥3 ≤ 200000
𝑥2 + 𝑥4 ≤ 40000
Minimum Delivery Constraints :
𝑥1 + 𝑥3 ≥ 100000
𝑥2 + 𝑥4 ≥ 10000
Inventory Constraints :
𝑥1 + 𝑥2 ≤ 80000
𝑥3 + 𝑥4 ≤ 120000
Maximum D-Metric Constraints :
25𝑥1 + 15𝑥3 ≤ 23 ∗ (𝑥1 + 𝑥3)
25𝑥2 + 15𝑥4 ≤ 23* (𝑥2 + 𝑥4)
Minimum P-Metric Constraints :
87𝑥1 + 98𝑥3 ≥ 88 ∗ (𝑥1 + 𝑥3)
87𝑥2 + 98𝑥4 ≥ 93 ∗ (𝑥2 + 𝑥4)
𝟏 𝟐 𝟑 𝟒
+
17
3.5 Solving the Model :
3.5 .1 Implementation of Mathematical Model in R :
18
3.5 .2 R Output Solution :
19
3.6 Managerial Statement :
To achieve a maximum monthly profit of € 25 million, Apotheeker needs to blend
75,455 vials of the EU constituent with 24,545 vials of the US constituent to create
100,000 vials of Chemo-1. Additionally, for the production of 10,000 vials of Chemo-
2, 4,545 vials of the EU constituent must be mixed with 5,455 vials of the US
constituent.
Constituents Chemo-1 Chemo-2
EU 75455 4545
US 24545 5455
Total 100000 10000
The D-metrics of Chemo - 1 and Chemo - 2 are 22.54 and 20, respectively
The P-metrics of Chemo - 1 and Chemo - 2 are 89.7 and 93 , respectively
Metric Chemo-1 Chemo-2
D- Metric 22.54 20
P- Metric 89.7 93
