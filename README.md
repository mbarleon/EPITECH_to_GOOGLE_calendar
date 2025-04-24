# EPITECH_to_GOOGLE_calendar

Synchronize your Epitech calendar with Google!

# Features

  - [x] Synchronization of epitech calendar on google calendar
  - [x] Update modified events / Remove canceled events
  - [x] Display location and link of event and mails of teaching assistants in google event description
  - [x] Display only the selected slot for multi-slots events
  - [ ] Project timeline
  - [ ] Fetch events the events which you supervise (HUB acti for example)
  - [x] Fetch registered events from private epitech calendars
  - [ ] Support multi epitech accounts (great for AERs who have two epitech accounts and calendars)

# Example

This is my google calendar:
 - In green: registered events from my epitech calendar
 - In light pink: registered project timeline
 - In grey: events that I supervise (often HUB activities)
 - In red: registered events from my AER epitech calendar

![google calendar](.github/assets/google_calendar.png)

# Usage

### Fetch all next events

```
$ python3 main.py
```

### Fetch all events since date

```
$ python3 main.py YYYY-MM-DD
```

# Config

## Python3 - Requirements

```
$ sudo python3 -m pip install -r requirements.txt
```

## Config file

Create a `config.json` file (from `config-sample.json`) with the following content at root of the repo:

```json
[
    {
        "comment": "student / aer ...",
        "epitech_cookie": "...",
        "calendarID_events": "...@group.calendar.google.com",
        "calendarID_timeline": "...@group.calendar.google.com",
        "calendarID_teaching_team": "...@group.calendar.google.com",
        "calendarID_other_calendars": "...@group.calendar.google.com",
        "google_user_data_path": "C:\\Users\\...\\AppData\\Local\\Google\\Chrome\\User Data",
        "google_profile": "Default"
    }
]
```

 - `comment` is what you want, it doesn't matter, it's just useful not to get mixed up if you have multiple accounts
 - `epitech_cookie` is your user cookie, find it by going on the intra and going into dev console -> application -> cookies -> user
 - `calendarID_events` is the calendar in which you want to put all registered events
 - `calendarID_timeline` is the calendar in which you want to put projects timeline
 - `calendarID_teaching_team` is the calendar in which you want to put events which you supervise (HUB activities for example)
 - `calendarID_other_calendars` is the calendar in which you want to put events registered in your private epitech calendars
 - `google_user_data_path` is the path of your chrome user data folder
 - `google_profile` is the folder where your user profile is stored

The `calendarID_timeline`and `calendarID_teaching_team` are currently disabled because the intra does not let you do a lot of requests and they are less useful to me.

If you don't want some events you can delete line in `config.json` or set value to `null`.
If you want to put all events in only one calendarID you can by using the same calendarID.

### Multi epitech account or fiend account? So easy!

```json
[
    {
        "comment": "student",
        "epitech_cookie": "...",
        "calendarID_events": "...@group.calendar.google.com",
        "calendarID_timeline": "...@group.calendar.google.com",
        "calendarID_teaching_team": "...@group.calendar.google.com",
        "calendarID_other_calendars": "...@group.calendar.google.com"
    },
    {
        "comment": "aer",
        "epitech_cookie": "...",
        "calendarID_events": "...@group.calendar.google.com",
        "calendarID_timeline": "...@group.calendar.google.com",
        "calendarID_teaching_team": "...@group.calendar.google.com",
        "calendarID_other_calendars": "...@group.calendar.google.com"
    }
]
```

## How to get calendarID?

 - Create a calendar in google
 - Go in your new calendar's settings
 - Go in `Integrate Calendar` section
 - Copy `Calendar ID` (in general it looks like `...@group.calendar.google.com` or `...@gmail.com`)

## Google `credentials.json`

To connect your google account with this application, you also need to create an OAuth credentials file ([How generate credentials](Generate_credentials.md)). Then, rename the downloaded file to `credentials.json` and put it in the root of the repo.

# Automatization

To automatize the synchronization with yours epitech calendars, you can use a cron

For example, to run the program every half hour, you can copy this in your crontab (`crontab -e`):

```
*/30 * * * * cd /full/path/EPITECH_to_GOOGLE_calendar/; python3 main.py &>> log
```
