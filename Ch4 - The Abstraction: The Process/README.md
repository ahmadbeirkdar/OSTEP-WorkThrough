1. Should use 100% of the CPU as there is no waiting for an IO operation to complete
2. IO length takes 5, if not set. So it is 4(P0) + 5(P1 IO) = 9. Therefore 9 CPU cycles
3. 
Time     PID: 0     PID: 1        CPU        IOs 
  1      RUN:io      READY          1            
  2     WAITING    RUN:cpu          1          1 
  3     WAITING    RUN:cpu          1          1 
  4     WAITING    RUN:cpu          1          1 
  5     WAITING    RUN:cpu          1          1 
  6*       DONE       DONE       

It takes 5 cpu cycles as P1 runs while P0 is waiting for IO to complete
4. It will take 5(P0 IO) + 4(P1) = 9 CPU cycles as P1 does not run while P0 is waiting for IO
5. Same thing as Q3, because it allows the P1 to run when P0 is waiting for IO
6. No they are not, P0 is runs the first IO then waits for other process to finish till P0 runs its remaining IOs
                ahmadbeirkdar@Ahmads-iMac Ch4 - The Abstraction: The Process % python process-run.py -l 3:0,5:100,5:100,5:100 -S SWITCH_ON_IO -I IO_RUN_LATER -c -p
                Time     PID: 0     PID: 1     PID: 2     PID: 3        CPU        IOs 
                1      RUN:io      READY      READY      READY          1            
                2     WAITING    RUN:cpu      READY      READY          1          1 
                3     WAITING    RUN:cpu      READY      READY          1          1 
                4     WAITING    RUN:cpu      READY      READY          1          1 
                5     WAITING    RUN:cpu      READY      READY          1          1 
                6*      READY    RUN:cpu      READY      READY          1            
                7       READY       DONE    RUN:cpu      READY          1            
                8       READY       DONE    RUN:cpu      READY          1            
                9       READY       DONE    RUN:cpu      READY          1            
                10       READY       DONE    RUN:cpu      READY          1            
                11       READY       DONE    RUN:cpu      READY          1            
                12       READY       DONE       DONE    RUN:cpu          1            
                13       READY       DONE       DONE    RUN:cpu          1            
                14       READY       DONE       DONE    RUN:cpu          1            
                15       READY       DONE       DONE    RUN:cpu          1            
                16       READY       DONE       DONE    RUN:cpu          1            
                17      RUN:io       DONE       DONE       DONE          1            
                18     WAITING       DONE       DONE       DONE                     1 
                19     WAITING       DONE       DONE       DONE                     1 
                20     WAITING       DONE       DONE       DONE                     1 
                21     WAITING       DONE       DONE       DONE                     1 
                22*     RUN:io       DONE       DONE       DONE          1            
                23     WAITING       DONE       DONE       DONE                     1 
                24     WAITING       DONE       DONE       DONE                     1 
                25     WAITING       DONE       DONE       DONE                     1 
                26     WAITING       DONE       DONE       DONE                     1 
                27*       DONE       DONE       DONE       DONE                       

7. Yes, P0 now runs its IOs after the one before is done. This allows P1 P2 and P3 to run while P0 is waiting for IO
                ahmadbeirkdar@Ahmads-iMac Ch4 - The Abstraction: The Process % python process-run.py -l 3:0,5:100,5:100,5:100 -S SWITCH_ON_IO -I IO_RUN_IMMEDIATE -c -p
                Time     PID: 0     PID: 1     PID: 2     PID: 3        CPU        IOs 
                1      RUN:io      READY      READY      READY          1            
                2     WAITING    RUN:cpu      READY      READY          1          1 
                3     WAITING    RUN:cpu      READY      READY          1          1 
                4     WAITING    RUN:cpu      READY      READY          1          1 
                5     WAITING    RUN:cpu      READY      READY          1          1 
                6*     RUN:io      READY      READY      READY          1            
                7     WAITING    RUN:cpu      READY      READY          1          1 
                8     WAITING       DONE    RUN:cpu      READY          1          1 
                9     WAITING       DONE    RUN:cpu      READY          1          1 
                10     WAITING       DONE    RUN:cpu      READY          1          1 
                11*     RUN:io       DONE      READY      READY          1            
                12     WAITING       DONE    RUN:cpu      READY          1          1 
                13     WAITING       DONE    RUN:cpu      READY          1          1 
                14     WAITING       DONE       DONE    RUN:cpu          1          1 
                15     WAITING       DONE       DONE    RUN:cpu          1          1 
                16*       DONE       DONE       DONE    RUN:cpu          1            
                17        DONE       DONE       DONE    RUN:cpu          1            
                18        DONE       DONE       DONE    RUN:cpu          1       