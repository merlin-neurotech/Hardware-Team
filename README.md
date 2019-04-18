# Hardware-Team
As this was the inaugural year for Merlin’s Hardware Team, we started this project with no prior knowledge, no previous projects to look back on, and no graduate students or professors as advisors to help guide us along the way. Once we got started, we realized quickly that it wasn’t an easy task to build an EEG acquisition board with none of the above resources available. What we did realize however, was that we didn’t want any other club who was starting up to have to go through the same hardships that we were going through. This is why the goal of our project was to create a simple acquisition board that new teams would be able to complete, and also create a library of resources alongside it to help teach these teams along the way. 

# Background Research
When developing a design for an EEG acquisition board, you first need to understand what the process of reading brain waves involves. As your brain transmits data, it is sending electrical impulses through the different neurons that are located in your brain. This creates voltage differences that vary with time, in circular firing patterns, that depending on the action the brain is performing, can show reproducible data when read. Therefore, by obtaining frequency domain data from these voltage differences, we can obtain meaningful frequency responses that correspond to actions, such as concentration or eye movement. 

If the raw data is obtained from the voltage differences, you won’t be able to obtain meaningful responses. Signal processing must be applied to remove meaningless artifacts and constant noise from the data signal. The data that is desired is usually the alpha waves and the beta waves of the brain. These waves occur between the 8-12 Hz and 12-30 Hz frequency ranges, respectively, and therefore you can realistically filter out all other frequencies so that the data can be properly analyzed. On top of this, the standard signals that are received are far too small to be able to properly analyze. Therefore, during the signal processing some form of gain must be applied to the signal using amplifiers. 

# Design Process
The first element of the circuit is what takes data straight from your brain. As mentioned before, a voltage difference in the electrical impulses is what we want to measure. To obtain this, we’ll want at least three electrodes, two at different areas on your head that are experiencing electrical impulses, and one located at a “ground”. This “ground” is usually located at a point on your head that experiences no electrical, or very few, impulses. Therefore, while the other areas are experiencing electrical potentials, it is always in reference to these area that is experiencing no electrical stimulation. To analyze this, an instrumentation amplifier is used which takes the voltage difference between your two inputs, and compares that to the reference ground that is set. The instrumentation amplifier then amplifies the signal by a gain factor that is dependant on a resistor between its 1 and 8 pins.

The second element is a series of filtering components. Through the use of capacitors, resistors, inductors, and an operational amplifier, lowpass, highpass, bandpass, and bandstop filters can be implemented. For our design, lowpass, highpass, and bandstop filters were used. Lowpass filters are used to filter out unnecessary data that is greater than the frequencies we’re focusing on, or letting the low frequencies pass through, highpass filters are used to filter out unnecessary data that is lower than the frequencies we’re focusing on, letting the high frequencies pass through, and the bandstop filter, otherwise known as a notch filter, removes frequencies that are at a single frequency or range of frequencies. On top of this, the op-amp also helps to amplify the signal by a gain factor that is determined by resistors connected from the inverting, negative, input to the output. The main filters needed are 60 Hz notch filters, due to noise from power lines, highpass filters below 7 Hz, and lowpass filters above 30 Hz.

The last part of the design is implementing the method of data transfer to the computer. Depending on the amount of analog signal ports you have, the channels of the board can be increased, allowing for data to be collected from more electrodes. The cheapest option available is just using your computer as the controller. The sound card in your computer allows for two channels to be used as it can choose sound between left and right speakers, so by hooking up your acquisition board to an aux cable that goes into your computer it can act as a two channel board. The next option that is slightly more costly is using a microcontroller such as an arduino or a raspberry pi. An arduino has six analog channels already built in and therefore can turn your board into a six channel board. Using a raspberry pi alongside a simple analog-to-digital converter, your board can have eight channel capabilities. These can continue to be extended by using multiplexers that can create boards that have upwards of 64 channels, however more hardware will need to implemented, otherwise good data won’t be able to be acquired as it won’t be able to filter the data while cycling through all 64 channels at a rate fast enough to acquire a good signal.

# Problems
Initial problems with designing the board were all oriented around the use of a breadboard. When trying to implement complex designs onto a small breadboard, it is very easy to have things get disconnected, miswired, or have wires touching that shouldn’t be. This makes getting a proof of concept very difficult, because the circuit can work in theory but you need to rebuild it many times to get functional data. 

The next issue was with ordering parts for the PCB. During the design stage not all part choices had their corresponding part number recorded. Therefore, when parts were being ordered to go with the PCB there were issues with the screw terminals and variable resistor because different ones were ordered then the ones that the PCB was designed for. The variable resistor was actually a three pin potentiometer, but it was still able to be soldered to the board. However, the screw terminals had pin distances that were too far apart, and therefore wires had to be soldered directly to the board instead of the much cleaner design that was intended with screw terminals.

The last hardware issue was with our electrodes. The only electrodes we had available to us were dry electrodes that were quite old, having very worn contacts. This lead to our data that was acquired to be very poor and inconsistent

Other than the above issues with getting a functional design and ordering parts, the largest setback was being a team with no experience. As this was the first year of Merlin’s Hardware Team, there was no previous resources, research, or designs to build off of. On top of this, the team consisted entirely of 1st, 2nd, and 3rd year undergraduate students. This meant that for us, we had no prior neurotechnology experience, as well as many members had no electronics experience. Therefore, the entire first semester and half of the second semester was entirely dedicated to doing research into neurotechnology, and teaching members some of the basics of circuit design and electronics. This large research base did aid the team in the end, allowing for a final design and PCB to be completed, and creating a library of knowledge that is available to future members of the team. 

# Final Design
The final design incorporated two 60 Hz notch filters, a 1 and a 7 Hz highpass filter, and a 31 Hz lowpass filter. The two 60 Hz notch filters allowed for removal of the majority of power line noise, while the 1, 7 and 31 Hz filters allowed for removal of the excess data that isn’t within the range of the alpha and beta waves. The instrumentation amplifier provides a gain of about 89 and the potentiometer implemented at the final op amp allows for additional gain of between 83 and 455. Depending on the person, this means that the resulting waveform will most likely have an amplitude of slightly under 1V, a very reasonable voltage to measure.

![schematic](https://github.com/merlin-neurotech/Hardware-Team/blob/master/EEGSchematic.png)

