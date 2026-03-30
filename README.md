# Market Basket ARM Comparative Analysis

This repository presents a technical comparison of three association rule mining (ARM) algorithms—Apriori, ECLAT, and FP-Growth—using a real transactional groceries dataset.


## Repository Description
A comparative market basket analysis project that applies Apriori, ECLAT, and FP-Growth on grocery transactions to extract frequent itemsets, generate association rules, and benchmark algorithmic performance in terms of execution time and memory usage.

## Objective
I implement and compare Apriori, ECLAT, and FP-Growth to identify co-occurring items in retail transactions and evaluate which algorithm is more practical for scalable association rule mining.

## Project Structure
- `market_basket_arm_comparative_analysis.ipynb` — Main notebook with preprocessing, algorithm execution, visualization, and benchmarking.
- `dataset/Groceries_dataset.csv` — Transaction-level groceries dataset.
- `README.md` — Documentation including theory and implementation details.

## Technical Theory

### 1) Association Rule Mining
Association rule mining discovers relationships among items bought together in transaction data. Rules are represented as:

$$X \Rightarrow Y$$

where $X$ (antecedent) and $Y$ (consequent) are itemsets.

Common quality metrics:

- **Support**
$$support(X) = \frac{\text{transactions containing } X}{\text{total transactions}}$$

- **Confidence**
$$confidence(X \Rightarrow Y) = \frac{support(X \cup Y)}{support(X)}$$

- **Lift**
$$lift(X \Rightarrow Y) = \frac{confidence(X \Rightarrow Y)}{support(Y)}$$

Interpretation: lift greater than 1 indicates positive co-occurrence strength between itemsets beyond random chance.

### 2) Apriori
Apriori uses a level-wise candidate generation strategy and the anti-monotonic property:
- If an itemset is infrequent, all its supersets are infrequent.

Pros:
- Simple and interpretable.

Limitations:
- Expensive candidate generation and multiple database scans for large datasets.

### 3) ECLAT
ECLAT uses a vertical data format (transaction ID lists) and computes frequent itemsets via set intersections.

Pros:
- Efficient intersections for moderate-size data.

Limitations:
- Can become memory/computation heavy on large or dense datasets.

### 4) FP-Growth
FP-Growth compresses transactions into an FP-Tree and mines frequent patterns without explicit candidate generation.

Pros:
- Typically faster and more memory efficient than Apriori for large datasets.

Limitations:
- Tree construction complexity and implementation overhead.

## Technical Implementation Details

### Data Preparation
1. Load `Groceries_dataset.csv`.
2. Group by `Member_number` and `Date` to build transaction baskets.
3. Convert baskets into encoded boolean matrix using `TransactionEncoder` for Apriori and FP-Growth.
4. Convert transactions into tabular form for ECLAT implementation.

### Algorithm Configuration
- **ECLAT**: `min_support = 0.01`, combinations limited to size 1–2 for controlled runtime.
- **Apriori**: `min_support = 7 / len(transactions)` and rule extraction using lift.
- **FP-Growth**: similar support threshold with confidence-based rule generation.

### Benchmarking
A benchmark wrapper measures:
- Execution time (seconds)
- Peak memory usage (MB)

using `time` and `memory_profiler` for comparative analysis across algorithms.

### Visualization
The notebook includes:
- Frequent itemset and rule outputs
- FP-tree-style structure visualization using `networkx` and `matplotlib`
- Tabular performance comparison across Apriori, ECLAT, and FP-Growth

## Environment and Dependencies
- Python 3.x
- pandas
- mlxtend
- pyECLAT
- memory-profiler
- matplotlib
- networkx

## Expected Outcome
- Frequent itemsets and high-quality association rules from grocery transactions.
- A technical comparison showing computational trade-offs among Apriori, ECLAT, and FP-Growth.
- Practical guidance on selecting ARM algorithms depending on data scale and resource constraints.

## Author
**Manolina Das**  

