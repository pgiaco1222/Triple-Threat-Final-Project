# Triple-Threat-Final-Project
# SCO file for the "Triple Threat" final project.
# This solo project will plan on creating a 3 minute song using RTCMix coding, hardware synthesis, and VST Instruments. 

rtsetparams(41000, 2)
bus_config("WAVETABLE", "aux 2-3 out")
bus_config("EQ", "aux 2-3 in", "out 0")

bus_config("NOISE", "aux 0-1 out")
bus_config("FILTSWEEP", "aux 0-1 in", "out 0")



st = 0
dur = 0.15
amp = 10000


env = maketable("line", 1000, 0,0, 0.1,1, 1,0.8, 10,0)
waveform = maketable("wave", 2000, "buzz14")



notes = {pchlet("Db3"), pchlet("Eb3"), pchlet("F3"), pchlet("Ab3"), pchlet("Db3"), pchlet("C4")}
pitch = len(notes)

duration = {4, 8, 2, 6, 8, 2}
mult = len(duration)

pan = makeLFO("sine", 0.01, 0.35, 0.65)

amp2 = 0.8
FiltType = 0  //0: lowpass, 1: highpass, 2: lowshelf, 3: highshelf, 4: peaknotch
Input = 1
Bypass = 0 //0: bypass off, 1: bypass on
cutoff = 12000
CutEnv = maketable("line", 1000, 0,0, 10, 1)
resonance = 5.0


RingDown = 1
Steep = 1.9
Balance = 1
Input = 0
Bypass = 0 
CentFreq = makeLFO ("sine", 0.5, 1000, 8000)
CentEnv = maketable("line", 2000, 0,0, 0.1,1, 1,0.8, 10,0)
BWidth = -0.25


for (i = 0; i < 24; i = i + 1)
{

index = i % (pitch)
freq = notes[index]

index2 = i % (mult)
durMult = duration[index2]


WAVETABLE(st, dur*durMult, amp*env, freq, pan, waveform)
EQ(st, 0, dur, amp2, FiltType, Input, pan, Bypass, cutoff*CutEnv, resonance) 

NOISE(st, dur, amp*env, pan)
FILTSWEEP(st, 0, dur, 1, RingDown, Steep, Balance, Input, pan, Bypass, CentFreq*CentEnv, BWidth)

st = st + dur
}
notes[4] = pchlet("Eb4")

for (i = 0; i < 24; i = i + 1)
{

index = i % (pitch)
freq = notes[index]

index2 = i % (mult)
durMult = duration[index2]


WAVETABLE(st, dur*durMult, amp*env, freq, pan, waveform)
EQ(st, 0, dur, amp2, FiltType, Input, pan, Bypass, cutoff*CutEnv, resonance) 

NOISE(st, dur, amp*env, pan)
FILTSWEEP(st, 0, dur, 1, RingDown, Steep, Balance, Input, pan, Bypass, CentFreq*CentEnv, BWidth)

st = st + dur
}
notes[3] = pchlet("Bb3")
notes[4] = pchlet("F4")
notes[5] = pchlet("Dd4")

for (i = 0; i < 24; i = i + 1)
{

index = i % (pitch)
freq = notes[index]

index2 = i % (mult)
durMult = duration[index2]


WAVETABLE(st, dur*durMult, amp*env, freq, pan, waveform)
EQ(st, 0, dur, amp2, FiltType, Input, pan, Bypass, cutoff*CutEnv, resonance) 

NOISE(st, dur, amp*env, pan)
FILTSWEEP(st, 0, dur, 1, RingDown, Steep, Balance, Input, pan, Bypass, CentFreq*CentEnv, BWidth)

st = st + dur
}

//amp = 1
//FiltType = 0  //0: lowpass, 1: highpass, 2: lowshelf, 3: highshelf, 4: peaknotch
//Input = 1
//pan2 =  0.0 //makeLFO("sine", 0.5, 0.0, 1.0)
//Bypass = 0 //0: bypass off, 1: bypass on
//cutoff = makeLFO("sine", 0.11, 220, 8000)
//resonance = 5.0

//EQ(0, 0, 100, amp, FiltType, Input, pan2, 0, cutoff, resonance)
//EQ(0, 0, 100, amp, FiltType, Input, pan2, 0, cutoff, resonance)
