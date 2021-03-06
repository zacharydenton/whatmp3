whatmp3 is a small script to create mp3 torrents out of FLACs.

Depends on mktorrent, lame/oggenc/ffmpeg/neroAacEnc+neroAacDec, and metaflac.

Configuration is handled at the top of the file in the configuration section.

Usage
-----
Running `whatmp3` on its own won't do too much. You need to specify the lame or oggenc flags you want to convert with, and the directories you want to convert.

    --320 --V2 --V0 --Q8 --ALAC --FLAC...
        encode to 320, V2, V0, or whatever else specified in 'enc_options' in the file
    --original
        create torrent for original FLACs
    --help
        print help message and quit
    --verbose
        increase verbosity (default false)
    --moveother
        move other files in flac directory to torrent directory (default true)
    --output="PATH"
        specify output directory for torrents
    --zeropad
        zeropad tracklists (default true)
    --dither
        dither FLACs to 16/44 before encoding (default false)
    --passkey="PASSKEY"
        specify tracker passkey
    --tracker="TRACKER"
        specify tracker address to use (default "http://tracker.what.cd:34000")
    --notorrent
        do not generate a torrent file (default false)
    --threads=NUM
        run NUM encoding threads (default 1)
    --replaygain
        enables replaygain (default false); please note replaygain is not allowed on what.cd
    --upload
        uploads torrents to What.CD after creating them
    
Minimally, you need a passkey, a tracker, and an encoding option to create a 
working torrent to upload

If you would like to upload that torrent after creating it, you will additionally 
need the mechanize library and a What.CD username and password.

You need to add your torrent passkey and output directory in order to make the `.torrent` file to upload to What.CD:

    passkey = "YOUR PASSKEY HERE"

To upload the torrent after creating it, specify your What.CD username and password like so:
    
    username = "USERNAME"
    password = "PASSWORD"

This will convert `OSI - Office of Strategic Influence` to V2 and V0:

    whatmp3 --V2 --V0 OSI\ -\ Office\ of\ Strategic\ Influence

This will convert `Porcupine Tree - Deadwing` and `Porcupine Tree - In Absentia` to 320 CBR, V0, and V2 (the "perfect three"):

    whatmp3 --320 --V2 --V0 Porcupine\ Tree\ -\ Deadwing Porcupine\ Tree\ -\ In\ Absentia

`.torrent` files will be created in your `output` directory.

This will encode a FLAC release to V0, V2, 320, Q8, and AAC (by default), and then upload torrents for FLAC, V0, V2, 320, Q8, and AAC to What.CD:
    
    whatmp3 --original --upload Various\ - 1996\ - Icelandic\ Folk\ Music\ [FLAC]

The --original option should only be specified if the release does not yet exist on What.CD. If you are adding new formats or a different release, do not use the --original option. Instead, specify the '[Add format]' URL when prompted for the upload URL.

This will dither a 24 bit FLAC release to V0 and 16 bit FLAC, and upload to What.CD:

    whatmp3 --dither --upload --V0 --FLAC "Led Zeppelin - I (Classic 200) (PBTHAL Vinyl Rip 2010) 192kHz"

Threading is supported since version 3.0; use the `--threads NUM` option (or set `max_threads`):

    whatmp3 --threads 2 --V2 "Enslaved - Isa"

`whatmp3` also supports a few command line flags as of 2.0, use `--verbose` or `-v` to print extra messages:
    
    whatmp3 --verbose --V2 Nightingale\ -\ I
