# Summer Work To-Do List

- **Author**: Luke Marren
- **Recent Updates**:
  - Date: 6-12-25
  - Maintainer(s): Luke Marren

## Future Items
- [ ] Real-time data viz on website - Learn JavaScript, HTML/CSS
    - [ ] Add user authentication to website so specific users see specifc things
- [ ] Feed Rebecca's data into a SQL database on cPanel
- [ ] Hook up RPis to new infrastructure - Dependent upon Eric's needs
- [ ] Make pressure, humidity sensor - Consult with Eric, John about implementation specifics
- [ ] Make cross-platform app with user authentication

## Things to do now
- [x] Create new floor plans and flowchart
    - [x] Re-do flowchart using plantUML
        - [ ] Continue working on flowchart
            - Need to represent helium pipe line distances
            - Need to represent buildings (color code)
                - [ ] Use IPs.json???
    - [ ] Re-do floorplans using iPad, then convert to SVG
        - [ ] Necessary for adding JS interactivity later
            - [ ] idea is to hover over meters, get real-time summary data, then click and get real-time graph

- [ ] Update 5's reading.txt and lost data
    - [ ] Update 7 from 27
    - Make a python script that will update reading.txt and fill in the missing data

- [ ] Clean up scripts and organize RPI file structure
    - Format, comment, and add type hints and docstrings to python files
    - Reorganize RPI file structure - but be careful about this (make sure dev and loomis are on the same page)
        - folder for python scripts
        - folder for helium (stays the same)
        - folder for shell scripts
        - folder for logging errors from cron jobs
        - misc folder

- [ ] Create RPi health logging script
    - Log data as a CSV file on all sorts of health metrics

- [ ] Create RPi health analysis/alert script(s)

- [ ] Finish setting up RPi dev workflow
    - [ ] Make sure crontabs are the same throughout and are implemented as such
        - [ ] Use sudo to do this

- [ ] Set up website dev workflow
    - [x] Figure out how to locally (cross-platform) connect to shared directory
        - [ ] Write documentation on how to do so
    - [ ] Use .env, pre-hook-commits with python scipt to change file paths

- [ ] Document technologies
    - [x] How to use git
    - [x] How to navigate the GitHub
    - [ ] How to use the Bash Shell
    - [ ] How to program properly in Python
