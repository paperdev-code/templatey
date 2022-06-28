```                            
# 888888888888                                          88                                               
#      88                                               88                ,d     
#      88                                               88                88                             
#      88   ,adPPYba,  88,dPYba,,adPYba,   8b,dPPYba,   88  ,adPPYYba,  MM88MMM  ,adPPYba,  8b       d8  
#      88  a8P_____88  88P'   "88"    "8a  88P'    "8a  88  ""     `Y8    88    a8P_____88  `8b     d8'  
#      88  8PP"""""""  88      88      88  88       d8  88  ,adPPPPP88    88    8PP"""""""   `8b   d8'   
#      88  "8b,   ,aa  88      88      88  88b,   ,a8"  88  88,    ,88    88,   "8b,   ,aa    `8b,d8'    
#      88   `"Ybbd8"'  88      88      88  88`YbbdP"'   88  `"8bbdP"Y8    "Y888  `"Ybbd8"'      Y88'     
#                                          88                                                   d8'      
#      Paperdev's incredibly basic         88         file creation & automation tool!         d8'       
```
---
I needed a very simple tool to automate some very simple things.

`curl -LO https://raw.githubusercontent.com/paperdev-code/templatey/main/templatey`

## Usage
`./templatey -c <config files> -t <template files>`

## What?
This is a tool for quickly creating many files based on templates, and filling in the gaps with values defined in a config.

### Config files
These files have a very simple syntax.
Here is a **complicated** config called 'templatey.config' with a custom selector:
```
# This is a comment

@selector=@...@

background-color=#334466
foreground-color=#664433
```
This particular selector is the default, so it can be omitted.

#### Selectors
Sometimes, you might use many different file types, and some characters may already have meaning. So multiple selectors can be defined aswell:
```
# Anything with the following pattern works! (yes, even spaces)
@selector=#...#
@selector=<templatey>...</templatey>
```
**When selectors are defined, the default selector is replaced!**

#### Keys and values
The keys and values are used to replace content inside the template.
```
# Anything can be a key, as long as the beginning is alphabetic!
some entry = some value
# the key 'some entry ', would be replaced with ' some value' (yes, this includes spaces!)
```
### Template files
These can be any file that you feed to the program, they likely contain your patterns somewhere in them.
For example, take the file style.css.templatey:
```css
body {
  background-color: @background-color@;
  color: <templatey>foreground-color</templatey>;
}
```
Note: The template file can have any extension, after processing, the extension is removed.

### Usage
Running the command
```sh
./templatey -c templatey.config -t style.css.templatey 
```
The following file named 'style.css' will be produced.
```css
body {
  background-color: #334466;
  color: #664433;
}
```
### Predefine arguments
To run the program by only typing `./templatey`, arguments can be predefined in the top of the script.
Simply add all templates and configs to `CONFIG_FILES` and `TEMPLATE_FILES` respectively.

## What's with the spaces?
Parsing is incredibly naive, I might write a decent parser in the future. But I won't encounter it in my usecases.
