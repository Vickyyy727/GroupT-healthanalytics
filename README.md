# Introduction to Health Analytics Group Project template
Outline for Introduction to Health Analytics student group project

## Description of data
In this section you should describe what data you use for your project with enough detail that anyone could download it and run your analysis.
- **IPUMS series**: We use the IPUMS International Census Data, which provides standardized individual-level information from various national censuses. This dataset is well-suited for our analysis of health insurance coverage and education levels in Mexico.
- **Countries**: We use the IPUMS International Census Data, which provides standardized individual-level information from various national censuses. This dataset is well-suited for our analysis of health insurance coverage and education levels in Mexico.
- **Years**: We include data from the 2010 and 2015 Mexican census. These years were selected to provide a comparative analysis of health insurance coverage and education levels before and after certain policy changes in the country.
- **How to access the data**: The data can be accessed from IPUMS International at the following link:
https://international.ipums.org/international/

To obtain the data, follow these steps:
1.	Create an IPUMS account (if you do not already have one).
 
2.	Request access to the Mexican census data for the years 2010 and 2015.
 
3.	Select the relevant variables, which include:

        •	Health Insurance Coverage (HLTHCOV) – Binary variable (1 = insured, 0 = not insured) 
	
        •	Education Level (EDUCMX) – Level of education completed
	
        •	Income (INCEARN) – Proxy for economic status
	
        •	Age (AGE) – Continuous variable
	
        •	Sex (SEX) – Binary gender variable
	
        •	Urban/Rural Residence (URBAN) – Categorical variable for heterogeneity analysis
	
 4.	Download the dataset in a compatible format.

## Description of how to run the code
Here you should explain how someone could replicate the analysis in your report. If there are several code files, explain what each of them does.

How to reproduce this analysis:
The aim of this study is to explore ‘the impact of education level on health insurance coverage in Mexico’, based on empirical analyses of IPUMS International Census data (2010 and 2015). Our central question of interest is whether educational attainment affects the likelihood of an individual's access to health insurance, and whether this effect varies across ‘urban and rural areas’. To this end, we construct a series of Logistic regression models, controlling for individuals' income, age, gender, and other factors, to analyse the relationship between education level and health insurance coverage. This document describes in detail how to reproduce this study, including data processing, variable transformation, regression modelling, and results visualisation.

Data Import and Processing：
The first step in the analysis is the loading and initial cleaning of the data. We use IPUMS International Census Data, a dataset that contains detailed information at the individual level and is able to support our empirical analyses. After the data is properly loaded, we extract the core variables needed for the study, including the dependent variable Health Insurance Coverage (HLTHCOV), the core independent variable Educational Attainment (EDUCMX), and a set of control variables such as Income (INCEARN), Age (AGE), Sex (SEX), and Rural-Urban Attributes (URBAN). As the raw data may contain missing values, we processed them using na.omit() to minimise the impact of missing data on the regression analysis. In addition, to ensure comparability of the data, we harmonise the definitions of variables across years to ensure that data from 2010 and 2015 can be used in an integrated manner. The treatment of variables is also critical. For example, health insurance coverage is a dichotomous variable (1 = insured, 0 = uninsured), and we transformed the raw data if it was not coded as such. Similarly, education level, which may be stored in a different categorical manner, is normalised to a numeric variable for use in regression models. Additionally, there are often extreme values in the income data, so we log-transform the income variable (log(INCEARN + 1)) to reduce the effect of outliers and improve the robustness of the regression model.

Model construction and regression analysis：
After completing data cleaning and variable processing, we enter the regression modelling stage. This study adopts a Logistic regression model, the dependent variable is a binary variable (whether or not to have health insurance), the core independent variable is the level of education, while controlling for income, age, gender, and urban/rural attributes, and the specific regression includes the following regression equations:
```
   model1 <- glm(HLTHCOV ~ EDUCMX, data = df, family = binomial)
   model_with_income <- glm(HLTHCOV ~ EDUCMX + log_INCEARN + SEX + AGE + URBAN, 
                             data = df, family = binomial)
   model_without_income <- glm(HLTHCOV ~ EDUCMX + SEX + AGE + URBAN, 
                            data = df, family = binomial)
   urban_model <- glm(HLTHCOV ~ EDUCMX + log_INCEARN + SEX + AGE, 
                   data = df %>% filter(URBAN == "Urban"), 
                   family = binomial)
   rural_model <- glm(HLTHCOV ~ EDUCMX + log_INCEARN + SEX + AGE, 
                   data = df %>% filter(URBAN == "Rural"), 
                   family = binomial)
   interaction_model <- bigglm(HLTHCOV ~ EDUCMX * URBAN + log_INCEARN + SEX + AGE, data = df, family = binomial())
```
In summary, first, we conduct an overall regression analysis to examine the effect of education level on health insurance coverage. Then, in order to explore the urban-rural differences, we further divided the regression into urban-rural regressions, i.e., we built regression models for urban and rural residents separately, in order to examine whether there is a significant difference in the impact of education level on health insurance coverage in different regions (in this process, we did Mediation Analysis and Heterogeneity Analysis, and conducted coefficient test).

Results Visualisation and Interpretation:
After the regression analysis is complete, we use summary(model) to check the regression results and use ggplot2 to visualise the results. For example, we can plot the heat map of the dataset coverage_summary to visualise the effect of different variables on health insurance coverage. In addition, we generate fitted curves for education level and health insurance coverage to see the relationship between the two. In particular, we plot the regression prediction curves for urban and rural areas to illustrate the urban-rural differences. The results show that education level has a significant positive effect on health insurance coverage, i.e., the higher the education level, the higher the probability that an individual has health insurance. However, this relationship differs significantly between urban and rural areas, with the effect being more pronounced in urban areas, whereas in rural areas the effect of income on health insurance coverage may be more significant. We speculate that this phenomenon may be related to the fact that insurance and social security systems are less developed in rural areas, whereas in urban areas the level of education is more likely to increase the health awareness of individuals and thus promote insurance coverage.

How to replicate the analysis:
If you wish to reproduce our study, please follow the steps below:

	1. Install the R dependencies
	2. Run the R Markdown file
             ##Open the Mexico.Rmd file and click the Knit button to run all the code and generate the full analysis.
	3. Examine the regression results
             ##Look at the summary(model) output in the Console to ensure that the regression coefficients and statistical significance are as expected. Also, check that the graphs generated by ggplot2 clearly show the effect of education level on health insurance coverage.

