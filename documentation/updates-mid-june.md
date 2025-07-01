# Program Updates for Mid-June

- **Author**: Luke Marren
- **Recent Updates**:
  - Date: 6-12-25
  - Maintainer(s): Luke Marren

## Table of Contents

- [Accomplishments](#accomplishments---week-of-6-9-25)
    - [Monday](#monday-6-9)
    - [Tuesday](#tuesday-6-10)
    - [Wednesday](#wednesday-6-11)
    - [Thursday](#thursday-6-12)
    - [Friday](#friday-6-13)
- [Goals for the Next Two Weeks](#goals-for-the-next-two-weeks)
    - [Week 1](#week-1-6-16)
    - [Week 2](#week-2-6-23)


## Accomplishments - Week of 6-9-25

### Monday (6-9)
- Created `email_greg.py` script on the `RPis` GitHub (and on the actual two main analysis Raspberry Pis - `John's/dev` and `Sloan's/loomis434`).
    - This sends Greg Labbe, "the helium guru," an email with a text file attachment displaying meter 1-29's `dailyTotalCubicFeet` for the previous day.
    - I set it to run every day at 7 am under `loomis434's` crontab (check out the cronjob via `crontab -e` on Sloan's Pi).

### Tuesday (6-10)
- Spent a lot of the day learning/troubleshooting how to set up local environments for editing the website locally (and pushing to the `medusa` GitHub repository).
- Came to the following conclusions:
    - We should use `Path` from the `pathlib` Python library for working with paths.
        - `Os.path` is old news (but still supported) as of Python 3.6 (we run on virtual environments with Python 3.10 on cPanel and 3.9 on the RPis) - pathlib is preferred.
    - Parsing windows paths (`\` as opposed to `/`) from `.env` files can be really tricky.
        - It would be easier to read in a `.json` file for paths specific to each of our local environments that point to the shared helium directory.
        - For secrets/private information such as API keys and other passwords that *need* to be kept private, we can use a `.env` file and read them in.
            - Either way, we should never commit configuration/environment files that are specific to our local development environment.

### Wednesday (6-11)
- Changed `27. A101 CLSL` to `27. CLSLA Basement` on all website .html, .js, and .py files (except for the total page graphs because those PNGs are made and stored on the RPis staticly)
    - **Note**: I did not change the values for meter 27 that are sent to our python scripts internally.
        - The names of our CSV files have not changed - our data integrity is paramount - the metadata our users *can* see doesn't matter much.
    - Upon changing this, I came across a **bug** in our `selectAnalysis.py` code and figured out which Python files we actually use and which ones we don't.
        - **selectAnalysis.py Bug**: I added `line 242` - `z = data["date"]` because without it, the file would run into a `ValueError` because `z` would be called in an if statement on `line 333`.
            - I have no idea how we didn't stumble on this bug earlier or why `Select |> select totals` was working previously.
            - Also, the code in `selectAnalysis.py`, especially from `line 240` down, is very hard to read; the logic is poor and the variable names are not helpful.
        - Python files being used
            - Our Python graphing scripts save a `.png` file to the `pngs/` folder in `public_html`, which our front-end javascript then pulls into the html.
                - To do this, we *must* have the following line after our shebang line: `print("Content-Type: text/html\n")`
                    - This addition is used in `diff.py` (used for the lab recovery page - `differences.html`) and `selectAnalysis.py` (used on `index.html`) on `line 3`.
                    - `monthly_totals.py`, which is used on `monthly.html` uses slightly different logic to pull its graph - and for some reason it doesn't need the `print("Content-Type: text/html\n")`
                    - None of `differenceSelectAnalysis.py`, `selectDifferences.py`, or `SelectTotals.py` are called by any of the JavaScript files (`differences.js`, `index.js`, `monthly.js`, and `totals.js`) in their `runPython()` functions, so they are not in use (and may never be)
                        - Double-check before deleting them.
        - Here's a quick table that shows what's in use by the website right now:
            - | Page Name | .html | .js | .py |
              | --------- | ----- | --- | --- |
              | Select | `index.html` | `index.js` | `selectAnalysis.py` |
              | Lab Recovery | `differences.html` | `differences.js` | `diff.py` |
              | Totals | `totals.html` | `totals.js` | *N/A* |
              | Monthly Totals | `monthly.html` | `monthly.js` | `monthly_totals.py` |
              | Documents | `documents.html` | *N/A* | *N/A* |
- Visited Dean Olson, director of the NMR labs operated by the chemistry department.
    - He gave me a full tour of his facilities (super fascinating) and a rundown of what he *needs* displayed on the webpage.
    - Dr. Olson needs 5 things:
        - [ ] For us to change the `Select |> meters` dropdown graph so that only data points on individual days are connected by lines and not on multi-day periods.
        - [ ] Add zeros to the graphs when there is no data logged
            - Have a separate indication for data loss/mistakes
        - [ ] A tabular/graphical visualization of flow rate updated in real-time
            - So adding a table column / graph that spits out the average rate of change of helium flow (i.e., second_quantity - first_quantity / second_time - first_time)
            - **Note**: never change the underlying csv data - this is to be computed on top of that.
        - [ ] A tabular/graphical visualization of the total reading in real-time
        - [ ] A tabular/graphical visualization of the % efficiency per month
            - Chemistry (`meter 27`) gets a big fill every month over a three-day span
                - Typically its from Monday-Wednesday (4th Monday of the month)
            - Dr. Olson needs us to take the amount of liquid helium his labs used during this fill period (check the invoice data) and compare it to the amount of helium we recovered starting from right before the start of the fill to right before the start of the next fill.

### Thursday (6-12)

- Wrote documentation (such as this file) for most of the day.
- Got local development working for the website by using a python server with the command `python -m http.server 8000 --cgi`

    - We can now edit the website locally with all the data and files we need available to us!
        - Just need good documentation for environment stuff (.env, venv/, config.json, pre-commit hooks, and requirements.txt)

### Friday (6-13)

## Goals for the Next Two Weeks

### Week 1 (6-16)

- Write some front-end JavaScript to

### Week 2 (6-23)
