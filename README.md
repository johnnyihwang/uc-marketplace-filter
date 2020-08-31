# UCMarketplaceFilter

Searches UofC Marketplace, and rings a notification if any new postings match given keywords.

Use the application to quickly snipe highly sought-after items like bikes, cheap electronics, etc.

## Requirements
* Python3
* Selenium, BeautifulSoup

The notification is implemented through PyQt5, so if your system does not support it there may be issues. In this case turn notifications off by providing the flag `-n` (see below).

## How to use
    > python main.py -h
    usage: main.py [-h] [-k [FILENAME]] [-c [FILENAME]] [-g [ID]] [-n] [-p [SECONDS]]

All arguments are optional.

* `-h` : Displays the help message.
* `-k FILENAME` : Provide filename for where the keywords are stored. Default is file `keywords`.
* `-c FILENAME` : Provide filename for credentials. If the argument is not given, you will enter your credentials through stdin. If argument is given but filename is not, default file used is `credentials.json`. The JSON file must have attributes `email` and `pass`. For obvious security reasons, keeping your information stored in an unencrypted file is not recommended.
* `-g ID` : Provide ID of the group. Useful when you want to test it out for other marketplaces. Defaults to ID of the UofC marketplace.
* `-n` : If given, the Qt notification will not be activated. Messages on the terminal will still appear when matching posts are found.
* `-p SECONDS` : Wait time before attempting to get new posts. Defaults to 270 seconds.



### Keyword File Template

Each line can be considered as a single "keyword". In other words, all characters in one line must be in the post/title in order for it to be considered as a match. Whitespaces are also considered. If you provide a whitespace in a line, the post will be considered as a match if there are any number of whitespaces in the specified position.

For example, if the post says `Selling bikes and    inner tubes`, the keyword file

    dinner
    sand
will not match. However,

    bike
    fish
    cards
will match (match on `bike`), and

    d inner
    fish
    cards
will also match (match on `d inner`).

The keywords are not case-sensitive; whether you provide keywords in lower case or upper case does not matter.

A general tip is to include as many related words as possible. For example, if you are looking for bikes, you should include "bike", "bicycle", etc.
