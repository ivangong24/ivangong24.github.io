---
title: Exam Grading for PDF
author: ivan
date: 2024-05-16 20:00:00 +0800
categories: [study]
tags: [exam, grading, pdf]
---

# Introduction

When you serve as a teaching assistant, you may need to grade exams. Usually, you can use Canvas or Gradescope to grade exams. However, if the exam is in-person, you may need to first scan all the exams into PDF files and then grade them. This article introduces how to grade exams for multiple PDF files, including how to extract the specific pages for your own part so that you are blind to the student's name and other information and how to extract the text/notes you made during grading in R.

# Tools

- [pdftk](https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/): A command-line tool for manipulating PDF files.
- [Adobe Acrobat Reader DC](https://get.adobe.com/reader/): A PDF reader that allows you to add notes to the PDF file.
- [R](https://www.r-project.org/): A programming language for statistical computing.


# Extract Specific Pages

First, you need to extract the specific pages for your own part. For example, if you are responsible for grading Part B and Part D, you only want to see the related pages instead of the whole exam. You can use `pdftk` to do it.

Before doing that, make sure that you have installed `pdftk` on your computer. You can download it from the [official website](https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/). Then, you may want to add it to path so that you can use it in the command line.

Say you have a folder called `exams` that contains all the exams in PDF format, and the corresponding pages for Part B and Part D are 6, 9, 10. You can create a `.bat` file use the following command and put it in the `exams` folder. Then, run the `.bat` file to extract the specific pages for your own part.

```batch
@echo off
for %%I in (*.pdf) do (
    pdftk "%%I" cat 6 9-10 output "%%~nI-YOURINITIAL.pdf"
)
```

# Extract Text/Notes in graded PDF files

After grading, you may want to extract the text/notes you made during grading to see the total score you gave to each part. Let's say you have a score for each question and you summed them up to get the total score for part B and part D separately on page 6 and page 9 (i.e., the first and second page of the extracted pdf), respectively. You can use the following R code to extract the text/notes in the graded PDF files.

First, make sure you load the required packages.

```r
if (!require("pacman")) install.packages("pacman")

pacman::p_load(
  pdftools, # pdf text extraction
  here,     # project management
  tidyverse # data manipulation
)
```

Then, you can use the following code to extract the text/notes in the graded PDF files.

```r
# get the full path of the pdf files
pdf_names <- list.dirs(here(), recursive = TRUE) %>% 
  list.files("\\.pdf$", full.names = TRUE, recursive = TRUE)

# extract text from pdf files
text_data <- pdf_names %>% 
  map(pdf_text, .progress = TRUE)

# clean the text data by combining each line and separating by ";" 
grade_data <- text_data %>% 
  map(function(data){
    seq_along(data) %>% 
      map(function(i){
        data[[i]] %>% 
          str_split("\n") %>%
          map_chr(~ .x %>% str_trim() %>% str_c(collapse = " ")) %>% 
          str_c(collapse = "; ")
      })
  })

# create a tibble to store the cleaned data
grade_data_clean <- tibble(
  document = basename(pdf_names), 
  part_b   = grade_data %>% map_chr(~ .x[[1]]),
  part_d   = grade_data %>% map_chr(~ .x[[2]])
)

```

Now, you can export the `grade_data_clean` to an Excel file or other formats to report the grading results. Cheers!
