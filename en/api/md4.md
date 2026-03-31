# media

Play audio files.

## media.create(data)

`Parameters`:

`data`: URL or file base64 value

`Returns`: instance

Playback starts automatically after creation — no need to call start.

## [instance].start()

Start playback.

## [instance].pause()

Pause playback.

## [instance].stop()

Stop playback.

## [instance].loop(state)

`Parameters`:

`state`: boolean

Enable/disable loop playback. Audio plays once by default.

## media.closeAll()

Close all instances.
