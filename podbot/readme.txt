POD-bot 3.0 metamod.

This version of POD-bot MUST be used with metamod. You MUST have metamod
installed in order to run it. Forget about editing the liblist.gam, it simply
won't work.

Get metamod from http://www.metamod.org, or install AdminMod or AMX Mod X 
(since AdminMod or AMX Mod X installs metamod automatically during the setup).

Then edit metamod's plugins.ini file and add a line like this one:

   win32 addons/podbot/podbot_mm.dll

or

   linux addons/podbot/podbot_mm_i386.so

depending on whether you run Windows or Linux. Once you do that the bot is
installed and ready to work.

If it doesn't, TRIPLE CHECK your installation before complaining. It's most
likely your fault. First ensure that metamod is installed and working. Then,
bring down the server console and type "meta list". If metamod reports "BADF"
then most likely you placed the POD-bot folder in the wrong directory. The
"podbot" folder MUST be in the "cstrike" (or "czero") directory.

This version of POD-bot works with Counter-Strike 1.5, 1.6 and CZERO

We advise you to delete any previous .pxp files that you may have used with
former versions of this bot.

Since the bot now supports the new CS 1.6 weapons, you MUST use the included
bot_weapons.cfg file which takes them into account. If you attempt to use an
older weapon configuration file from POD-bot 2.5 or 2.6, the bot will crash.

The bot settings are cvars now (since V3) - read more in podbot.cfg.
The "addbot" command has been changed into "add" command (but the syntax 
is not changed). All podbot command need to use "pb" prefix in front of them. 
Also those for waypointing. Examples:
pb add
pb wpmenu
pb menu

A Bots United production.
http://forums.bots-united.com/
