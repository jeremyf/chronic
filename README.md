Chronic
=======

## DESCRIPTION

Chronic is a natural language date/time parser written in pure Ruby. See below
for the wide variety of formats Chronic will parse.


## INSTALLATION

The best way to install Gollum is with RubyGems:

    $ [sudo] gem install chronic


## USAGE

You can parse strings containing a natural language date using the
Chronic.parse method.

    require 'rubygems'
    require 'chronic'

    Time.now   #=> Sun Aug 27 23:18:25 PDT 2006

    #---

    Chronic.parse('tomorrow')
      #=> Mon Aug 28 12:00:00 PDT 2006

    Chronic.parse('monday', :context => :past)
      #=> Mon Aug 21 12:00:00 PDT 2006

    Chronic.parse('this tuesday 5:00')
      #=> Tue Aug 29 17:00:00 PDT 2006

    Chronic.parse('this tuesday 5:00', :ambiguous_time_range => :none)
      #=> Tue Aug 29 05:00:00 PDT 2006

    Chronic.parse('may 27th', :now => Time.local(2000, 1, 1))
      #=> Sat May 27 12:00:00 PDT 2000

    Chronic.parse('may 27th', :guess => false)
      #=> Sun May 27 00:00:00 PDT 2007..Mon May 28 00:00:00 PDT 2007

See Chronic.parse for detailed usage instructions.


## EXAMPLES

Chronic can parse a huge variety of date and time formats. Following is a
small sample of strings that will be properly parsed. Parsing is case
insensitive and will handle common abbreviations and misspellings.

Simple

* thursday
* november
* summer
* friday 13:00
* mon 2:35
* 4pm
* 6 in the morning
* friday 1pm
* sat 7 in the evening
* yesterday
* today
* tomorrow
* this tuesday
* next month
* last winter
* this morning
* last night
* this second
* yesterday at 4:00
* last friday at 20:00
* last week tuesday
* tomorrow at 6:45pm
* afternoon yesterday
* thursday last week

Complex

* 3 years ago
* 5 months before now
* 7 hours ago
* 7 days from now
* 1 week hence
* in 3 hours
* 1 year ago tomorrow
* 3 months ago saturday at 5:00 pm
* 7 hours before tomorrow at noon
* 3rd wednesday in november
* 3rd month next year
* 3rd thursday this september
* 4th day last week

Specific Dates

* January 5
* dec 25
* may 27th
* October 2006
* oct 06
* jan 3 2010
* february 14, 2004
* 3 jan 2000
* 17 april 85
* 5/27/1979
* 27/5/1979
* 05/06
* 1979-05-27
* Friday
* 5
* 4:00
* 17:00
* 0800

Specific Times (many of the above with an added time)

* January 5 at 7pm
* 1979-05-27 05:00:00
* etc


## TIME ZONES

Chronic allows you to set which Time class to use when constructing times. By
default, the built in Ruby time class creates times in your system's local
time zone. You can set this to something like ActiveSupport's TimeZone class
to get full time zone support.

    >> Time.zone = "UTC"
    >> Chronic.time_class = Time.zone
    >> Chronic.parse("June 15 2006 at 5:45 AM")
    => Thu, 15 Jun 2006 05:45:00 UTC +00:00


## LIMITATIONS

Chronic uses Ruby's built in Time class for all time storage and computation.
Because of this, only times that the Time class can handle will be properly
parsed. Parsing for times outside of this range will simply return nil.
Support for a wider range of times is planned for a future release.


## CONTRIBUTE

If you'd like to hack on Chronic, start by forking the repo on GitHub:

http://github.com/github/chronic

To get all of the dependencies, install the gem first. The best way to get
your changes merged back into core is as follows:

1. Clone down your fork
1. Create a thoughtfully named topic branch to contain your change
1. Hack away
1. Add tests and make sure everything still passes by running `rake`
1. If you are adding new functionality, document it in the README
1. Do not change the version number, we will do that on our end
1. If necessary, rebase your commits into logical chunks, without errors
1. Push the branch up to GitHub
1. Send a pull request for your branch