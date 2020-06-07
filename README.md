# C-library with floating point P, PI, PD, PID-controllers implementation

* This embedded C-library provides the various types of P/I/D-controllers:
	* Proportional (P) controller
  *	Proportional–integral (PI) controller
  * Proportional–derivative (PD) controller
  *	Proportional–integral–derivative (PID) controller
 
* Project structure
  * README.md - current file
  * LICENSE - file with license description
  * fp_pid.h - C-header file with user data types and function prototypes
  * fp_pid.c - C-source file with firmware functions

* [More about P/I/D-controllers here.](https://en.wikipedia.org/wiki/PID_controller)

# HowToUse (example)

		#include "fp_pid.h"
		
		// updatable user variables:
		float MyInValue, MyOutValue;
		
		// 1st step: create and initialize the global variable of user data structure
		tPI sPI = PI_DEFAULTS;
		
		// 2nd step: do some settings
		sPI.fDtSec = 0.0001f;     // set the discretization (sapmle) time
		sPI.fKp = 0.1f;           // set the proportional coefficient
		sPI.fKi = 0.01f;          // set the integral coefficient
		sPI.fUpOutLim = 140.0f;   // set the PI-controller's output upper limit
		sPI.fLowOutLim = -140.0f; // set the PI-controller's output lower limit
		
		// 3rd step: Next code must be executed every time with sPI.fDtSec period if a 
		// new calculation of PI-controller's output is needed
		sPI.fIn = MyIn;           // set the new value of PI-controller's input
		sPI.m_calc(&sPI);         // call the PI-controller's output calculation function
		MyOutValue = sPI.fOut;    // update MyOutValue variable
		
		// call this function in case only when you need to reset the PI-controller's internal variables
		sPI.m_rst(&sPI);

# License
  
[MIT](./LICENSE "License Description") 
