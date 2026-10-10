# Make your own product videos with Claude + Fish Audio

By @vibha.in.progress · paid partnership with Fish Audio · https://fish.audio/?fpr=9m9vy8

## Prompt 01

```
I'm not technical, so do everything for me. Connect Fish Audio to this project so you can voice my videos.
1. Add the Fish Audio MCP server: claude mcp add --transport http fish-audio https://api.fish.audio/mcp
   Then tell me to run /mcp so I can sign in to my Fish Audio account. It uses OAuth, so no API key is needed for this part.
2. Install the official Fish Audio skill pack: npx skills add https://docs.fish.audio
   It adds two skills, fish-audio-sdk and fish-audio-api, so you write correct Fish Audio code.
3. For scripted voiceovers, use the free model s2.1-pro-free through the Fish Audio API. Create a .env file and open it for me so I can paste my key from fish.audio/app/api-keys. Never print the key, never put it in code or in chat.
4. Test everything: generate one 5-second line in a warm English voice, play it for me, and tell me the voice name, how long it took and where the file is saved.
If I need to click anything or restart the app, tell me exactly what, step by step.
```

## Prompt 02

```
I'm not technical, so do everything for me. You're my motion design director. In [FOLDER, e.g. ~/motion-refs/] there are [NUMBER] screen recordings of motion design videos I love. Study every one of them frame by frame before you write anything. If ffmpeg isn't installed, install it first.
1. Extract frames: ffmpeg -i "$f" -vf "fps=4,scale=1280:-1" frames/$name/%04d.jpg
2. Find every cut: ffmpeg -i "$f" -vf "select='gt(scene,0.3)',showinfo" -f null - and log the timestamps
3. Make a contact sheet per video: ffmpeg -i "$f" -vf "fps=1,scale=480:-1,tile=6x4" sheets/$name.jpg, then read every sheet
For each video give me: the palette (hex), the type (families, weights, sizes), every camera move, the transition at each cut, easing and pace (average shot length in seconds), signature moves worth stealing and moves to avoid.
Finish with ONE house style I can reuse: 10 rules, each pointing to the frame it came from. Save it as house-style.md and show it to me.
```

## Prompt 03

```
Using house-style.md, storyboard a [30-45]s product video for [PRODUCT] ([WEBSITE]).
First pull the brand palette, fonts and logo from the website.
Give me a beat table: time, scene, on-screen text, voiceover line, motion, sound effect.
Cut every 1.5 to 3 seconds on a [122] BPM grid, with the drop at [12.0]s.
Story: problem, then the turn, then a product tour, then proof, then the logo.
Then wireframe every scene as a simple grey-box frame and render ONE storyboard sheet so I can approve the layout.
Don't build anything in colour until I say go.
```

## Prompt 04

```
I'm not technical, so do everything for me. Build the video from the storyboard I approved.
Use HyperFrames (free and open source, github.com/heygen-com/hyperframes) to write every scene as HTML and render it to MP4. Install it if it isn't there.
Follow house-style.md exactly. Recreate the product's screens in code instead of using blurry screenshots, so every frame stays sharp.
Output 1920x1080 at 30fps, plus a 1080x1920 vertical version for Reels.
Leave clearly marked gaps where the voiceover goes.
Before rendering, show me a contact sheet of the key frames and wait for my notes.
```

## Prompt 05

```
Audition voices for this script. Pick 5 Fish Audio library voices that fit [CHARACTER, e.g. a calm British helpdesk agent]. No celebrity clones.
Have each voice read the same 2 lines: one emotional, one businesslike, so I can hear the range.
Save them as voice-1-[name].mp3 to voice-5-[name].mp3 in audio/auditions/.
Give each one a one-line note: tone, pace, what it's best for.
Transcribe every take with Whisper to check every word came out right.
Then wait for me to pick.
```

## Prompt 06

```
Now direct the performance like a voice actor, using the voice I picked.
Add Fish Audio S2.1 Pro emotion tags in square brackets wherever the feeling changes. Pair a physical cue with an emotion, for example [sighs] [frustrated], [empathetic], [calm], [surprised].
Tags affect everything after them, so place them exactly where the mood shifts.
Vary pace and pauses to match the beat sheet. Re-generate any line that sounds flat.
Check every take with Whisper, then show me the script with the tags so I can approve it.
```

## Prompt 07

```
Be my sound designer for this video. Use Mixkit (mixkit.co) as the ONLY source for music and sound effects.
1. First read Mixkit's Sound Effects Free License and Stock Music Free License and confirm they cover commercial use in social video.
2. From my beat sheet, list every sound we need: a whoosh before each transition, a thump on hard cuts, pops for on-screen UI, a riser into the drop, and one music bed at [122] BPM.
3. Search mixkit.co for each one, download the best 2 options into audio/sfx/ and audio/music/, and log the title, URL and license of every file in CREDITS.md.
4. Detect every cut and beat in my render with ffmpeg, place the sound effects on them and duck the music 8 dB under the voiceover.
5. Master to -14 LUFS and send me a 10-second preview before the full export.
```

## Prompt 08

```
Final pass. Put it all together: the approved video, the Fish Audio voiceover and the Mixkit sound.
Line the voiceover up with the beat sheet so every line lands on its scene.
Render the final MP4 at 1080p, 30fps, in both 16:9 and 9:16.
Then play it back in your head beat by beat, fix anything that feels rushed or off the grid, and tell me what you changed.
Last, give me a list of the 3 frames you'd use as thumbnails.
```