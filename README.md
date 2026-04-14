# cvs-minuteclinic-impact-on-retail-sales

## **Project Summary**

CVS Pharmacy has invested heavily in expanding its in-store MinuteClinic network. While the clinical benefits are well established, management is interested in whether clinics also increase front-end retail sales. In particular, they want to understand whether clinic visitors generate additional purchases while in the store.

The business objective is to estimate the causal impact of opening a MinuteClinic on monthly front-end retail sales and to assess whether this effect differs between urban and suburban stores.

## **DAG Analysis**

To structure the causal analysis, we construct a Directed Acyclic Graph (DAG) relating the key variables.

Treatment ($D_{it}$): MinuteClinic is open and operational at store $i$ in month $t$ (binary)

Outcome ($Y_{it}$): Monthly front-end retail sales at store $i$ in month $t$ (dollars)

Unobserved Store Quality ($\alpha_i$): Time-invariant store-level characteristics such as manager quality, neighborhood loyalty, and store layout, which affect both CVS's clinic siting decisions and baseline sales

Time Effects ($\gamma_t$): Platform-wide demand shocks, seasonality, and macro trends that affect all stores simultaneously

Urban Status ($Urban_i$): Whether the store is in an urban vs. suburban location, affecting both baseline sales levels and treatment effect magnitude

Store Size ($Size_i$): Physical store footprint (square feet), correlated with both sales capacity and clinic placement priority

The core identification challenge is selection bias: CVS does not open MinuteClinics randomly. Higher-performing, larger, or strategically-located stores may be prioritized for clinics, meaning a naive before/after comparison would overstate the effect. Our methods are designed to address this directly.

## **Methods Used**

We deploy three complementary causal inference strategies:

Synthetic Control (SC): Constructs a weighted combination of never-treated stores that best matches our focal store's pre-treatment sales trajectory. Any post-treatment divergence between the real store and its synthetic twin is the estimated treatment effect.

Synthetic Difference-in-Differences (SDiD): Extends SC by incorporating both unit-level and time-period weights in a DiD framework, producing a more efficient pooled estimate across all cohort 1 treated stores and control stores.

Heterogeneous Treatment Effects (HTE) - Causal Forest: Uses a machine-learning estimator (Random Forest applied to causal inference) to estimate individualized treatment effects at the store level, then tests whether urban stores systematically experience larger effects than suburban ones.

## **Summary of Results**

Across all three methods, we find consistent and statistically significant evidence that MinuteClinic openings increase monthly front-end retail sales. SC estimates a lift of approximately $4,600 per month for the focal urban store (Store 61). SDiD estimates an average treatment effect of approximately $3,731 per month across Cohort 1 stores. The Causal Forest confirms an ATE of $3,786/month (SE: $400). Contrary to our prior hypothesis, the HTE analysis does not find meaningful urban/suburban differentiation — estimated CATEs are nearly identical across store types ($3,749 for urban vs. $3,775 for suburban), a limitation we attribute to the store-level collapsed specification and limited treatment variation in the data.

## **Business Implications**

The consistent, positive, and significant findings provide CVS with a strong causal foundation for continued MinuteClinic investment. All three methods converge on a range of $3,700–$4,600/month in incremental front-end retail revenue per clinic, translating to approximately $44,800–$55,200 in annual incremental retail revenue per clinic. This should be incorporated into total clinic ROI modeling alongside clinical revenue streams.
