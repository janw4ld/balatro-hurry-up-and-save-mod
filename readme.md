# hurry up and save

this patch addresses two annoyances in Balatro:

- progress and settings saves are written to disk once every 5 seconds, which
  - loses settings changes when someone quits too quickly after changing their settings
  - allows players to alt+f4 to undo a mistake in a run
  - makes progress losses after a crash bigger than expected
- the quit button on the main menu just closes the game no matter what's going on, and this contributes to settings loss

computers in 2025 (at least on my platform of choice, linux) have very high IOPS & disk throughput and can handle a lot of writes no problem. so the patch:

- changes the save timer to 0.5s instead of 5
- modifies the quit button's callback to wait for all save events to complete before closing the game, so nothing is lost even if you quit before the 0.5s period

the save timer's period can be changed [here](https://github.com/janw4ld/balatro-hurry-up-and-save-mod/blob/main/lovely.toml#L15) if 0.5s is too quick for you or you wanna keep it at 5s to make use of "undo" but don't want the quit button to throw away your changes.
