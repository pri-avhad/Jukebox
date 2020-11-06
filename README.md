# Jukebox
## Audio Player using Arduino

Please note that this project also requires SPI and SD libraries. These are built-in libraries.

Implementation:
The Arduino in the circuit shown above loads the .wav files from the micro-SD card. It then generates a signal and outputs it through the speaker connected to digital pin 9. This allows the speaker to create sounds and play Audio. 
The .wav files used in this circuit have a slight limitation in playing audio. Since a Arduino is used, it cannot read complex .wav files. Therefore, the .wav files should be converted to have these dimensions:
Samples Per second (Hz): 16000 
Channel: Mono
Bits Per Sample: 8
As mentioned earlier, the speaker is connected to Pins 9 and GND (not shown in the circuit diagram). Additionally, we need to connect SD Card Module and 3 Push Buttons. Since the interface between Arduino UNO and SD Card Module is through SPI Communication, the connections the connections are as follows.
The CS Pin of SD Card Module is connected to Pin 4. Chip Select (CS) pin can be connected to any Digital I/O Pin but the rest of the SPI Pins of SD Card Module must be connected to corresponding SPI Pins of Arduino. SCK or SPI Clock Pin of SD Card is connected to Pin 13 of Arduino. The MOSI and MISO pins of SD Card Module are connected to Pins 11 and 12 of Arduino UNO respectively. The power pins i.e. VCC and GND are connected to +5V and GND of Arduino.
Additionally, We have used 3 push buttons to control the music playback. Play / Pause Button is connected to Pin 5, Next Track Button is connected to Pin 6 and Previous Track Button is connected to Pin 7 of Arduino. All these buttons are configured with internal pullups in the program.

Preparing Audio Files and PCM Library
•	WAV Files
Before proceeding further, there are a couple of things we need to take care of. The first one is to convert our audio / music files to WAV format i.e. they should be .wav files. This is because, the supporting libraries, which I will mention next, support only PCM Audio in WAVE File Format (.wav).
So, our first step is to convert our mp3 files to .wav files. For this we can use any audio converter software, the convert option in VLC Media Player or any online tools. I will be using an online tool called ONLINE-CONVERT.com. It supports multiple files like archives, audio, documents etc.
Go to the Audio converter option in the website and select “Convert to WAV” option or simple use this website - https://audio.online-convert.com/convert-to-wav


Upload the mp3 file and in the optional settings, set the following:

Change bit resolution: 8 Bit,
Change sampling rate: 16000 Hz, 
Change audio channels: mono, 
PCM format: PCM unsigned 8-bit

After making the above-mentioned changes, click on start conversion and the converted file will be downloaded automatically.

•	PCM Library
The second important thing is to add a special library called TMRpcm developed by TMRh20. We can download it directly from the official GitHub page or we can add it directly in the Arduino IDE.
In Arduino IDE, go to Tools Manage Libraries… and search for “TMRpcm” and click on install.

Working of Arduino based Music Player
After making the hardware connections as mentioned above, getting audio files ready, setting up the Arduino IDE (install libraries), we are ready to implement our own audio player using Arduino.
First, format the microSD Card as FAT using any formatting software like SD Memory Card Formatter and copy all the WAV audio files to the card. Insert the card into the slot on the SD Card Module and make all the necessary connections.
Connect Arduino to computer and in the Arduino IDE, use the above given code. In the code, make necessary changes i.e. in the void song () function, replace the file names with the song names in our SD card.
We have named all my audio files as song1.wav, song2.wav, etc. and used the same names in the function. After making necessary changes, upload the code.
By default, the first song (i.e. song1.wav) will play automatically once the Arduino is reset. We can use the Play / Pause Button to well, play or pause the current track. Use Next Button to play the next track and Prev Button to play the previous track.
