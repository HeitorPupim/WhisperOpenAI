# WhisperOpenAI
Usage of Whisper AI to translate/transcribe audio files.

<h2> Run WhisperAI in the Command Line. </h2>
credits to Kate Weber @ deepbram tutorials


<h3> Setup </h3>

You'll need python on your machine, at least version 3.7. Let's set up a virtual environment with venv (or conda or the like) if you want to isolate these experiments from other work.

```
mkdir whisper
cd whisper
python3 -m venv venv
source venv/bin/activate

# always a good idea to make sure pip is up-to-date
pip3 install --upgrade pip

```

Next, install a clone of the Whisper package and its dependencies (torch, numpy, transformers, tqdm, more-itertools, and ffmpeg-python) into your python environment.

```
pip3 install git+https://github.com/openai/whisper.git 
```

Especially if it's pulling torch for the first time, this may take a little while. The repository documentation advises that if you get errors building the wheel for tokenizers, you may also need to install rust. You'll also need ffmpeg - installation depends on your platform. Here are some examples:

```
# on Ubuntu or Debian
sudo apt update && sudo apt install ffmpeg

# on Arch Linux
sudo pacman -S ffmpeg

# on MacOS using Homebrew (https://brew.sh/)
brew install ffmpeg

# on Windows using Chocolatey (https://chocolatey.org/)
choco install ffmpeg

# on Windows using Scoop (https://scoop.sh/)
scoop install ffmpeg
``` 

<h3> Using the Tool </h3>

Great! You're ready to transcribe! In this example, we're working with [Nicholas Tesla's vision of a wireless future](https://ia800604.us.archive.org/1/items/nonfiction025_librivox/snf025_nikolateslawirelessvision_anonymous_gu.mp3) - you can get this audio file at the LibriVox archive of public-domain audiobooks and bring it to your local machine if you don't have something queued up and ready to go.

The OpenAI Whisper tool has a variety of models that are English-only or multilingual, and come in a range of sizes whose tradeoffs are speed vs. performance. You can learn more about this [here](https://github.com/openai/whisper#available-models-and-languages). We, the researchers at Deepgram, have found that the small model provides a good balance.

``` 
whisper "snf025_nikolateslawirelessvision_anonymous_gu.mp3" --model small --language English
```

```
[00:00.000 --> 00:09.880]  Nikola Tesla sees a wireless vision by Anonymous, the New York Times, 3rd October, 1915.
[00:09.880 --> 00:11.920]  This is a LibriVox recording.
[00:11.920 --> 00:14.920]  All LibriVox recordings are in the public domain.
[00:14.920 --> 00:20.200]  For more information or to volunteer, please visit LibriVox.org.
[00:20.200 --> 00:23.760]  Nikola Tesla sees a wireless vision.
[00:23.760 --> 00:29.080]  Things his world system will allow hundreds to talk at once through the Earth.
[00:29.080 --> 00:31.760]  Trans-static disturbance.
[00:31.760 --> 00:37.480]  Inventor hopes also to transmit pictures by the same medium which carries the voice.
[00:37.480 --> 00:43.880]  Nikola Tesla announced to the Times last night that he had received a patent on an invention
[00:43.880 --> 00:50.320]  which would not only eliminate static interference, the present bugaboo of wireless telephony,
[00:50.320 --> 00:55.520]  but would enable thousands of persons to talk at once between wireless stations and make
[00:55.520 --> 01:01.920]  it possible for those talking to see one another by wireless regardless of the distance separating

...

[07:25.160 --> 07:30.520]  Wireless is coming to mankind in its full meaning like a hurricane some of these days.
[07:30.520 --> 07:36.120]  Some day there will be, say, six great wireless telephone stations in a world system connecting
[07:36.120 --> 07:42.080]  all the inhabitants on this earth to one another, not only by voice, but by sight.
[07:42.080 --> 07:45.240]  Its surely coming.
[07:45.240 --> 07:50.940]  End of Nikola Tesla sees a wireless vision by Anonymous, The New York Times, 3rd October
[07:50.940 --> 08:13.840]  1915.
```

