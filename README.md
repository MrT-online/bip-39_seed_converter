# BIP-39_Seed_Converter
Various converters for encoding BIP-39 seeds in a compact storage form or for decoding.

## Description:
This document describes how to manually convert a BIP-39 SEED phrase into several compact storage formats.

## Encoding a 12 or 24 word seed phrase to a 66 character hex hash.
1. Identify the index (0-2047) of each word in the BIP-39 list.
2. Apply Rule 1: Swap the order of the indexes (Remember each swap. E.g.: "Swap the current index of word 1 with the index of word 7.")
3. Apply Rule 2: Note an index offset for each index in the BIP-39 list. E.g.: "Word 1: Take the index of the word that is 1 rank after the current index."
   So if the original index was 6 then it is 7 after applying rule 1: 6 + 1 = 7.
4. Convert each index thus determined into an 11-digit binary number (with leading zeros).
5. String all binary numbers together.
6. Divide the resulting binary string into 8-bit groups.
7. Convert each 8-bit group to a hexadecimal value.

### Example
Seed:
	abandon
	ability
	able
	about
	above
	absent
	absorb
	abstract
	absurd
	abuse
	access
	accident
	account
	accuse
	achieve
	acid
	acoustic
	acquire
	across
	act
	action
	actor
	actress
	actual

1. Determining the respective index of each word in the BIP-39 list:
	0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23
	
2. Application of Rule 1 (Example):
	Word 1:	Swap the current index of the word 1 with the index of the word 7.
	Word 2:	Swap the current index of the word 2 with the index of the word 23.
	Word 3:	Swap the current index of the word 3 with the index of the word 4.
	Word 4:	Swap the current index of the word 4 with the index of the word 3.	(already applied)
	Word 5:	Swap the current index of the word 5 with the index of the word 22.
	Word 6:	Swap the current index of the word 6 with the index of the word 16.
	Word 7:	Swap the current index of the word 7 with the index of the word 1.	(already applied)
	Word 8:	Swap the current index of the word 8 with the index of the word 20.
	Word 9:	Swap the current index of the word 9 with the index of the word 14.
	Word 10: Swap the current index of the word 10 with the index of the word 12.
	Word 11: Swap the current index of the word 11 with the index of the word 15.
	Word 12: Swap the current index of the word 12 with the index of the word 10.	(already applied)
	Word 13: Swap the current index of the word 13 with the index of the word 17.
	Word 14: Swap the current index of the word 14 with the index of the word 9.	(already applied)
	Word 15: Swap the current index of the word 15 with the index of the word 11.	(already applied)
	Word 16: Swap the current index of the word 16 with the index of the word 6.	(already applied)
	Word 17: Swap the current index of the word 17 with the index of the word 13.	(already applied)
	Word 18: Swap the current index of the word 18 with the index of the word 24.
	Word 19: Swap the current index of the word 19 with the index of the word 21.
	Word 20: Swap the current index of the word 20 with the index of the word 8.	(already applied)
	Word 21: Swap the current index of the word 21 with the index of the word 19.	(already applied)
	Word 22: Swap the current index of the word 22 with the index of the word 5.	(already applied)
	Word 23: Swap the current index of the word 23 with the index of the word 2.	(already applied)
	Word 24: Swap the current index of the word 24 with the index of the word 18.	(already applied)

	=> New order of the index: 6, 22, 3, 2, 21, 15, 0, 19, 13, 11, 14, 9, 16, 8, 10, 5, 12, 23, 20, 7, 18, 4, 1, 17

3. Application of Rule 2 (Example):
	Word 1:	Take the index of the word that is 1 ranks after the current index.
	Word 2:	Take the index of the word that is 2 ranks after the current index.
	Word 3:	Take the index of the word that is 3 ranks after the current index.
	Word 4:	Take the index of the word that is 4 ranks after the current index.
	Word 5:	Take the index of the word that is 5 ranks after the current index.
	Word 6:	Take the index of the word that is 6 ranks after the current index.
	Word 7:	Take the index of the word that is 7 ranks after the current index.
	Word 8:	Take the index of the word that is 8 ranks after the current index.
	Word 9:	Take the index of the word that is 9 ranks after the current index.
	Word 10: Take the index of the word that is 10 ranks after the current index.
	Word 11: Take the index of the word that is 11 ranks after the current index.
	Word 12: Take the index of the word that is 12 ranks after the current index.
	Word 13: Take the index of the word that is 13 ranks after the current index.
	Word 14: Take the index of the word that is 14 ranks after the current index.
	Word 15: Take the index of the word that is 15 ranks after the current index.
	Word 16: Take the index of the word that is 16 ranks after the current index.
	Word 17: Take the index of the word that is 17 ranks after the current index.
	Word 18: Take the index of the word that is 18 ranks after the current index.
	Word 19: Take the index of the word that is 19 ranks after the current index.
	Word 20: Take the index of the word that is 20 ranks after the current index.
	Word 21: Take the index of the word that is 21 ranks after the current index.
	Word 22: Take the index of the word that is 22 ranks after the current index.
	Word 23: Take the index of the word that is 23 ranks after the current index.
	Word 24: Take the index of the word that is 2047 ranks after the current index.

	=> New order of the index: 7, 24, 6, 6, 26, 21, 7, 27, 22, 21, 25, 21, 29, 22, 25, 21, 29, 41, 39, 27, 39, 26, 24, 16
	
