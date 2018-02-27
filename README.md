# MSK Encoder Readme

Current version v1.6
- Will decode a 48 kHz sampled audio signal with carrier frequency of 10 kHz.
- Currently only works with 10 kHz carrier wave, trying to debug issues with using other frequencies
- Frequency recovery loop not yet finished so 10 kHz carrier frequency hard coded in
- Lots of additional variables and files that are created to output different stages in modulation/demodulation for debugging
- Have been working with 480 kHz in the file just to make the signals more smooth for visualisation during development

#####
To run
#####
Encoding:
1. Ensure there is a file 'binary.txt' that contains the bits stream you want to encode
2. Run msk_encoder_v1.6
3. When prompted, select option '1. msk encode'

Decoding
1. Ensure there is a file 'msk_encoded_message.txt' that contains the msk encoded message
2. Run msk_encoder_v1.6
3. When prompted, select option '2. msk decode'



#####
Contains 2 main functions:
#####
All inputs have defaults that are stated at the beginning of the document
Only file that must be ready is the binary input file, default filename is "binary.txt"

1. msk_encode
Generates an output file with and amplitude list of the modulated MSK message


Inputs 			- carrier amplitude
       			- carrier frequency
       			- bit rate
       			- sample rate
			- message filepath (binary file to input to modulator)

Outputs 		- 0

Generated files 	- msk_encoded_message.txt 	(list of amplitudes of msk modulated signal)
			***ALL FILES BELOW WILL NOT BE OUTPUT IN FINAL VERSION***
			- mibits.txt 			(NRZ values of I arm bits)
			- mqbits.txt			(NRZ values of Q arm bits)
			- mibits_msk.txt		(I arm bits represented as sinusoids)
			- mqbits_msk.txt		(Q arm bits represented as sinusoids)
			- miarm.txt			(modulated I arm signal)
			- mqarm.txt			(modulated Q arm singal)



2. msk_decode
Demodulates MSK message from a file with list of amplitudes such as that generated by msk_encode

Inputs 			- sample rate
			- bit rate
			- encoded file path
			- sync key
			- butterworth filter order
			- butterworth filter cutoff frequency

Outputs 		- 0

Generated files 	- msk_demodulated_message.bin 	(output file containing binary data from modulated signal)
			- mdi1.txt			)
			- mdq1.txt			)
			- mdi2.txt			)
			- mdq2.txt			)
			- mdi3.txt			) all of these files store the signal amplitudes at different stages during demodulation for visualisation during development
			- mdq3.txt			) if you want I can include a diagram showing at what points in demodulation these files correspond to
			- mdi4.txt			)
			- mdq4.txt			)
			- mdibits.txt			)
			- mdqbits.txt			)


#####
Other functions - these won't be included in the final product
#####

3. generate_timer_file
Generates a timer file to give an x axis to plot the signal at any stage in modulation/demodulation against'

Inputs 			- start 			(starting x axis value, default 0)
			- sample rate
			- encoded message

Outputs 		- 0

Generated files 	- timer.txt 			(list of time samples)



4. sanity_checks
Checks that default values make sense

Inputs 			- none

Outputs 		- 0 if default variables are ok
			- 1 if default variables are not ok

Generated files 	- none



5. count_lines
Counts lines in a file

Inputs 			- file

Outputs 		- line count

Generated files 	- none

 
 
# Frequency Recovery Loop Readme

Current version vC.4.3
- does not work
- currently working on outputting quantifiable error from the costas_loop() function 
- produces extra files that will not be in final product for visualisation during development

#####
2 Main Functions
#####


1. frequency_finder

Inputs 				- VCO_start 		(starting gues for carrier frequency)
				- encoded_message 	(msk modulated message file)
				- sample rate

Outputs 			- VCO_f 		(carrier frequency)

Generated files 		- none



2. costas_loop

Inputs 				- VCO_f 		(guess for carrier frequency)
				- filt1a
				- filt1b
				- filt2a
				- filt2b
				- sample_rate
				- max_samples 		(amount of samples to inlcude when finding freqency)
				- bit period

Outputs 			- VCO_f 		(guess for carrier frequency that was input)
				- f_err 		(error)

Generated files 		- frvC_A1.txt		)
    				- frvC_B1.txt		)
    				- frvC_C1.txt		)
    				- frvC_A2.txt		)
    				- frvC_B2.txt		)
    				- frvC_A3.txt		) - files to visualise the signal at different points during frequency recovery
    				- frvC_B3.txt		)
    				- frvC_C2.txt		)
    				- frvC_C3.txt		)
    				- frvC_C4.txt		)
    				- frvC_timer.txt	)

