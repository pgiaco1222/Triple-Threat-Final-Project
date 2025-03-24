# Triple-Threat-Final-Project
SCO file for the "Triple Threat" final project.

amp = 8000
env = maketable("line", 1000, 0,0, 0.5,1, 1,0.8, 9,0.7, 10,0)
wave = maketable("wave", 1000, "buzz")
st = 0
dur = 0.1

srand(22/7)

for(i = 0; i < 99; i=i+1)
{

	freq=pickwrand(65, 40, 98, 40, 110, 10, 116, 5, 55, 5)
	pan = irand(0.0, 1.0)
	dur = pickwrand(0.1, 60, 0.25, 30, 0.05, 10)
	WAVETABLE(st, dur, amp*env, freq, pan, wave)
	WAVETABLE(st+0.1, dur, amp*env, freq*2.01, pan, wave)
	st = st + dur
}
