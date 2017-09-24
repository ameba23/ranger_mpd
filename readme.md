
# using ranger for playing music

I love ranger file manager and i love mpd (music player daemon).  While there are some good mpd clients available, its good to be able to play music directly from a file manager because other file operations can be performed to organise the collection as well.  and because rangers interface is powerful and familiar to me.  i still use ncmpcpp for managing playlists.  Actually i much prefer the interface of 'practical music search' [pms](https://ambientsound.github.io/pms/) but i had some problems with it (which might have been resolved by now...)

I already have keybindings in my window manager to toggle pause, skip and seek with mpd so it is not really needed to add these to ranger. but i put this one in anyway:

    map . shell -f mpc seek +5
    map , shell -f mpc seek -5


## embedded cover art previewing using ffmpeg
in ranger's scope.sh, in the section: 

    if [ "$preview_images" = "True" ]; then

add:

    case "$extension" in
       # Use ffmpeg to extract album art from mp3:
       # todo: if this fails, just display the first jpg in the dir. 
       mp3)
            ffmpeg -y -i "$path" "$cached" && exit 6 ;;
    esac


## script to play tracks and directories (recursively) even if they are outside of the mpd database directory.  

    # Play file(s) or directories in mpd (using a script) - this can also play files outside of mpd music directory.
    map P shell -f find %s -type f | sort | mpcaddnew 

    # queue file(s) or directories to end of mpd playlist but do not play them (even if they are outside of mpd database) 
    map ba shell -f find %s -type f | sort | mpcaddnew --noplay

## more features:
* keybinding to jump to currently playing song (from wiki)
* wrapper to colourise exiftool, for when no cover art is available. exiftool provides a lot of information and i can be difficult to see the tags which are most interesting (title, artist, album)
