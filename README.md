# Lab_3_Early_Debouncer
Since mechanical inputs are not perfect, bouncing of the input signal can occur. This unstable input can create issues if not accounted for, thus, a debouncer can be implemented to deal with bouncing inputs. In this lab, we develop an early debouncer circuit to ensure the stability of our inputs for at least 20ms.

[Lab 3 Files](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/tree/main/Lab3Files)

## Early Debouncer
![Early Detection Debouncer State Diagram](https://github.com/Fall-2023-Classes/lab-2-square-wave-generator/assets/112601782/96e25a3b-244e-462a-a34b-0094f033d6bc)
![Early Detection Debouncer ASM Chart](https://github.com/Fall-2023-Classes/lab-2-square-wave-generator/assets/112601782/89f85d5f-a5cb-4d2f-91ff-f788fd509b99)

Our [Early Debouncer](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/early_debouncer.sv) Circuit is a moore finite state machine with 8 total states. The inputs to be read in our FSM are the *sw* and the *m_tick* which can be seen in both the State Diagram/ASM Chart and the early_debouncer module. In an early debouncer, the very first edge of the input that is detected is held for a minimum of 20ms before checking the input again. This ensures that our input signal is stable for at least 20ms, preventing potential errors that come from an unstable, bouncing input. To obtain a stable signal for at least 20ms, we use three basic [modulus counters](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/mod_counter.sv) that generates a *max_tick* (*m_tick*) at exactly 10ms each. Since a counter/timer uses a clock, it is always running and always ticking 24/7, meaning our *sw* input can occur at any time between the 0ms-10ms tick rate. Therefore, three modulus counters are used to ensure a stable signal for a minimum of 20ms and a maximum of 30ms.
  - [early_debouncer module file](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/early_debouncer.sv)
    - [early_debouncer Test Bench Simulation File](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/SimulationFiles/early_debouncer_TB.sv)
  - [modulus_counter file](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/mod_counter.sv)

    
## Test Circuit
![image](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/assets/112601782/e2d461f6-a24d-457c-bb46-be4bad8568b8)

To test our [early debouncer](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/early_debouncer.sv), we can implement the test circuit shown above that will count the number of button presses and display it on two sets of [seven segment displays](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/seven_seg.sv). To visualize the bouncing input and the debounced input, we count two different button inputs - one of them will be debounced and the other will be the raw input signal with no debouncer. As you would expect, the debounced counter will accurately count the amount of button presses, while the non-debounced counter may count multiple times for a single press.

- [Top Module](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/top.sv)
- [Early Debouncer](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/early_debouncer.sv)
- [Rising Edge Detector](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/rising_edge_detect_mealy.sv)
- [Binary Counter (BCD)](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/binary_counter_bcd.sv)
- [Display module](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/display.sv)
  - [Seven Segment Decoder](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/seven_seg.sv)
  - [Seven Segment Digit Controller](https://github.com/Fall-2023-Classes/lab_3_early_debouncer/blob/main/Lab3Files/DesignFiles/seven_seg_control.sv)

