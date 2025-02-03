# Introduction to Health Analytics Group Project template
Outline for Introduction to Health Analytics student group project

## Setup Instructions
1. One person from the group should:
    - Fork this repository by following instructions [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo). Make sure you rename it!
    - Add the other members of your team to the repository by following the instructions [here](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository).

2. All members of the group should then:
    - Sign in to Github and Github Desktop
    - Clone the forked repository to your local computer and open in Github Desktop by following the instructions [here](https://docs.github.com/en/desktop/adding-and-cloning-repositories/cloning-a-repository-from-github-to-github-desktop).
    - Make a change to your local copy of the repo (e.g. add a test file), commit that change and then push to the master using the instructions [here](https://docs.github.com/en/desktop/making-changes-in-a-branch/committing-and-reviewing-changes-to-your-project-in-github-desktop). Ignore the information about branches - for now you can just work on the main branch.

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
