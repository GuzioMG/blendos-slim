# blendOS Slim
These are slightly modified and re-structured base BlendOS tracks in the way ico277 thought is better ([according to Ast3risk](https://asterisk.lol/blog/blend_v4/), this mainly entails it being more lightweight - hence the name of this project: blendOS Slim). I thought the same, with a couple of caveats:
* I'm not a big fan of getting rid of Waydroid (yes, I know, you can re-add it - but whoever controls the defaults, controls the world, and I quite like the message being sent by including it by default: blendOS blends *all* Linux distros, even Android. Yes, I just claimed Android is a Linux distro. Fight me.) - although I *do* believe there is value in letting users opt out of it (A lot of people might not need it, thus only causing bloat for them. And this is supposed to be the Slim version, after all - so limiting bloat should be the top priority). As such, this repo provides both Waydroid-free (ico277's) and Waydroid-enabled (just like the OG ones) tracks.
* Despite ico277 aiming to be more lightweight, they included `xorg` in the base track for desktop, which carries quite a lot of unnecessary bloat for anyone on Wayland. I changed that by separating X.Org-enabled versions from those that don't ship it.
* I'm not a big fan of getting rid of OpenSSH from the base version, personally. So I restored it! I also added `zip`, `unzip`, `wget` and `htop` to the list while at it. I know this is supposed to be the Slim version, but just 5 extra packages (or even 4, if you count compared to the OG version) ain't a lot (certainly less than the gigabytes of bloat from the default version) - and these tools are found on nearly all Linux systems out there. I'm surprised that they weren't included in the OG version (except OpenSSH), to be honest. I know some folks might prefer `curl` over `wget`, so I contemplated not including `wget` (in case you haven't realized - the theme of this repo is, broadly speaking, „more choice to the user” and (as such) no defaults are usually blindly assumed), but then I remembered that most of these people typically have `wget`, anyway, since a lot of scripts depend on it.
* On KDE, Konsole and Doplhin are forced upon you. While I like Dolphin, personally - I understand why someone might want to swap it out for something simpler. Konsole, meanwhile, I like to replace with Yakuake (for most stuff) and KiTTY (as a fallback) - and I can't be the only one not using Konsole, right? Anyway, these packages were removed from the KDE track. This, however, also leaves it without any terminal or file browser - so be careful about that.

## WARNING!!!
These are experimental and may be broken in some weird ways! In their version, `ico277` said „If such thing occurs, please contact me on discord at `ico278`” and I initially planned to change it to „If such thing occurs, please contact me on Discord at `.guzio.`”, but on second thought - I probably couldn't help you anyway, even if you contacted me. I only applied some slight changes to ico277's repo. Or, well, I guess changes are pretty substantial - but at the end of the day, when you install a track, the total packages you get are similar. So... Contact ico277 directly, then? But it doesn't feel right to dump my repo's problems onto someone else. As such, let me say this: If a problem occurs, try to debug it yourself (if you can't, contact *both* me *and* ico277 - preferably via [blendOS's Discord](idk), to avoid pointless duplications). Some package is likely missing, so just throw things at the wall and see what sticks. Once you discover what's missing, please open a Pull Request, so that everyone can benefit from it. I'll then try to contribute it back to ico277's repo, if relevant. *(Also, I know that by the sound of this paragraph it may seem like me and ico277 are buddies - but I actually never heard of them up until recently.)*

## Available tracks:
* Lightweight TTY: `core`
* Lightweight TTY without WiFi support: `server-base` (as the name implies, it's just the base of a complete server track - if you want to deploy it on a server and have it do anything useful there, you'll need a lot more packages, eg. Docker or nginx)
* Pre-made base for a custom desktop: `desktop-base` (`desktop-base-x11` for a version with X.Org pre-installed; `desktop-base-waydroid` for a version with Waydroid pre-installed)
* GNOME: `gnome` (`gnome-x11` for an X.Org version; `gnome-waydroid` for a version with Waydroid pre-installed)
* KDE Plasma: `kde` (`kde-x11` for an X.Org version; `kde-waydroid` for a version with Waydroid pre-installed)
* Cinnamon: `cinnamon`
* LXQT: `lxqt`
* MATE: `mate`
* XFCE: `xfce`
* Hyprland: `ico277` (custom Hyprland setup according to whatever ico277 uses, use at your own risk)
* My personal setup: `guzio`

## Usage Examples
Example `/system.yaml` files using this repo:
### Directly installing a track, as-is from this repo:
Unless you're installing the `guzio` track (like in the example shown below), this is probably not recommended, as no other desktop track ships a web browser. So, at minimum, one should add `firefox` or their preferred browser. Also, for KDE users, it's crucial to install a terminal.
```
repo: 'https://pkg-repo.blendos.co/'

impl: 'https://github.com/ico277/blendos-tracks/raw/main'

track: 'guzio'
```
### Modifying a track:
In the following example, I added `firefox` to the `cinnamon` track (as recommended above).
```
 repo: 'https://pkg-repo.blendos.co/'

 impl: 'https://github.com/blend-os/tracks/raw/main'

 track: 'cinnamon' 

 packages: 
     - 'firefox'
```
### Hungry for more?
Check out [Ast3risk's guide](https://asterisk.lol/blog/blend_v4/) or [the official blog post](idk) for some more `/system.yaml` examples and its documentation (such as how to add more repos, run comands on build-time or enable services).

## License
You might've noticed something strange: I forked a GPL3-licensed repo, but now it's suddenly MIT-licensed. Why? Well, GPL just kinda... Doesn't make sense for this use case, to be honest. *(Also, I kinda despise the whole „FOSS or die” mentality (being more pragmatic, I care more about Open Source Software - FOSS's practical implications without any ideological nonsense attached to it) and the FSF, but I digress).*

