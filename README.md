NodaTime.NetworkClock
=====================

A `NodaTime.IClock` implementation that gets the current time from an NTP server instead of the computer's local clock.

```
PM> Install-Package NodaTime.NetworkClock
```

Example Usage:

```csharp
// Just like SystemClock, you can obtain a singleton instance
var clock = NetworkClock.Instance;

// Optionally, you can adjust some settings.
// These are the defaults, and can be omited if you aren't going to change them.
clock.NtpServer = "pool.ntp.org";              // which server to contact
clock.CacheTimeout = Duration.FromMinutes(15); // how long between calls to the server

// Call .Now to get the current time
Instant now = clock.Now;

// Like any clock, you can then convert to the local time zone
DateTimeZone tz = DateTimeZoneProviders.Tzdb["America/New_York"];
ZonedDateTime zdt = now.InZone(tz);

// Of course, you can convert this to whatever format makes sense in your application.
// You can use any of the following:
LocalDateTime ldt = zdt.LocalDateTime;
OffsetDateTime odt = zdt.ToOffsetDateTime();
DateTimeOffset dto = zdt.ToDateTimeOffset();
DateTime dt = zdt.ToDateTimeUnspecified();
```
