# pyNPS
<p align="center">
<img src="https://octodex.github.com/images/pythocat.png" width="448" height="448">
</p>

PyNPS is a [Nopaystation](https://beta.nopaystation.com/) client writen in python3.7 that, with the help of [wget](https://www.gnu.org/software/wget/) and [pkg2zip](https://github.com/mmozeiko/pkg2zip/), can search, download and decrypt/extract PSVita, PSP and PSX games from Nopaystation database. It's basically a command line version of [NPSBrowser](https://nopaystation.com/vita/npsReleases/) writen by a moron (aka me).

Before downloading any of your legally obtained (wink wink wink) pkg file you have to update your NPS database, you don't have to do it every time you want to download something, but only in your first run to construct your initial database and after that just once in a while to get info about new pkgs NPS adds to their database:

Updating all system's databases:
>$ python3.7 main.py -c _all -u

<br/>
Updating database per console:

>$ python3.7 main.py -c psv -u #updates only vita's db

>$ python3.7 main.py -c psp -u #updates only psp's db

>$ python3.7 main.py -c psv -u #updates only psx's db

Database is located by default at: /home/USER/.config/pyNPS/database
******
## Configuration file
Configuration file is created at: /home/USER/.config/pyNPS/settings.ini

If you delete it, it'll be recreated with default parameters in the next run. The options are pretty much self explanatory.

******
## pkg2zip
This script uses lusid1's pkg2zip, as [recomended by NoPayStation](https://twitter.com/NoPayStation/status/1096508850080043010), to handle the .pkg extractions, you have 3 options:

1. You can can a binary, compiled by myelf (version 2.2) [here](https://gofile.io/?c=ov20wF), just drop it inside /home/USER/.config/pyNPS/lib/ after that pyNPS will autodetect and use it automatically, no need to add the path to your config file;

2. If you're an Arch or Suse user, you can compile it from [AUR](https://aur.archlinux.org/packages/pkg2zip-fork/), after you install it pyNPS will autodetect and use it automatically, no need to add the path to your config file;

3. Or you can just grab the sources from lusid1's repo and compile it yourself [here](https://github.com/lusid1/pkg2zip/releases), drop the binary here /home/USER/.config/pyNPS/lib/ after that pyNPS will autodetect and use it automatically, no need to add the path to your config file;

In case you decide to store your binary outside /home/USER/.config/pyNPS/lib/ you'll need to specify this folder in your config file unde the "pkg2zip_location" option.

******
## wget
This software uses wget to make the downloads therefore it won't work if you don't have it installed in your system, most distros already come with wget installed, if you don't have it chances are you're on some crazy non-userfriendly distro and you probably know your way around for installing it. If you don't just google.

You can drop a wget binary at /home/USER/.config/pyNPS/lib/ after that pyNPS will autodetect and use it automatically, no need to add the path to your config file.

In case you decide to store your binary outside /home/USER/.config/pyNPS/lib/ you'll need to specify this folder in your config file unde the "wget_location" option.
******
## Examples: searching
Updating the PSP database and searching for a Sonic game in any region:
>$ python3.7 main.py -c psp -u -dg sonic
```
Updating Database for Playstation Portable:
Downloading File: PSP_GAMES.tsv [###################-] 98% 550K @ 71.4K/s
renaming file: ./DATABASE/PSP/PSP_GAMES.tsv ./DATABASE/PSP/GAMES.tsv
Downloading File: PSP_DLCS.tsv [####################] 100% 450K @ 100%/s
renaming file: ./DATABASE/PSP/PSP_DLCS.tsv ./DATABASE/PSP/DLCS.tsv
Downloading File: PSP_THEMES.tsv [####################] 100% 0K @ 100%/s
renaming file: ./DATABASE/PSP/PSP_THEMES.tsv ./DATABASE/PSP/THEMES.tsv
Downloading File: PSP_UPDATES.tsv [####################] 100% 0K @ 928K=0.02s/s
renaming file: ./DATABASE/PSP/PSP_UPDATES.tsv ./DATABASE/PSP/UPDATES.tsv
1 ) ULUS10323 | US   | GAMES | Sonic Rivals 2 | 455.7 MiB
2 ) ULES00622 | EU   | GAMES | Sonic Rivals | 195.1 MiB
3 ) ULES00940 | EU   | GAMES | Sonic Rivals 2 | 219.8 MiB
4 ) ULUS10195 | US   | GAMES | Sonic Rivals | 196.8 MiB
Enter the number for what you want to download, you can enter multiple separated by commas:
```
******
Search for an european release of spyro for PSX
>$ python3.7 main.py -c psx -r eur -dg spyro
```
1 ) NPEE00074 | EU   | GAMES | Spyro 2: Gateway to Glimmer  | 343.6 MiB
2 ) NPEE00074 | EU   | GAMES | Spyro 2: Gateway to Glimmer (German store)  | 343.6 MiB
3 ) NPEE00074 | EU   | GAMES | Spyro 2: Gateway to Glimmer (Russian store)  | 343.6 MiB
4 ) NPEE00075 | EU   | GAMES | Spyro: Year of The Dragon  | 339.6 MiB
5 ) NPEE00075 | EU   | GAMES | Spyro: Year of The Dragon (German store)  | 339.7 MiB
6 ) NPEE00075 | EU   | GAMES | Spyro: Year of The Dragon (Russian store)  | 339.6 MiB
7 ) NPEE00076 | EU   | GAMES | Spyro the Dragon  | 329.8 MiB
8 ) NPEE00076 | EU   | GAMES | Spyro the Dragon (German store)  | 329.8 MiB
9 ) NPEE00076 | EU   | GAMES | Spyro the Dragon (Russian store)  | 329.8 MiB
Enter the number for what you want to download, you can enter multiple separated by commas:
```
******
Search for for themes and demos related to the word "touhou in any region:
>$ python3.7 main.py -c psv -dt -dde touhou
```
1  ) PCSE00947 | US   | THEMES | Touhou Genso Rondo Theme | 6.723 MiB
2  ) PCSE00990 | US   | THEMES | Touhou Genso Wanderer PlayStation Vita Theme | 4.514 MiB
3  ) PCSE01104 | US   | THEMES | Touhou Kobuto V: Burst Battle 4 Theme | 4.038 MiB
4  ) PCSB01039 | EU   | THEMES | Touhou Genso Wanderer PlayStation Vita Theme | 4.514 MiB
5  ) PCSB01129 | EU   | THEMES | Touhou Kobuto V: Burst Battle Theme 4 | 4.038 MiB
6  ) PCSG00999 | JP   | THEMES | Touhou Kobuto V | 2.533 MiB
7  ) PCSE01104 | US   | THEMES | Touhou Kobuto V: Burst Battle Theme 3 | 5.581 MiB
8  ) PCSE01104 | US   | THEMES | Touhou Kobuto V: Burst Battle Theme 2 | 5.174 MiB
9  ) PCSE01104 | US   | THEMES | Touhou Kobuto V: Burst Battle Theme 1 | 2.533 MiB
10 ) PCSG90252 | JP   | DEMOS  | Touhou Soujinengi V (DEMO) | 335.6 MiB
Enter the number for what you want to download, you can enter multiple separated by commas:
```
******
Search for for everything (themes, games, demos, dlcs and updates) related to the word "knight" in any region region:
>$ python3.7 main.py -c psv knight

<br/>
Or if you like suffering:

>$ python3.7 main.py -c psv -dg -dd -dt -du -dde knight
```
1  ) PCSE00244 | US   | GAMES   | Valhalla Knights 3 | 897.8 MiB
13 ) PCSA00017 | US   | DLCS    | LittleBigPlanet Knights of Old Pre-Order Costume Pack | 100 KiB
49 ) PCSB00861 | EU   | THEMES  | Digimon Story Cyber Sleuth Custom Theme: Royal Knights Set | 4.999 MiB
53 ) PCSB00743 | EU   | UPDATES | Shovel Knight | 120.8 MiB
Enter the number for what you want to download, you can enter multiple separated by commas:
```
******
I see... you just wanna everything related to Shovel Knight? Sure:
>$ python3.7 main.py -c psv "shovel knight"
```
1 ) PCSE00640 | US   | GAMES   | Shovel Knight | 132.2 MiB
2 ) PCSB00743 | EU   | GAMES   | Shovel Knight | 137.6 MiB
3 ) PCSE00640 | US   | THEMES  | Shovel Knight Theme | 4.34 MiB
4 ) PCSE00640 | US   | UPDATES | Shovel Knight | 124.1 MiB
5 ) PCSB00743 | EU   | UPDATES | Shovel Knight | 120.8 MiB
Enter the number for what you want to download, you can enter multiple separated by commas:
```
******
Wanna return every single american DLC for the psvita? Sure, it's slow but it's a free country:
>$ python3.7 main.py -c psv -r usa -dd _all
```
that's too big to output here, mate :<
```
******
## Examples: syntax for selecting files to download
After you make your search you'll probably want to download something, if it's a single file that's pretty easy, just type the number when asked and it'll start the download for you. If you wanna multiple downloads, you can always separate the numbers by commas. But there's an even more advance (and cool) way for downloading things, and that's using "slices", here's how to do it with some examples:
>$ python3.7 main.py -c psv -dt -dde touhou
```
1  ) PCSE00947 | US   | THEMES  | Touhou Genso Rondo Theme | 6.723 MiB
2  ) PCSE00990 | US   | THEMES  | Touhou Genso Wanderer PlayStation Vita Theme | 4.514 MiB
3  ) PCSE01104 | US   | THEMES  | Touhou Kobuto V: Burst Battle 4 Theme | 4.038 MiB
4  ) PCSB01039 | EU   | THEMES  | Touhou Genso Wanderer PlayStation Vita Theme | 4.514 MiB
5  ) PCSB01129 | EU   | THEMES  | Touhou Kobuto V: Burst Battle Theme 4 | 4.038 MiB
6  ) PCSG00999 | JP   | THEMES  | Touhou Kobuto V | 2.533 MiB
7  ) PCSE01104 | US   | THEMES  | Touhou Kobuto V: Burst Battle Theme 3 | 5.581 MiB
8  ) PCSE01104 | US   | THEMES  | Touhou Kobuto V: Burst Battle Theme 2 | 5.174 MiB
9  ) PCSE01104 | US   | THEMES  | Touhou Kobuto V: Burst Battle Theme 1 | 2.533 MiB
10 ) PCSG90252 | JP   | DEMOS   | Touhou Soujinengi V (DEMO) | 335.6 MiB
Enter the number for what you want to download, you can enter multiple numbers using commas:
```
* To download files 1 to 9, the masochist method, you type: 1,2,3,4,5,6,7,8,9
* To download files 1 to 9, the cool-kid method, you type: 1-9
* To download files 1 to 5 and files 8 to 10: 1-5,8-10
* To download files 1, 4 and files 6 to 10: 1,4,6-10
* To download files 1, 4 and files 6 to 10, the crazy way, as the software doesn't care about order or duplicates: 10-6,1,4,6

******

For more information just run:
>$ python3.7 main.py -h

```
usage: main.py [-h] [-c {psv,psp,psx,_all}] [-r {usa,eur,jap,asia}] [-dg]
               [-dd] [-dt] [-du] [-dde] [-u]
               [search]

positional arguments:
  search                search something to download, you can search by name
                        or ID or use '_all' to return everythning.

optional arguments:
  -h, --help            show this help message and exit
  -c {psv,psp,psx,_all}, --console {psv,psp,psx,_all}
                        the console you wanna get content with NPS.
  -r {usa,eur,jap,asia}, --region {usa,eur,jap,asia}
                        the region for the pkj you want.
  -dg, --games          to download psv/psp/psx games.
  -dd, --dlcs           to download psv/psp dlcs.
  -dt, --themes         to download psv/psp themes.
  -du, --updates        to download psv/psp game updates.
  -dde, --demos         to download psv demos.
  -u, --update          update database.

```
