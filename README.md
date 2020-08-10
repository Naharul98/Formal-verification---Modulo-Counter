# Formal-verification---Modulo-Counter
**A modulo counter model implemented in GCLang along with a set of properties to formally verify correctness of the model**

> Model for modulo counter 8 and 16 is implemented in the files ModuloModel8.gc and ModuloModel16.gc respectively

The model developed follows representation of numbers in the modulo counter as binary, with each bit having a boolean value of either true (represented by 1) or false (represented by 0). For the modulo 8 counter model, I have used 3 bits - as 2^3 = 8. Which means a maximum of 8 unique numbers can be represented in 3 bits, which is enough for counter modulo 8. However, for modulo 16 counter, I had to use 1 extra bit to accomodate all the values in the counter.

### Properties for the model to verify its correctness of modulo 8 model
- In all paths of computation, it should always hold that if we are in state 111 (7 in decimal), then the next state, in all possible paths should be 000 (0 in decimal). If the counter is at state 111, which represents 7 in binary, it should reset back to 0 as it is a modulo counter of 8.
    - **Property: AG((bit0 & bit1 & bit2) -> AX(!bit0 & !bit1 & !bit2))**
- For every reachable state, for all paths starting at that state we must eventually reach another state where it is 0 or 1 or 2 or 3 or 4 or 5 or 6 or 7. No matter which state counter is in, we must continuously hit all of 0,1,2,3,4,5,6,7 eventually. In addition, the only cycle in kripke structure is 0,1,2,3,4,5,6,7,0. There isn’t a second cycle as if there is, the model will fail due to properties 2-10.
    - **Property: AG(AF(!bit0 & !bit1 & !bit2))**
    - **Property: AG(AF(bit0 & !bit1 & !bit2))**
    - **Property: AG(AF(!bit0 & bit1 & !bit2))**
    - **Property: AG(AF(bit0 & bit1 & !bit2))**
    - **Property: AG(AF(!bit0 & !bit1 & bit2))**
    - **Property: AG(AF(bit0 & !bit1 & bit2))**
    - **Property: AG(AF(!bit0 & bit1 & bit2))**
    - **Property: AG(AF(bit0 & bit1 & bit2))**
- Initial state is 000 (0 in decimal).
    - **Property: !bit0 & !bit1 & !bit2**

