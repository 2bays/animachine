# animachine
"""
The original plan for this project was to become an animation recording mechanism that would edit a
live animation in the same vein as a looping drum machine.  The tool ended up being a little clunky,
but the way we interacted with a clock coming from external midi devices changed in the process.

I am eager to move forward and continue the animation machine development, but I wanted to ask you
about three parts in particular.

#1 Does the way I've mapped the midi incoming from an APC40 make sense?  Years ago, I was having a 
problem with midiinmap CHOP cooking every time I touched any knob of 80 on an APC40, so I split it up
based on banks and seems to be performing properly, but I'm unsure if it is bad practice to split up a
midi device so many times like I have.

#2 Revolves around the use of GAL components in chops/profile_builder.  I'm unsure if I have the components properly "clone immune."
Also, I wrote a script to repopulate the Value1 parameters of the GAL components in the case you want to edit
a previously confirmed bank of parameters.  It's called text4 and it is the top most text in the profile_builder contatiner.
I'm unsure if this is a proper method or I would be better off editing local storage to change these values.

#3 Centers around a topic discussed during a 'Let's Talk Touch' session with Ian.  You were describing a
method to clone a base into another base so you can re-use effects.  I created a bin full of bases with a
series of logics in them to turn on and off lights.  The issue I'm having is, if the container
chops/base_beat is not opened, the scripts will not alter the clone parameter when I hit the corresponding
trigger on my midi controller.  Everything changes, the period of each effect, the direction, but it's 
always the same pattern.

Order of Signal

chops/beat
	The genesis of this project begins with BPM incoming from a DJM-900.  Any suitable BPM value can be substituted
	and placed into time_null.  For this demonstration I've already switched the tempo 126 BPM.

#	bar_reset
#		Inside chops/beat/bar_reset, the bpm is used by beatCHOPs to create a series of ramps that are used
#		to power lookups and logics later.

#		b79 (mod.buttons.b79) is the master button that resets each period to 0 and lock the beat to the incoming music.

chops/profile_builder
	Inside of profile_builder are dats that have presets loaded to them.  Each column of a dat corresponds
	to either b[1-40:8]	or b[2-40:8].  These scripts don't use MOD though, it calls from the midi device directly.  

	The scripts are located in chops/selectors/column1 and column2 respectively.

	 

chops/base_beat
	Here, the information for period, pattern, direction are cloned into bins for color and the two types of beat, 
	Accent and Beat.

	To reiterate, one of the main problems I'm having is that these scripts will not populate the clones the way I intend.
	When the container is opened in my network, every thing works as expected, but if I navigate away from the container and push
	the buttons the dreaded red x will appear on any container above base_beat.  The period and direction change normally
	but the pattern will not change.  When I click into base_beat, the red x's disappear and the pattern immediately 
	changes to what it should be.

fixtures
	channels from chops/base_beat/beat_out, base_beat/accent, and base_beat/color_per_fix are fed into  wall washer LEDs and
	par can LEDs.

	The signal intensity for the washers is on s1 and the cans are on s2.  

"""