4. Convert each decimal number of the index from step 3 into an 11-bit binary number (see BIP-39 list) 
	00000000111
	00000011000
	00000000110
	00000000110
	00000011010
	00000010101
	00000000111
	00000011011
	00000010110
	00000010101
	00000011001
	00000010101
	00000011101
	00000010110
	00000011001
	00000010101
	00000011101
	00000101001
	00000100111
	00000011011
	00000100111
	00000011010
	00000011000
	00000010000

3. Sequence of all 11-bit binary numbers:
000000001110000001100000000000110000000001100000001101000000010101000000001110000001101100000010110000000101010000001100100000010101000000111010000001011000000011001000000101010000001110100000101001000001001110000001101100000100111000000110100000001100000000010000

4. Division of the consecutive 11-bit binary number into 8-bit number groups:
	00000000
	11100000
	01100000
	00000011
	00000000
	01100000
	00110100
	00000101
	01000000
	00111000
	00011011
	00000010
	11000000
	01010100
	00001100
	10000001
	01010000
	00111010
	00000101
	10000000
	11001000
	00010101
	00000011
	10100000
	10100100
	00010011
	10000001
	10110000
	01001110
	00000110
	10000000
	11000000
	00010000
	
	(with a 24 SEED there are 33x 8-bit binary numbers)

5. Converting each 8-bit binary number into a hexadecimal number and concatenating them:
	D2E060030060340540381B02C0540C81503A0580C81503A0A41381B04E0680C010

Congratulation you have determined the 66 characters for your seed phrase!

	
## Decoding a HEX hash into a 12 or 24 word SEED phrase.
1. Convert each hexadecimal value to an 8-bit binary number.
2. String all 8-bit binary numbers together.
3. Divide the binary string into 11-bit groups.
4. Convert each 11-bit group to a decimal number. This is the index of the word in the BIT-39 list.
5. Apply rule 2 in reverse. For example, if the index of the word determined in step 4 has the index 7 and I remembered 1, I now calculate the opposite: 7 - 1 = 6
6. Apply rule 1 only once for each word.
7. Determine the corresponding word in the BIP-39 list for each index.

### Example:
HEX hash: D2E060030060340540381B02C0540C81503A0580C81503A0A41381B04E0680C010

1. Dividing the HEX hash into groups of 2:
	D2
	E0
	60
	03
	00
	60
	34
	05
	40
	38
	1B
	02
	C0
	54
	0C
	81
	50
	3A
	05
	80
	C8
	15
	03
	A0
	A4
	13
	81
	B0
	4E
	06
	80
	C0
	10

2. Converting each group of 2 into an 8-bit binary number:
	00000000
	11100000
	01100000
	00000011
	00000000
	01100000
	00110100
	00000101
	01000000
	00111000
	00011011
	00000010
	11000000
	01010100
	00001100
	10000001
	01010000
	00111010
	00000101
	10000000
	11001000
	00010101
	00000011
	10100000
	10100100
	00010011
	10000001
	10110000
	01001110
	00000110
	10000000
	11000000
	00010000
	
3. Sequence of 8-bit binary numbers:
110100101110000001100000000000110000000001100000001101000000010101000000001110000001101100000010110000000101010000001100100000010101000000111010000001011000000011001000000101010000001110100000101001000001001110000001101100000100111000000110100000001100000000010000

4. Division of the sequence of 8-bit binary numbers into 11-bit binary number groups: 
	00000000111
	00000011000
	00000000110
	00000000110
	00000011010
	00000010101
	00000000111
	00000011011
	00000010110
	00000010101
	00000011001
	00000010101
	00000011101
	00000010110
	00000011001
	00000010101
	00000011101
	00000101001
	00000100111
	00000011011
	00000100111
	00000011010
	00000011000
	00000010000

