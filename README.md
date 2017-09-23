# uart_dbg_if
A UART to AHB master bridge for debug usage

Protocol
========

Uart parameter: Odd parity, baudrate must lower than Fsys/16.

System Status:

0 - DBGIDLE (Waiting for handshake, for handshake, you have to use 0x55 for baudrate synchronize)

1 - DBGPREHS (Once it recieved baudrate synchronization signal, it must reply you a character '', you have to send '' to debug if.)

2 - DBGREQGNT [Optional] (Once the pre-handshake stage is completed, the debug i/f must tell host status of this debug i/f, if it requires permission, host have to send a key to i/f).

3 - DBGESTABLISHED (In this situation, the debug i/f can write or read any data from the bus matrix).

If parity error occured, the executing command will be cancel. If it continously occured for three times, the interface will fall to DBGIDLE state.


Commands
=========

Write data to memory.

Read data from memory.

Exit debug mode.

System reset.
