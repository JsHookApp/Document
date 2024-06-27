# media

Used to play music

## media.create(data)

`Parameters`:

`data`: url address or file base64 value

`Return value`: instance

After calling, it will play automatically by default, no need to call start

## [Instance].start()

Start playing

## [Instance].pause()

Pause playing

## [Instance].stop()

Stop playing

## [Instance].loop(state)

`Parameters`:

`state`: boolean

Whether to play in a loop, by default, music is played only once

## media.closeAll()

Close all instances
