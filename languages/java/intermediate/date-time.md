# Date and Time

- Use different libraries for differnt needs
  - `LocalDate` for just the date
  - `LocalTime` for just the time
  - `LocalDateTime` for both time and date
  - `ZoneDateTime` for time, date and time zone


## LocalDate

Examples:

The date to day is 13 May 2018

NOTE the return  values is just the toString() representation of LocalDate.

- Getting current date, in format YYYY-MM-DD
```java
LocalDate dateNow = LocalDate.now();
//return 2018-05-13
```

Can do some maths with the date
```java
dateNow.plusDays(3);
// return 2018-05-16

dateNow.minus(5, ChronoUnit.MONTHS);
// returns 2017-12-13
```
  - There are lots of methods to use

Can do some comparisions
```java
boolean equal = dateNow.isEqual(dateNow);
// returns true

dateNow.isBefore(dateNow.minusDays(1));
// reutrns false
```

Formatting the date
```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("d/MM/uuuu");
String formattedDate = dateNow.format(formatter);
//returns 13/05/2018
```

Parsing string date
```java
LocalDate parseDate = LocalDate.parse("2016-08-16");

LocalDate parsedDateFormatted = LocalDate.parse("16-Aug-2016", DateTimeFormatter.ofPattern("d-MMM-yyyy"));

LocalDate parsedDateWordFormatted = LocalDate.parse("Tue, Aug 16 2016", DateTimeFormatter.ofPattern("E, MMM d yyyy"));
```
 - Note the pattern of formatter matches the string representation of the date, and thus can turn into LocalDate format
 - list of patterns
   - https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html

Creating Date
```java
LocalDate someDate = LocalDate.of(2015, Month.JANUARY, 20);
//returns 2015-01-20

LocalDate someOtherDate = LocalDate.of(2016, 11, 19);
// return 2016-11-19
```

Get parts of the date
```java
dateNow.get(ChronoField.MONTH_OF_YEAR);
// returns 5 (May is 5th month of year)

DayOfWeek dayOfWeek = dateNow.getDayOfWeek();
// return sunday
```

Alter parts of the date
```java
LocalDate changedDayOfWeek = dateNow.withDayOfMonth(DayOfWeek.FRIDAY.getValue());
// return 2018-05-05

LocalDate dateWithChangedYear = dateNow.with(ChronoField.YEAR, 2024);
// returns 2024-05-13

```

## LocalTime

Very similar methods to those in LocalDate

## LocalDateTime

Very similar methods to those in LocalDate


```java

```

### Links



## ZoneDateTime

## Duration

- https://docs.oracle.com/javase/8/docs/api/java/time/Duration.html

## Time measurement

A great way of measuring how long a method call takes.

```java
long startTime = System.currentTimeMillis();

someMethodToMeasure();

long endTime   = System.currentTimeMillis();

long totalTime = endTime - startTime;

```

- http://tutorials.jenkov.com/java-date-time/time-measurement.html
## links

- https://dzone.com/articles/java-8-date-and-time
- http://www.oracle.com/technetwork/articles/java/jf14-date-time-2125367.html
- http://www.baeldung.com/java-8-date-time-intro
- https://www.tutorialspoint.com/java8/java8_datetime_api.htm
- https://www.journaldev.com/2800/java-8-date-localdate-localdatetime-instant
- http://tutorials.jenkov.com/java-date-time/index.html
- https://github.com/winterbe/java8-tutorial#date-api
