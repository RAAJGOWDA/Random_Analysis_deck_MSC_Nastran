# Random_Analysis_deck_MSC_Nastran #Acceleration Set3
RESTART VERSION=1 KEEP
ASSIGN MASTER='enter yor file name here_sol103_freq_2000hz.MASTER'
$
SOL 111
CEND
$
ECHO=NONE
include 'include\enter the random set file bdf with acceleration input name here_set_elm_random.bdf'
Set 3 = 500001
$
SPC =       1
METHOD =    91
RANDOM = 96
STRESS(PLOT,REAL,PSDF,NORPRINT) = 1
ACCELERATION(plot,rprint, psdf)=3
FREQUENCY =       92
SDAMPING(STRUCTURE) =     1001
$
SUBCASE       1
  LABEL= FWD(-X)
  DLOAD =       93
$2345678$2345678$2345678$2345678$2345678$2345678$2345678$2345678$2345678
BEGIN BULK
PARAM,          RESVEC,                YES
PARAM,         ENFMETH,             REL
PARAM,         ENFMOTN,             REL
PARAM,         OUGCORD,          GLOBAL
$
PARAM,COUPMASS,1       
PARAM,GRDPNT,0       
PARAM,K6ROT,100.0   
PARAM,MAXRATIO,1.0+8   
PARAM,POST,-1      
PARAM,SNORM,20.0    
$  
include 'include\enter your entire fem bdf name here.bdf'
$
RANDPS        96       1       1     1.0     0.0    1003
SPC            1  500001  123456     0.0
EIGRL         91     0.0  2000.0                                    MASS
$
FREQ1         92    20.0     2.0      40
$FREQ1         92   100.0    10.0     100
$FREQ1         92  1100.0    30.0      30
$
FREQ,92,20.0,80.0,350.0,2000.0 
FREQ2         92     1.0  2000.0     50
FREQ4         92     1.0  2000.0     0.1       3
$
TABDMP1     1001    CRIT        
+            0.0    0.02  2000.0    0.02ENDT    
$
DLOAD         93     1.0     1.0      94
RLOAD2        94      95                    1002            ACCE
SPCD          95  500001       1    -1.0
$
TABLED1     1002  LINEAR  LINEAR
+            0.0     0.0     1.0  9810.0  2000.0  9810.0ENDT    
TABRND1     1003     LOG     LOG
+           20.0    0.01    80.0    0.04   350.0    0.04  2000.0   0.008
+         2000.1   0.008ENDT
ENDDATA
