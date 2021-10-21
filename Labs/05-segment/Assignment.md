# Lab 5: Unai Telletxea

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/UTAN25/Digital-electronics-2](https://github.com/UTAN25/Digital-electronics-2)


### 7-segment library

1. In your words, describe the difference between Common Cathode and Common Anode 7-segment display.
   * CC SSD: All catodes have to be conected to the same GND, so to switch any part ON we must apply voltage to the pin. Active High.
   * CA SSD: All anodes have to be conected to the same power source, so to switch any part ON we must NOT apply voltage to the pin. Active Low.

2. Code listing with syntax highlighting of two interrupt service routines (`TIMER0_OVF_vect`, `TIMER0_OVF_vect`) from counter application with at least two digits, ie. values from 00 to 59:

```c
/**********************************************************************
 * Function: Timer/Counter1 overflow interrupt
 * Purpose:  Increment counter value from 00 to 59.
 **********************************************************************/
ISR(TIMER1_OVF_vect)
{
    
    if (counter1==9) //Add 1  to the first digit at the start of the 10th cicle
    
       counter1=0;   //Last digit
       counter2++;   //First digit
        
    else
    
       counter1++;
    
    if (counter2==6) //Replace number 60 with 00
      counter2=0;
      counter1=0;

}
```

```c
/**********************************************************************
 * Function: Timer/Counter0 overflow interrupt
 * Purpose:  Display tens and units of a counter at SSD.
 **********************************************************************/
ISR(TIMER0_OVF_vect)
{
    static uint8_t pos = 0;
    if (pos)   //flip between the 2 display position every loop
    
        SEG_update_shift_regs(counter2,1);   //Display the first digit
        pos=0;
        
    else
    
        SEG_update_shift_regs(counter1,0);   //Display the last digit
        pos=1;

}
```

3. Flowchart figure for function `SEG_clk_2us()` which generates one clock period on `SEG_CLK` pin with a duration of 2&nbsp;us. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![your figure]()


### Kitchen alarm

Consider a kitchen alarm with a 7-segment display, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

1. Scheme of kitchen alarm; do not forget the supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure]()
