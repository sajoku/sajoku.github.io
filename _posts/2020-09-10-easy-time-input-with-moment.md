---
layout: post
title: Input times easily by converting shorthand times
intro: Create timestamps from values like "10d" or "10d 2h 1m"
tags: typescript javascript moment momentjs
---

For a project I want to enter timestamps. But I want to make it fairly easy and
fast for the user to do this. There are a few users that are a bit more adept to
working with a console and so I figured entering times by hand would be awesome 🚀.

This project works with bootstrap 4 so it already makes use of
bootstrap-timepicker. This means you'll get a nice popup and can select a date
time from there with your mouse.

The thing I'm after is being able to enter something like "10d" or "1d 12h" and
calculate what that would be in a timestamp. "10d" meaning today + 10 days.
1d 12h meaning today + 1 day + 12 hours.

I recently got into TypeScript and figured this would be a nice thing to make
with it. Here goes:

```typescript
declare var moment: any;
export class EasyTimeInput {
  datetimeInput: HTMLInputElement;
  regex = new RegExp(/([0-9]{1,3}[d,h])/gi);
  oneDayInMinutes = 1440;
  oneHourInMinutes = 60;
  oneMinute = 1;

  //Call this with `new EasyTimeInput(document.querySelector("input"))`
  constructor(inputElement: HTMLInputElement) {
    this.datetimeInput = inputElement;

    //check if the given input actually exists or do nothing
    if (this.datetimeInput) {
      this.listenToUserInput();
    }
  }

  //Listen to the blur event; If the input looses focus this triggers
  listenToUserInput() {
    this.datetimeInput.addEventListener("blur", () => {
      this.setCalculatedTime(this.datetimeInput);
    });
  }

  //receives the input element and changes the value
  setCalculatedTime(datetime: HTMLInputElement) {
    var calculatedTime = this.calculateTimeStamp(datetime.value);
    datetime.value = calculatedTime;
  }

  //calculates a new date and time based on the given value
  calculateTimeStamp(givenValue: string): string {
    var self = this;

    var minutesToAdd: number = 0;
    //Match against things like '10d 1h' or '1d' or '11m'
    var matches: string[] = givenValue.match(self.regex) || [];

    //loop through the matches and add the correct 'minutes' to the
    //result. For 1d this would do 1*1440
    Array.prototype.forEach.call(matches, function (match: any) {
      let multiplier = self.oneDayInMinutes;
      if (match.indexOf("h") !== -1) {
        multiplier = self.oneHourInMinutes;
      }
      if (match.indexOf("m") !== -1) {
        multiplier = self.oneMinute;
      }

      minutesToAdd += multiplier * parseInt(match);
    });

    //Create a new Date object and inject the time into it
    let newDateObj = new Date(new Date().getTime() + minutesToAdd * 60000);
    //return a new moment object formatted into a string
    return moment(newDateObj).format("DD-MM-YYYY HH:mm");
  }
}
```

disclaimer: There are some things specific to my environment
so this might not work for you.

The line `declare var moment: any;` is there as `moment` is a global variable in
this app. This makes it available to this class without having to import it.

If you have any suggestions on improving this code or just want to shout out
shoot me tweet @sajku or email hey@muliphen.nl 👍🏻
