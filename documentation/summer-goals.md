# Summer Work To-Do List

## Big Ticket Items
- [ ] Create new floor plans and flowchart
- [ ] Clean up scripts and organize RPI file structure
- [ ] Real-time data viz on website - Learn JavaScript, HTML/CSS
- [ ] Feed Rebecca's data into a SQL database on cPanel
- [ ] Hook up RPis to new infrastructur - Dependent upon Eric's needs
- [ ] Make pressure, humidity sensor - Consult with Eric, John about implementation specifics

## Things to do now
- [x] Create new floor plans and flowchart
    - [x] Re-do flowchart using plantUML 
    - [ ] Re-do floorplans using iPad, then convert to SVG
        - [ ] Necessary for adding JS interactivity later
            - [ ] idea is to hover over meters, get real-time summary data, then click and get real-time graph

- [ ] Update 5's reading.txt and lost data
    - Make a python script that will update reading.txt and fill in the missing data
    - Consult with Eric about how to implement this, because Rebecca's programs depend on the reading.txt files and the csvs

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

