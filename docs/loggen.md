# Log Generator
![Screenshot](img/loggenerator.png)

!!! Danger

    **This is for testing only, and need to be enable in settings by an administrator. Do not test it on a live production machine. Right now it's not possible to use external scheduler with this log generation. It has not been built in yet. Don't forget to setup cron job for log generation, more info in installation section.**

Log generation is where you generate scheduled logs. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/90IsBbZszSk?si=poE19wTtbwbbiaX9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

It uses the same procedure as the original log generator, but it can handle multiple logs to be added at the same time for log generation.

## Wildcards
System support filepath wildcards for date and time. And the following is supported:

| Wildcard    | Info |
| -------- | ------- |
| %m  | Month, zero padded (01 - 12)    |
| %d | Day of the month, zero padded (01 - 31)     |
| %Y    | Four digit year    |
| %y    | Two digit year    |
| %G    | Four digit year, as per ISO 8601    |
| %a    | Abbreviated weekday name --e.g. 'mon', 'tue'    |
| %A    | Full weekday name --e.g. 'monday', 'tuesday'    |
| %b    | Abbreviated month name --e.g. 'jan', 'feb'    |
| %h    | Abbreviated month name --e.g. 'jan', 'feb'    |
| %B    | Full month name --e.g. 'january', 'february'    |
| %D    | Date (mm-dd-yy)    |
| %e    | Day of the month, space padded ( 1 - 12)    |
| %F    | Date (yyyy-mm-dd)    |
| %H    | Hour, 24 hour, zero padded (00 - 23)    |
| %k    | Hour, 24 hour, space padded ( 0 - 23)    |
| %i    | Hour, 12 hour, space padded ( 0 - 12)    |
| %J    | Hour, 12 hour, unpadded (1 - 12)    |
| %I    | Hour, 12 hour, zero padded (00 - 12)    |
| %j    | Day of year (0 - 365)    |
| %l    | Month, unpadded (1-12)    |
| %M    | Minute, zero padded (00 - 59)    |
| %P    | AM/PM string    |
| %S    | Seconds, zero padded (00 - 60)    |
| %u    | Day of the week, numeric, 1=Monday, 7=Sunday    |
| %w    | Day of the week, numeric, 0=Monday, 6=Sunday    |
| %V    | Week number, as per ISO 8601    |
| %W    | Week number, as per ISO 8601    |

## Generate Logs
![Screenshot](img/generatelog.png)
Press the generate log button to open the window where you select log service and date for log generation. When you have select correct service and date, press the Generate log button to add it to generate list.

!!! Info

    **It's possible to select multiple dates to add for log generation**

If a log exist, it will warn you about it. And if you agree, it will remove the old log when the new one is generated.

## Automatic Log Generator
![Screenshot](img/loggensettings.png)
There are an automatic log generator, that can generate your logs for you. It will work in the background, and generate the logs.
Press the Settings button to open up the settings window.

Here you can enable automatic generator. You can generate up to 7 days. Just enter how many days you will generate.

Under services select the services you would like to generate logs for.

It will start to generate two days before. And all information are stored on the server, and not in Rivendell Radio Automation.

!!! Info

    **If your last log will run on 2025-10-20, the log generator will generate new logs on 2025-10-19.**
    
    **Before you enable make shure you have logs generated in the past.**


## Logs List
The log list holds all logs that going to be generated or has been generated.

!!! Info

    **If the log has a purge date set to auto remove, the log generator data will also be removed on that day.**

In the status section, you can see if the log is ready for log generation, is generating or done.

The green button on each log is for regenerate a log. If you click on that it will remove the old one and generate a new one.

## Log generation Log
![Screenshot](img/loglog.png)
The log generation logs is located if you press the yellow information button. It store the information on the web server only and you can find information on the log generation.

!!! Info

    **During the development there will be more log information than needed. Some information will be removed when a more stable version is ready.**

## Remove log generation data
You can remove the log generation data by pressing the red X button. No real logs will be removed, only log generation data, and they are stored on the web server only.

You can also remove multiple log generation data if you check the check boxes and press the delete selected button that will pop up.