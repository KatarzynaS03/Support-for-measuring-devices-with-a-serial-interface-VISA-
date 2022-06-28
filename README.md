# Support-for-measuring-devices-with-a-serial-interface-VISA-
Getting to know the methods of operating devices equipped with a serial interface. For the implementation of the project, a multimeter with a serial interface compliant with the RS232 standard will be used. The project converted the measurements of resistance to temperature conversion for PT100 and KTY81-210

Assumptions:
- Communication with a multimeter
  - The program is to implement two-way communication with the multimeter via an interface
serial and VISA function
  - Communication is to be properly initialized after the program is started and completed before
stopping the program
  - Communication errors are to be signaled on the user panel (timeout)
  - The program is to support all ranges of resistance measurement available in the multimeter
  - Out of range result is to be signaled on the panel and it is not to cause reporting an error in the program
  - The received resistance measurement result is to be converted into a value expressed in Ohms (Double type)
- Converting resistance measurement results (made as SubVI):
  - The device is to perform the function of converting resistance to temperature for PT100 and KTY81-210
    - For PT100 use for selected factors and the dependencies (only for T> 0 ° C, where r is the measured resistance value):
    - For KTY81-210:
Perform curve fitting to typical resistance values ​​for temperatures ranging from -50 to
50 ° C (use the table in the catalog note and the spreadsheet or function
matches available in LabView). Enter the determined curve equation into the program and
be used to convert resistance to temperature
  - The converter of the resistance value to temperature is to be made in the form of a SubVI module
    - Inputs:
      - resistance (DBL type)
      - sensor type (U8 type), 0 → Pt100, 1 → KTY81
      - precision of the conversion result (U8 type) - rounding made in the SubVI diagram
      - temperature scale (BOOL type): true - Celsius, false - Fahrenheit
    - outputs:
      - temperature (DBL type) - determined according to the rules described in point 2a and rounded in accordance with input parameter specifying the precision
      - incorrect conversion (BOOL type) - signaled when the result for PT100 is lower than 0 ° C and for KTY81 when the result is less than -50 ° C or greater than 50 ° C
- Virtual device support
  - Enable the control of all input parameters of the converter (except for resistance)
  - Presentation of the results:
    - The operator can choose whether the program is to present the resistance value read from the multimeter or calculated temperature (the result unit should change)
    - The most recent result is to be displayed in the reading field
    - The history of the last 100 results is to be presented in a chart
    - The description of the graph axis should correspond to the current operating mode - temperature or resistance
    - The graph is cleared after changing the mode
  - If the temperature is displayed and the converter returned an error, the result is not visible in the results history
  - Signal incorrect conversion with the LED object (signaling independent of communication error)
  - The frequency of data reading and conversion is to be adjusted in the range from 500ms to 10s
  - After the program is started, the default setting values ​​are assumed
  - The panel is organized in a legible and ergonomic way
