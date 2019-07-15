automatically generate color themes from background images.
also allows jinja2 templating for config files and callbacks

# requires
* python3

# configuration
``` yaml
# a folder containing pictures to cycle through
background_dir: ~/Pictures/Backgrounds 
# a folder containing templates
template_dir: ~/.ricer/templates

templates:
  # each field is the name of a template in template_dir
  alacritty.yml: 
    # dest marks the destination for the rendered template
    dest: ~/.config/alacritty.yml
    # link will create a symlink from dest to the given path.
    link: ~/.alacritty/alacritty.yml
  i3config.sh: 
    dest: ~/.config/i3config.sh
    link: ~/.i3/config
    # callback will be run after successfully rendering the template
    callback: i3-msg restart
  # you can also just specify the destination if you don't need anything else
  theme.vim: ~/.vim/colors/theme.vim
```

# variables
* color: a list of 16 colors in the format `RRGGBB`
* background: an absolute path to the image used
* msg: a message that warns not to edit the rendered file and links to the template.

# TODO
* tolerate failure in a template


probably want to separate this into a few stages.
* determine background image and palette
    * http://charlesleifer.com/blog/suffering-for-fashion-a-glimpse-into-my-linux-theming-toolchain/
    * http://blog.z3bra.org/2015/06/vomiting-colors.html
* template config files with the palette
    - https://www.reddit.com/r/unixporn/comments/8giij5/guide_defining_program_colors_through_xresources/
* execute callbacks to update running programs
* default to solarized theme https://github.com/altercation/solarized

ideas:
* palette creation should fail if the input image isn't very color diverse
    - this should prevent any unreadable configs
* may want to steer around xresources considering wayland is a thing
* fonts
