
<!-- README.md is generated from README.Rmd. Please edit that file -->

# SwanScorer

<!-- badges: start -->

<!-- badges: end -->

The Strengths and Weaknesses of ADHD Symptoms and Normal Behavior Rating
Scale (SWAN) is a validated instrument for measuring
attention-deficit/hyperactivity disorder (ADHD) traits ([Burton et al.,
2018](https://doi.org/10.1101/248484)). The SwanScorer package provides
an easy way to automatically score your SWAN tests.

## Notes about the data

- The `get_swan_tscores()` function will ask you to upload a spreadsheet
  with your SWAN data. If you have any additional columns beyond the
  necessary columns described below, i.e. an identifier, those columns
  will remain untouched in the output. For example, if your input file
  has two additional columns, an identifier and parent’s education,
  those columns will pass through to the output file.

- Scores are automatically reversed before calculating the t-score so
  that a higher score is associated with higher ADHD trait.

- The test is split into two subdomains. Questions 1-9 measure
  inattentiveness. Questions 10-18 measure hyperactivity and
  impulsivity. If more than one question is missing from a subdomain the
  test will not be scored.

- T-scores will be generated based on gendered and non-gendered norms.
  Please feel free to include children who are trans or non-binary in
  your dataset and leave the codes for their gender as appropriate for
  the individuals in your study. Non-gendered t-scores will be generated
  for all individuals. To generate gendered t-scores for binary gendered
  participants be sure to code gender as 1 = boy and 2 = girl. Any
  gender not coded as 1 or 2 will not receive a gendered t-score. Any
  gender not coded as 1 or 2 will not receive a gendered t-score.

## Instructions

### Formatting Your Data

Our first step is to prepare your raw SWAN data.

1.  Prepare a spreadsheet, preferably a .csv file, with a row for each
    of the tests you’d like to score.

2.  Be sure the following columns are present in the spreadsheet and
    rename the columns to match the reference guide below. All of the
    following columns are necessary for the model. If age or
    p_respondent are missing from a row, the model will not return a
    t-score for that row.

    <div>

    | Column Name | Additional Information | Example |
    |----|----|----|
    | age | The child’s age | 5 - 18 <br><br> Note: Age in a numeric form, i.e. with decimals, will provide a more accurate t-score compared to an integer-based age |
    | gender | The child’s gender. Please feel free to include children who are trans or non-binary in your dataset and leave the codes for their gender as appropriate for the individuals in your study. Non-gendered t-scores will be generated for all individuals. To generate gendered t-scores for binary gendered participants be sure to code gender as 1 = boy and 2 = girl | 1 = Boy, 2 = Girl <br><br> Note: Any gender not coded as 1 or 2 will not receive a gendered t-score. |
    | p_respondent | Whether the survey was filled out by the parent or the child | 1 = Parent Respondent, 0 = Child / Youth Self-Respondent |
    | swan1 | 1\. Give close attention to detail and avoid careless mistakes | -3 (Far Below) to 3 (Far Above) |
    | swan2 | 2\. Sustain attention on tasks and play activities | -3 (Far Below) to 3 (Far Above) |
    | swan3 | 3\. Listen when spoken to directly | -3 (Far Below) to 3 (Far Above) |
    | swan4 | 4\. Follow through on instructions and finish schoolwork / chores | -3 (Far Below) to 3 (Far Above) |
    | swan5 | 5\. Organize tasks and activities | -3 (Far Below) to 3 (Far Above) |
    | swan6 | 6\. Engage in tasks that require sustained mental effort | -3 (Far Below) to 3 (Far Above) |
    | swan7 | 7\. Keep track of things necessary for activities | -3 (Far Below) to 3 (Far Above) |
    | swan8 | 8\. Ignore extraneous stimuli (able to ignore background noise/distractions) | -3 (Far Below) to 3 (Far Above) |
    | swan9 | 9\. Remember daily activities | -3 (Far Below) to 3 (Far Above) |
    | swan10 | 10\. Sit still (control movements of hands / feet or control squirming) | -3 (Far Below) to 3 (Far Above) |
    | swan11 | 11\. Stay seated (when required by class rules / social conventions) | -3 (Far Below) to 3 (Far Above) |
    | swan12 | 12\. Modulate motor activity (inhibit inappropriate running / climbing) | -3 (Far Below) to 3 (Far Above) |
    | swan13 | 13\. Play quietly (keep noise level reasonable) | -3 (Far Below) to 3 (Far Above) |
    | swan14 | 14\. Settle down and rest (control constant activity) | -3 (Far Below) to 3 (Far Above) |
    | swan15 | 15\. Modulate verbal activity (control excess talking) | -3 (Far Below) to 3 (Far Above) |
    | swan16 | 16\. Reflect on questions (control blurting out answers) | -3 (Far Below) to 3 (Far Above) |
    | swan17 | 17\. Await turn (stand in line and take turns) | -3 (Far Below) to 3 (Far Above) |
    | swan18 | 18\. Enter into conversations and games (control interrupting / intruding) | -3 (Far Below) to 3 (Far Above) |

    </div>

### Installation

You can install the development version of SwanScorer from
[GitHub](https://github.com/Schachar-Crosbie-Lab/SwanScorer) using the
code below.

``` r
# If the devtools package isn't installed already, do so first. 
install.packages("devtools")

devtools::install_github("Schachar-Crosbie-Lab/SwanScorer")
```

### Generate Scores

Use the code below to generate your t-scores. First, you will be
prompted to select your file. Second, we will check that your data are
formatted properly. Third, t-scores for the full test as well as the two
subdomains (inattentive and hyperactive) will be generated. Fourth, a
csv file with the t-scores will be saved to your working directory

If you receive an error, please correct the issue in your file, save
your file, then run the `get_swan_tscores()` function again.

``` r
library(SwanScorer)

# The get_swan_tscores checks that your data are formatted correctly and generates the t-scores
swan_tscores <- get_swan_tscores()
```

### Additional options

You have the option to specify…

1.  the file path of the input file

2.  where to export the csv file with t-scores

3.  not to export the csv file

``` r
library(SwanScorer)

# Example of how to specify the input file
swan_tscores <- get_swan_tscores(file = here("test_scores.csv"))

# Example of how to specify an output folder
swan_tscores <- get_swan_tscores(output_folder = file.path("C:","Users",..."yourpath"))

# Example of how to not export a csv file
swan_tscores <- get_swan_tscores(output_folder = NULL)
```

## Understanding the Output

### Reversed SWAN Scores

- Columns `swan1` to `swan18` are reverse-scored and returned as
  `swan1_reversed` to `swan18` reversed respectively.

### Summary Values

| Column | Description |
|----|----|
| swan_tot | A summed score of the answered questions across the entire test |
| swan_miss | A count of missing values across the entire test |
| swan_pro | A prorated score by dividing swan_tot by the number of answered questions across the entire test |
| swan_ia_tot | A summed score of the answered questions across the inattentive subdomain |
| swan_ia_miss | A count of missing values across the inattentive subdomain |
| swan_ia_pro | A prorated score by dividing swan_tot by the number of answered questions across the inattentive subdomain |
| swan_hi_tot | A summed score of the answered questions across the hyperactive subdomain |
| swan_hi_miss | A count of missing values across the hyperactive subdomain |
| swan_hi_pro | A prorated score by dividing swan_tot by the number of answered questions across the hyperactive subdomain |

### T-scores for generic model

| Column | Description |
|----|----|
| swan_tot_gender_tscores | A t-score across the entire SWAN test that adjusts for age, respondent, and gender |
| swan_tot_tscores | A t-score across the entire SWAN test that adjusts for age and respondent |
| swan_ia_gender_tscores | A t-score of the inattentive subdomain (questions 1-9) that adjusts for age, respondent, and gender |
| swan_ia_tscores | A t-score of the inattentive subdomain (questions 1-9) that adjusts for age and respondent |
| swan_hi_gender_tscores | A t-score of the hyperactive subdomain (questions 10-18) that adjusts for age, respondent, and gender |
| swan_hi_tscores | A t-score of the hyperactive subdomain (questions 10-18) that adjusts for age and respondent |
