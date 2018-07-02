talking-clock
=============

A highly configurable clock written in bash with soundpack and voice options.
Written by Storm Dragon
Released under the terms of the WTFPL: http://wtfpl.net, or see the included LICENSE file.

talking-clock can chime and/or announce the time when called usually by cron. It is highly configurable. It can be set to chime every hour, quarter, hour or half hour. For instructions on editing the crontab file see man crontab. Here are some suggested entries:
#chime every hour between 10:00AM and 10:00PM
0 10-22 * * * talking-clock
#chime every half-hour:
0,30 * * * * talking-clock
#chime every quarter-hour:
0,15,30,45 * * * * talking-clock
talking-clock can modify cron for you. to do so use
talking-clock --cron number
where number is 1 for every hour, 2 for every half-hour, or four for every quarter-hour. Any other entry removes talking-clock settings from, causing talking-clock to not chime at all unless called specifically by you. The --cron switch only allows one argument, using multiple arguments will not work. If you use the --cron argument it must be the first argument follow by only one other argument.

talking-clock understands the following arguments:
-a --audio Sound command. Command to play sound. the default is play -q provided by the sox package. Another example, if you have vorbis-tools installed would be
ogg123 -q
or
paplay
Note that with the ogg123 command the aplay command is used for the pico voice. Aplay will not work for the rest of the commands because it does not play ogg files.
-c --nochime Turn off chimes.
-n --nospeak turn off spoken time.
-s --soundpack Set path to soundpack. Sound packs should be in ogg format and contain 1.ogg, 2.ogg, ... 11.ogg, 12.ogg and 15.ogg, 30.ogg, and 45.ogg for the quarter-hour chimes.
-t --torify anonymously get your current temperature, used with -z --zipcode.
-v --voice Select voice. Default is espeak other options are
cepstral, espeak, festival, flite, flite_time googletts (requires the translate-shell package), pico, speech-dispatcher and custom.
To set a custom voice enter the command as in:
-v 'espeak -v en-us+klatt2'
zipcode and flite_time are incompatable. If you have zipcode set the temperature will not be read while using flite_time.
-z --zipcode Postal code: Will speak the temperature along with the time so long as you do not have nospeak set. E.G. -z 90210

talking clock can also read settings from the following files?
/etc/talking-clockrc global settings
XDG_CONFIG_HOME/talking-clock/talking-clockrc
(Usually XDG_CONFIG_HOME is ~/.config)
Settings for individual users. If both files exist the user specific settings will be used. Command line arguments are considered all powerful and will override all others.

Configuration files should be written as command=setting. Here is an example of a configuration file:
format=24
sound=play -q
soundpack=/home/USER/thunderstorm
chime=true
speak=true
zipcode=90210
torify=true
Soundpack should be the path to a directory. Do not include the trailing / talking-clock adds it for you.
voice=espeak -v en-us+klatt2 -s 300
Be careful when using custom voice commands, if it is not valid the program will not work. You do not have to specify parameters for voice commands if you want to use the defaults. You can use voice=espeak (this is the default), voice=cepstral, voice=speech-dispatcher, voice=pico, or voice=festival.

Creating soundpacks is very simple. Make a directory named anything you wish, thunderstorm for example, and place files inside it. The naming scheme for soundpack files follows the hours 1 through 12 and quarter hours 15, 30, 45. Each sound file must be in .ogg format. So, your directory will contain 1.ogg, 2.ogg, ... 12.ogg, 15.ogg, 30.ogg, and 45.ogg. If hourly chimes sound the same, use a bell for example, just name the chime bell.ogg. If hourly chimes should be prepended with a sound, then name the sound prepend.ogg, will play at each hour, before the chimes.To download or submit soundpacks go to:
https://stormdragon.tk/talking-clock/

If you wish to contact me you can find me on GNU Social as @storm@social.stormdragon.tk. Also don't forget to check out my blog located at:
https://stormdragon.tk/
I can also usually be found on irc.talkabout.cf in channel #a11y