The core assumption of GPL is that ANY modification done to the codebase must be contributed back to the community (not necessarily merge them into the base repo, but at the very least publish your own fork).

What does it mean in practice? Well, imagine you want to modify one of the tracks in this repo. You point your local `/system.yaml` to it, add whatever packages you need, and carry on. Great! But... Did you contribute the changes back to the community? You didn't! The only place they're stored is inside the `/system.yaml` on your machine. Thankfully, this is not a problem. Proprietary software can depend on FOSS, as long they're not bundled together and one only references the other - which is the case here („point your local `/system.yaml` to it”). But what if you want to *remove* a package instead? Well, since the tracks system only allows layering new packages on top without removing existing ones - the only way to do it is to copy-paste whatever track you wanted to modify into your `/system.yaml` and remove the package from there. And... Uh-oh, we have a problem! You just copied GPL-licensed material and modified it! Unless you now contribute it back, you're breaking the law! Obviously, no one would sue you for removing a package (I don't know who ico277 is IRL, but I doubt they have the resources for a lawsuit over such a stupid thing. It's kind of like *unethically obtaining* media (games, movies, whatever) from studios that went bankrupt - technically it's still illegal, but no one can afford to enforce it anymore.), but such a possibility even existing sounds unbelievably stupid, nevertheless.

As such - I re-licensed this repo under MIT. How is this ever legal? Well, as I said earlier - „Proprietary \[or anything non-GPL] software can depend on FOSS \[ie. GPL, in this case], as long they're not bundled together and one only references the other”. So, the only MIT-licensed files in this repo are those created from scratch (they only reference GPL ones). These are:
* the README (with the exception of code snippets in Usage Examples - first one being derived from ico277's GPL-licensed README (this technically means that I'm embedding GPL code into MIT code, which might not be legal - except Markdown files are considered text works, not code, and as such aren't covered by the GPL. I think so, at least), and the other one from [Ast3risk's blog post](https://asterisk.lol/blog/blend_v4/), whatever license they use)
* anything that ends with `-x11` or `-waydroid`
* `guzio` and `core` tracks

...and the rest are modified GPL-licensed files - and they stay GPL3, sadly.
