# ZIGBEE-PROTOCOL-in-Embedded-C-for-Trasmitter
#include <stdio.h>
#include "LPC17xx.H" 
#include "GLCD.h"
#include "Serial.h"
#define __FI 1 
void ZigbeeMeshTX_Init(void)
{
SER_SendString("+++"); 
SER_SendString("ATNDA00003000\r"); 
SER_SendString("ATGWR\r"); 
SER_SendString("ATNUD00002000\r"); 
SER_SendString("ATGWR\r"); 
SER_SendString("ATNCHF\r"); 
SER_SendString("ATSBD3\r"); 
SER_SendString("ATGWR\r"); 
SER_SendString("ATNPI00001111\r"); 
SER_SendString("ATGWR\r"); 
SER_SendString("ATGEX\r"); 
}
int main (void) {
LPC_SC->PCONP|=(1<<15);
SER_Init(); 
LPC_GPIO0->FIODIR |= 0x007f8000;
ZigbeeMeshTX_Init();
#ifdef __USE_LCD
GLCD_Init(); 
GLCD_Clear(White); 
GLCD_SetBackColor(Blue);
GLCD_SetTextColor(White);
GLCD_DisplayString(0, 0, __FI, " MCB1700 Demo ");
GLCD_DisplayString(1, 0, __FI, " Zigbee Mesh TX ");
GLCD_DisplayString(2, 0, __FI, " www.keil.com ");
GLCD_SetBackColor(White);
GLCD_SetTextColor(Blue);
GLCD_DisplayString(5, 0, __FI, "Tx character:");
GLCD_DisplayString(3, 0, __FI, "Press RESET to ");
GLCD_DisplayString(4, 0, __FI, "TRANSMIT");
#endif
SysTick_Config(SystemCoreClock/100); 
while (1)
{ 
GLCD_DisplayChar(7, 4, __FI,SER_PutChar('G'));
}
}
