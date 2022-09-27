# HasiboundLite

Adds new Lua functions, fixes some bugs, and more.

**For 64 bit Starbound only.** I recommend to play with that version anyway.

Likely incompatible with my old DLLs, but this one makes them obsolete. It includes an improved songbook search, and (almost) every Lua function of the old one.
Feature list below.
I still have many things planned, but since the progress is so slow I wanted to release this now.

Consider supporting me on [ko-fi](https://ko-fi.com/thefurrydevil), I really need it.

## Installation
- Replacer method: Navigate to your Starbound's win64 folder, rename **zlib1.dll** as to not override it, and paste my **zlib1.dll** and **hasiboundlite.dll**

I plan to add other methods of loading my DLLs.

## Features
I still have many things planned to add!

### Lua functions
All Lua functions added by this DLL are prefixed with _ to avoid name clashing.

`table or boolean` `_keys([number])` if a number is given returns whether the [SDL_ScanCode](https://wiki.libsdl.org/SDL_Scancode) key is pressed, else returns a table with every pressed key, in **string:SDL_ScanCode** pairs

`boolean` `_textInputActive()` returns whether Starbound wants text input (used to optionally ignore keypresses from **\_keys()**

`[string]` `_clipboard([string])` if a string is given sets that string as Windows clipboard text, else returns the current

`table` `_unsafe(string)` if called with the configured unsafe_key (see Config section below) returns a table with functions that are normally unavailable, else throws an error. This is used to access functions like **load** and **os.execute** without disabling Starbound's **safeScripts** setting

`player` `_star_player()` returns userdata with functions for the current player entity
- `integer, integer` `get_aim_position()`
- `set_body_directives(string)`
- `set_description(string)`
- `set_emote_directives(string)`
- `set_facialHair_group(string)`
- `set_facialHair_type(string)`
- `set_facialHair_directives(string)`
- `set_facialMask_group(string)`
- `set_facialMask_type(string)`
- `set_facialMask_directives(string)`
- `set_gender(string)`
- `set_hair_group(string)`
- `set_hair_type(string)`
- `set_hair_directives(string)`
- `set_name(string)`
- `set_species(string)`

`image` `_star_image(string)` returns userdata with functions for the given image
- `integer` `w()` width
- `integer` `h()` height
- `integer` `r(integer, integer)`
- `integer` `g(integer, integer)`
- `integer` `b(integer, integer)`
- `integer` `a(integer, integer)`
- `integer, integer, integer` `rgb(integer, integer)`
- `integer, integer, integer, integer` `rgba(integer, integer)`

### Songbook
- search/filter for songs (supports regular expression, automatic support for vanilla and extended songbook, can be modded to support other songbook replacers)
- automatically selects the new search field when opened
- navigate songs using arrow keys
- press Tab to switch between search field and band name, press Enter to play song

### Widgets
- scroll areas now have smooth scrolling and support holding shift for scrolling horizontally
- improved scroll logic

### Privacy
- do not send player inventory to server (prevents advanced item stealing)

### Misc
- world geometry can be made "hollow", allowing you to walk inside of it (if inside of it using a teleport, for example). This also vastly improves performance with /boxes enabled `physics.hollow_world`
- show your own characters (local entities) name when holding the highlight key `tweaks.show_local_names`
- render gui ontop of debug `tweaks.interface_over_debug`
- fix chatbubble movement delay

## Config
The DLL uses its own config that can be modified ingame using commands.
Examples:

`/hasiboundlite config set physics.hollow_world true`
`/hasiboundlite config set lua.unsafe_key test1234`

By default every option will be set to no value, which in most cases means disabled. (`physics.hollow_world` for example is disabled, meaning vanilla world geometry)
