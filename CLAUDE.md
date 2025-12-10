# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an R-based analysis project exploring fertility trends in the General Social Survey (GSS) data. The project investigates claims about progressive birth rates using survey methodology and statistical analysis.

**Research Question**: Does political ideology correlate with fertility rates when controlling for other factors like geography and socioeconomic status?

## Environment Setup

### R Environment Management

This project uses `renv` for reproducible package management:

```bash
# Install dependencies from lockfile
Rscript -e "renv::restore()"
```

The `.Rprofile` automatically activates the renv environment on startup.

### Required Packages

Key packages used throughout analyses:
- `gssr`: GSS data loader (pinned to specific version for census division data)
- `survey`: Complex survey design analysis
- `dplyr`: Data manipulation
- `ggplot2`: Visualization

## Working with Analyses

### Running R Markdown Documents

All analyses are R Markdown (`.Rmd`) files in `ideology_fertility/`:

```bash
# Render a specific analysis
Rscript -e "rmarkdown::render('ideology_fertility/overall_hetero_only.Rmd')"
```

In RStudio, use the "Knit" button or `Ctrl+Shift+K`.

### Analysis Files

The repository contains multiple analysis variations exploring different aspects:

- **overall_hetero_only.Rmd**: Analysis restricted to heterosexual respondents, examining fertility by political views
- **children_by_party_id.Rmd**: Uses party identification (Democrat/Independent/Republican) instead of ideological self-placement
- **pool_raw_surveys_rolling.Rmd**: Demonstrates proper survey pooling methodology
- **adds_homeownership.Rmd**: Extends analysis to control for region, community size, and homeownership
- **progressives_birth_rates.rmd**: Earlier iteration of the analysis

## Survey Analysis Architecture

### GSS Data Structure

The GSS uses complex survey design that requires special handling:

**Survey Design Variables**:
- `vpsu`: Primary sampling unit (clustering)
- `vstrat`: Stratification variable
- `wtssps`: Post-stratification weight (recommended for 1972-2024)

**Key Variables**:
- `childs`: Number of children (outcome)
- `polviews`: Political ideology (1=Extremely liberal, 7=Extremely conservative)
- `partyid`: Party identification (0=Strong Democrat, 6=Strong Republican)
- `age`: Respondent age
- `year`: Survey year
- `region`: Census region/division
- `xnorcsiz`: Community size classification
- `dwelown`: Homeownership status
- `sexornt`: Sexual orientation (3=Heterosexual)

### Survey Methodology Pattern

All analyses follow this standard pattern:

1. **Load and Filter Data**:
   - Filter for complete cases on required variables
   - Apply age filter (typically `age >= 35` for completed fertility)
   - Filter for years with design variables (`year >= 1975`)
   - Create grouped categorical variables

2. **Create Survey Design Object**:
   ```r
   options(survey.lonely.psu = "adjust")
   gss_design <- svydesign(
     ids = ~vpsu,
     strata = ~vstrat,
     weights = ~wtssps,
     data = gss_subset,
     nest = TRUE
   )
   ```

3. **Survey Pooling** (when used):
   - Pool raw survey data from multiple years (typically 7 surveys centered)
   - Compute single weighted estimate on pooled sample
   - This is proper survey methodology vs. averaging estimates

4. **Compute Estimates**:
   ```r
   results <- svyby(
     formula = ~childs,
     by = ~polviews_grouped + year,
     design = gss_design,
     FUN = svymean,
     na.rm = TRUE
   )
   ```

5. **Visualization**: Time series plots with confidence intervals

### Important Survey Analysis Principles

- **Never ignore survey design**: Always use `svydesign()` with clustering, stratification, and weights
- **Pooling methodology**: Pool raw data before computing estimates, don't average estimates
- **Weight selection**: Use `wtssps` for cross-sectional analysis (1972-2024)
- **Lonely PSU handling**: Set `options(survey.lonely.psu = "adjust")` before creating design objects
- **Missing data**: Filter for complete cases on design variables before creating survey design object

## Common Workflow

### Adding a New Analysis

1. Copy an existing `.Rmd` file as template (e.g., `overall_hetero_only.Rmd`)
2. Modify the parameter section (age filter, year range, pooling window)
3. Add any new GSS variables to the `select()` statement
4. Ensure proper filtering for complete cases
5. Update grouping logic in `mutate()` calls
6. Modify `svyby()` calls to analyze new grouping variables
7. Update plot aesthetics and labels

### Debugging Survey Design Issues

Common issues:
- **"Stratum with only one PSU"**: Use `options(survey.lonely.psu = "adjust")`
- **Missing design variables**: Check that `year >= 1975` filter is applied
- **Zero variance**: May occur with very small subgroups; check sample sizes
- **Weight variable not found**: Ensure `wtssps` is included in `select()` and complete

## Data Sources

The `gssr` package loads GSS data. A specific version is pinned to access census division data:

```r
# Installation command (in ideology_fertility/ReadMe.md)
remotes::install_github("kjhealy/gssr@ed90704")
```

## Project Context

See [ReadMe.md](ReadMe.md) for research motivation and background. The `ideology_fertility/ReadMe.md` contains detailed notes on data sources, methodological decisions, and related research references.
