# vhdl_abs
A finite state machine implementation of an ABS system written in VHDL with PSL statements.

The following is a realization of a finite state machine that tries to represent an ABS system that is present in many vehicles. 
It has been supposed that:
1) this system is an electronic sub-system controlled by an ECU;
2) this system oprates with digital logic;
3) this system will get as inputs the following:
	
	3.1)	Clock pulse and reset (CLK,RES);
	
	3.2)	Data regarding front brake pressure (FBP, front brake pressure) and rear brake pressure (RBP, rear brake pressure) which are collected by the
			respective sensors;
	
	3.3) 	Data regarding angular velocity of each tire:
	
		FRS, front-rear speed,
		FLS, front-left speed, 
		RRS, rear-right speed,
		RLS, rear-left speed;

	3.4)	Speed of the vehicle (SPD, speed).

4) this system has as output the state codes of front and rear chassis (ABS_STATUS_F,ABS_STATUS_R), as such:
	
		Output: (ABS_STATUS_F,ABS_STATUS_R)
		IDLE : (0000,0000)
		FBMS (front brakes monitoring state) : (0001,----)
		RBMS (rear brakes monitoring state) : (----,1110)
		FFLS (full front lock state) : (0010,----)	
		FRLS (full rear lock state) : (----,1101)
		FRWSS (front-right wheel spinning state) : (0011,----)
		FLWSS (front-left wheel spinning state) : (1100,----)
		RRWSS (rear-right wheel spinning state) : (----,0100)
		RLWSS (rear-left wheel spinning state) : (----,1011)
		ERRS (error state) : (0101,0101)
		FULL_LOCK (4 tires full lock state) : (1111,1111)
	

5) this system is affected by a technologic delay of 30 ps;
6) the %%WSS (wheel spinning states) are to be used only if a tire spins 80% faster than the otherone in the same chassis and if the vehicle is moving faster than 50 Km/h;
7) this system has the vehicle speed coded through a 4 bit vector (+1 =+10 Km/h, from 0 Km/h (0000) to a maximum of 150 Km/h (1111);
8) this system has a pressure threshold, the passing of which implies the activation of the full lock states.


This code has complimentary PSL statements that monitor the transitions of some states of this finite machine.

--Vrantamar
