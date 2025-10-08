# Challenge: Omniscient Flag's Metadata
As you step into the second chamber, a figure manifests. Before you stands a forgotten deity, a dead god spoken of only in whispers. Known by countless names: “Apostle of Epilogue and Eternity”, “Lone Messiah” and many more lost to time.

They leave nothing but a single image, a relic carrying his final secret. Hidden within its layers lies the key to ascend to the next chamber.

## Solution: 
- The very first analysis of the image file using online tools and ChatGPT provided one clear answer: this image had a second layer.
- The very first method used to find the layer was importing into lightroom. However that method seemed to return no results.
- AI was able to easily isolate all image layers. The top layer, the mid layer and a puzzling blank looking last layer.
- The middle layer contained the flag clearly written.

# Challenge: Test of Sweetness
This floor feels like a digital world. The space is an illusion, all pink and sweet, stretching around you in impossible patterns. Here, you are no longer a climber but just another user.

Ahead, a door glows faintly. It is the only path forward and requires a level of authority you do not yet have. Fragments of session memory flicker, hinting at what it might take to gain higher access.

## Solution: 
- Firstly, open inspect element pane.
- The challenge hinted at using cookie manipulation.
- It was a challenge to find the correct cookie, but it was easy to change user's access by rewriting permission user to admin.

# Challenge: Randomly Accessed Memories
On your ascent to this floor, you hear these fragments being played back



clone it, pull it, reset it, stage it,
commit, push it, fork, rebase it,
merge it, branch it, tag it, log it,
add it, stash it, diff, untrack it.



You look around and discover a chamber containing a vast archive of Daft Punk’s music, intertwined with cryptic commits left behind by other musicians. They seem ordinary at first glance, but not everything in the history is what it seems.

Challenge: https://github.com/evilcryptonite/daft-punk-archive

## Solution:
- The first clue was the line "intertwined with cryptic commits left behind by other musicians".
- I entered the commits list of the given github project.
- Manually scrolling showed 6 commits that were named differently.
- These 6 files gave the 3 parts of the flag easily.

# Challenge: Echoes and Pings
You come across the remnants of a fallen corporation and the final network communication ever sent by them.

Allegedly, the message contained an image that predicted the rise of the Citadel. Your task is to uncover what was sent and decode the communication to extract the passcode that will unlock the next floor.

## Solution:
- First, I had to figure out what .pcap was. It is a network log type file.
- Found an online tool to open it. It shoed hundreds of network logs.
- Since the description mentioned pictures, I went through all the pictures and found nothing.
- As a last ditch attempt, I asked ChatGPT to analyse the file.
- It easily found the correct image with the flag.

# Challenge: Selected Ambient Work
The symphonic adventure does not end here. On the next floor, a single song keeps echoing through the floor, repeating in a haunting loop. Amid the sound, you find a note left by a past candidate. It hints that the song holds a secret message, hidden in plain sight, much like how Aphex Twin concealed his face within his music with the help of spectrograms.

To move forward, you must find the message hidden in this sound.

Note: Separate the words in the flag with _ and make it UPPERCASE. Example: citadel{S3L3CT3D_AMB13NT_W0RK}

## Solution: 
- Listening to the .wav file showed clear morse code.
- An audibly different tone for the citadel, { and } were there.
- To filter the music out, the audio was recorded on another mic. This successfully filtered the music to near 0.
- That new wav file shows the flag. ChatGPT and online wav analysers were used.
