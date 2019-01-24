# RTT
> 调试或正常运行时高速打印输出信息

## 更改打印端口号

```C
//
// Send a string to terminal 1 which is used as error out.
//
SEGGER_RTT_SetTerminal(1); // Select terminal 1
SEGGER_RTT_WriteString(0, "ERROR: Buffer overflow");
SEGGER_RTT_SetTerminal(0); // Reset to standard terminal
```

## 打印样式控制

### 颜色

RTT_CTRL_RESET
> Reset the text color and background color.

RTT_CTRL_TEXT_*
> Set the text color to one of the following colors.

- BLACK
- RED
- GREEN
- YELLOW
- BLUE
- MAGENTA
- CYAN
- WHITE (light grey)
- BRIGHT_BLACK (dark grey)
- BRIGHT_RED
- BRIGHT_GREEN
- BRIGHT_YELLOW
- BRIGHT_BLUE
- BRIGHT_MAGENTA
- BRIGHT_CYAN
- BRIGHT_WHITE

RTT_CTRL_BG_*
> Set the background color to one of the following colors.

- BLACK
- RED
- GREEN
- YELLOW
- BLUE
- MAGENTA
- CYAN
- WHITE (light grey)
- BRIGHT_BLACK (dark grey)
- BRIGHT_RED
- BRIGHT_GREEN
- BRIGHT_YELLOW
- BRIGHT_BLUE
- BRIGHT_MAGENTA
- BRIGHT_CYAN
- BRIGHT_WHITE

#### 例子
```C
/*********************************************************************
* SEGGER Microcontroller GmbH *
* Solutions for real time microcontroller applications *
**********************************************************************
* *
* (c) 1995 - 2018 SEGGER Microcontroller GmbH *
* *
* www.segger.com Support: support@segger.com *
* *
**********************************************************************
----------------------------------------------------------------------
File : RTT.c
Purpose : Simple implementation for output via RTT.
It can be used with any IDE.
---------------------------- END-OF-HEADER ---------------------------
*/
#include "SEGGER_RTT.h"
static void _Delay(int period) {
int i = 100000*period;
do { ; } while (i--);
}
int main(void) {
int Cnt = 0;
SEGGER_RTT_WriteString(0, "Hello World from SEGGER!\n");
do {
SEGGER_RTT_printf("%sCounter: %s%d\n",
RTT_CTRL_TEXT_BRIGHT_WHITE,
RTT_CTRL_TEXT_BRIGHT_GREEN,
Cnt);
if (Cnt > 100) {
SEGGER_RTT_TerminalOut(1, RTT_CTRL_TEXT_BRIGHT_RED"Counter overflow!");
Cnt = 0;
}
_Delay(100);
Cnt++;
} while (1);
return 0;
}
/*************************** End of file ****************************/
```
