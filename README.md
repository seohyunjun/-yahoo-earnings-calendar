# Origin Repo [wenboyu2](https://pypi.org/user/wenboyu2/)

# Yahoo! Earnings Calendar Scraper
Scrapes Yahoo! Finance earnings calendar to get data for a specific date or a date range.

## Installation
### Pip
```sh
git clone https://github.com/seohyunjun/yahoo-earnings-calendar
```
### require (yfinanace, requests)
```
pip install -r requirements.txt
```

## Usage

### Get earnings date information on a specific date or in a date range
```python
import datetime
from yahoo_earnings_calendar import YahooEarningsCalendar

date_from = datetime.datetime.strptime(
    'Feb 2 2022  10:00AM', '%b %d %Y %I:%M%p')
date_to = datetime.datetime.strptime(
    'Feb 2 2022  1:00PM', '%b %d %Y %I:%M%p')
yec = YahooEarningsCalendar()
print(yec.earnings_on(date_from))
print(yec.earnings_between(date_from, date_to))
```

#### Data attributes
- companyshortname: Company Name
  - e.g., 20160606
- ticker: Ticker
  - e.g., AAPL
- startdatetime: Event Start Time
  - e.g., 2017-04-23T21:00:00.000-04:00
- startdatetimetype: Event Start Time Type
  - e.g., TAS (Time Not Supplied), AMC (After Market Close	)
- epsestimate: EPS Estimate
- epsactual: Reported EPS
- epssurprisepct: Surprise (%)
- gmtOffsetMilliSeconds: GMT Offset in MS

### Get the next earnings date of a specific symbol
```python
import datetime
from yahoo_earnings_calendar import YahooEarningsCalendar

yec = YahooEarningsCalendar()
# Returns the next earnings date of BOX in Unix timestamp
print(yec.get_next_earnings_date('box'))
# 1508716800
```

### Get all the available earnings data of a specific symbol
```python
from yahoo_earnings_calendar import YahooEarningsCalendar

yec = YahooEarningsCalendar()
    # Returns a list of all available earnings of BOX
print(yec.get_earnings_of('box'))
```

### Set delay between requests

By default, requests are delayed by 1.8 sec to avoid exceeding the 2000/hour rate limit. You can override the default delay by passing an argument to the `YahooEarningsCalendar` constructor.

```py
import datetime
from yahoo_earnings_calendar import YahooEarningsCalendar

my_custom_delay_s = 0.5

yec = YahooEarningsCalendar(my_custom_delay_s)
```