4. Convert any 11-bit binary number to a decimal number. This is the index of the word in the BIP-39 list:
	7,
	24,
	6,
	6,
	26,
	21,
	7,
	27,
	22,
	21,
	25,
	21,
	29,
	22,
	25,
	21,
	29,
	41,
	39,
	27,
	39,
	26,
	24,
	16

5. Application of Rule 2 in the reverse sense (example):
	Word 1:	Take the index of the word that is 1 ranks before the current index.
	Word 2:	Take the index of the word that is 2 ranks before the current index.
	Word 3:	Take the index of the word that is 3 ranks before the current index.
	Word 4:	Take the index of the word that is 4 ranks before the current index.
	Word 5:	Take the index of the word that is 5 ranks before the current index.
	Word 6:	Take the index of the word that is 6 ranks before the current index.
	Word 7:	Take the index of the word that is 7 ranks before the current index.
	Word 8:	Take the index of the word that is 8 ranks before the current index.
	Word 9:	Take the index of the word that is 9 ranks before the current index.
	Word 10: Take the index of the word that is 10 ranks before the current index.
	Word 11: Take the index of the word that is 11 ranks before the current index.
	Word 12: Take the index of the word that is 12 ranks before the current index.
	Word 13: Take the index of the word that is 13 ranks before the current index.
	Word 14: Take the index of the word that is 14 ranks before the current index.
	Word 15: Take the index of the word that is 15 ranks before the current index.
	Word 16: Take the index of the word that is 16 ranks before the current index.
	Word 17: Take the index of the word that is 17 ranks before the current index.
	Word 18: Take the index of the word that is 18 ranks before the current index.
	Word 19: Take the index of the word that is 19 ranks before the current index.
	Word 20: Take the index of the word that is 20 ranks before the current index.
	Word 21: Take the index of the word that is 21 ranks before the current index.
	Word 22: Take the index of the word that is 22 ranks before the current index.
	Word 23: Take the index of the word that is 23 ranks before the current index.
	Word 24: Take the index of the word that is 2047 ranks before the current index.
	
	=> New order of the index: 6, 22, 3, 2, 21, 15, 0, 19, 13, 11, 14, 9, 16, 8, 10, 5, 12, 23, 20, 7, 18, 4, 1, 17

6. Application of Rule 1 in the reverse sense (example):
	Swap the current index of the word 1 with the index of the word 7.
	Swap the current index of the word 2 with the index of the word 23.
	Swap the current index of the word 3 with the index of the word 4.
	Swap the current index of the word 4 with the index of the word 3.	(already applied)
	Swap the current index of the word 5 with the index of the word 22.
	Swap the current index of the word 6 with the index of the word 16.
	Swap the current index of the word 7 with the index of the word 1.	(already applied)
	Swap the current index of the word 8 with the index of the word 20.
	Swap the current index of the word 9 with the index of the word 14.
	Swap the current index of the word 10 with the index of the word 12.
	Swap the current index of the word 11 with the index of the word 15.
	Swap the current index of the word 12 with the index of the word 10.	(already applied)
	Swap the current index of the word 13 with the index of the word 17.
	Swap the current index of the word 14 with the index of the word 9.	(already applied)
	Swap the current index of the word 15 with the index of the word 11.	(already applied)
	Swap the current index of the word 16 with the index of the word 6.	(already applied)
	Swap the current index of the word 17 with the index of the word 13.	(already applied)
	Swap the current index of the word 18 with the index of the word 24.
	Swap the current index of the word 19 with the index of the word 21.
	Swap the current index of the word 20 with the index of the word 8.	(already applied)
	Swap the current index of the word 21 with the index of the word 19.	(already applied)
	Swap the current index of the word 22 with the index of the word 5.	(already applied)
	Swap the current index of the word 23 with the index of the word 2.	(already applied)
	Swap the current index of the word 24 with the index of the word 18.	(already applied)
	
	=> New order of the index: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23

7. Determination of the words for each index (SEED):
	abandon
	ability
	able
	about
	above
	absent
	absorb
	abstract
	absurd
	abuse
	access
	accident
	account
	accuse
	achieve
	acid
	acoustic
	acquire
	across
	act
	action
	actor
	actress
	actual

Congratulation you have successfully decoded your SEED phrase from your HEX hash!


## Econding a 12 or 24 word SEED phrase into a 44 characters Base64 hash.
	comin soon...

## Decoding a Base64 hash into a 12 or 24 word SEED phrase.
	comin soon...
