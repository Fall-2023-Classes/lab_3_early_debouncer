# Lab_3_Early_Debouncer
Since mechanical inputs are not perfect, bouncing of the input signal can occur. This unstable input can create issues if not accounted for, thus, a debouncer can be implemented to deal with bouncing inputs. In this lab, we develop an early debouncer circuit to ensure the stability of our inputs for at least 20ms.

[Lab 3 Files]()

## Early Debouncer
![Early Detection Debouncer State Diagram](https://github.com/Fall-2023-Classes/lab-2-square-wave-generator/assets/112601782/96e25a3b-244e-462a-a34b-0094f033d6bc)
![Early Detection Debouncer ASM Chart](https://github.com/Fall-2023-Classes/lab-2-square-wave-generator/assets/112601782/89f85d5f-a5cb-4d2f-91ff-f788fd509b99)
Our [Early Debouncer]() Circuit is a moore finite state machine with 8 total states. The inputs to be read in our FSM are the *sw* and the *m_tick* which can be seen in both the State Diagram/ASM Chart and the [early_debouncer module](). In an early debouncer, the very first edge of the input that is detected is held for a minimum of 20ms before checking the input again. This ensures that our input signal is stable for at least 20ms, preventing potential errors that come from an unstable, bouncing input. To obtain a stable signal for at least 20ms, we use three basic [modulus counters]() that generates a *max_tick* (*m_tick*) at exactly 10ms each. Since a counter/timer uses a clock, it is always running and always ticking 24/7, meaning our *sw* input can occur at any time between the 0ms-10ms tick rate. Therefore, three [modulus counters]() are used to ensure a stable signal for a minimum of 20ms and a maximum of 30ms.
  - [early_debouncer module file]()
    - [early_debouncer Test Bench Simulation File]()
  - [modulus_counter file]()

    
## Test Circuit

To test our [early debouncer](), we can implement a [test circuit]() that will count the amount of button presses and display it on two sets of [seven segment displays](). To visualize the bouncing input and the debounced input, we count two different button inputs - one of them will be debounced and the other will be the raw input signal with no debouncer. As you would expect, the debounced counter will accurately count the amount of button presses, while the non-debounced counter may count multiple times for a single press.

- [Top Module]()
- [Early Debouncer]()
- [Rising Edge Detector]()
- [Binary Counter (BCD)]()
- [Display module]()
  - [Seven Segment Decoder]()
  - [Seven Segment Digit Controller]()

