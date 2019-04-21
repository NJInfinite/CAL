<!--
Contains operations to manage the runtime of the CPU.

SETCYLE sets the speed of the bus relative to the speed of the CPU.

REGCYCLE determines what happens in a cycle, and controls performance.

LOAD is used to load threads.

UNLOAD is used to unload threads and store them to memory.

TERMINATE is used to terminate threads from memory.
-->

CREATE INTERVAL AS OB (<NUM>)

DEFINE CPU_SPEED
DEFINE CPU_TO_BUS_RATIO
DEFINE BUS_SPEED
DEFINE FAIL_SAFE

OP "SETCYCLE"
  BEGIN
    ? SET CPU_SPEED TO OB (<!CPUFREQ>) IS BIN_1
      TRUE
        **E.g. 2400MHz / 400 = 6. 6 is our scale factor.**
        SET CPU_TO_BUS_RATIO TO COMPUTE(CPU_SPEED / <!CPUBUSRAT>)
      FALSE
        SET FAIL_SAFE TO OB (<NUM>)
        SET FAIL_SAFE TO 1000
        SET INTERVAL TO FAIL_SAFE
  END

OP "REGCYCLE"
  BEGIN
  END

OP "LOAD"
  BEGIN
  END

OP "UNLOAD"
  BEGIN
  END

OP "TERMINATE"
  BEGIN
  END
