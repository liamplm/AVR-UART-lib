# Easy-AVR-USART-C-Library
An interrupt-driven USART (RS232) library for AVR microcontrollers, with support for multiple UARTs, using ring
buffers for receive/transmit. Designed to be easy to use, especially like arduino libraries (with less overload).

# Features
- easy to use
- support for up to 4 USART's
- extremly light interrupts (50/52 cycles for tx/rx in worst case)
- RS 485 compatibility
- printf()/scanf() streams compatibility
- partial V-USB compatibility (25 cycle ISR restriction (TX is broken at the moment))
- optimized as much as possible to reduce code size
- and much more

simple "hello world" code gives

		   text	   data	    bss	    dec	    hex	filename
		    404	     14	     68	    486	    1e6	avrt.elf

Program Memory Usage 	:	418 bytes   1,3 % Full
Data Memory Usage 		:	82 bytes   4,0 % Full

defined  NO_USART_RX flag gives

		   text	   data	    bss	    dec	    hex	filename
		    340	     14	     34	    388	    184	avrt.elf

Program Memory Usage 	:	354 bytes   1,1 % Full
Data Memory Usage 		:	48 bytes   2,3 % Full

Meanwhile Arduino generates 2KB of code.

For this result additional flag -mrelax is required in many IDE's (eg. Atmel studio 6.2)

# Notes
Lot of terminals sends only CR character as a newline terminator, instead of CRLF or even unix style LF
(BTW PuTTY doesn't allow to change this) but in return requires CRLF terminator to show not broken text.
This behaviour can be covered by RX_NEWLINE_MODE macro, by default set to CRLF.

- 0 - CR
- 1 - LF
- 2 - CRLF (default)

In case of reinitializing uart on the fly with non-constant ubbr try to use uart_reint() or define USART_USING_BOOTLOADER macro.
