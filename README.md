# sched_for_android  
query sched policy for all android task  
  
sched_for_android.sh  
***************************************************************  
   Author: duguowei  
   Date: 2022-8-8  
   Email: duguoweisz@gmail.com  
   Phone: 13417431640  
   WeChat: dgw_cn  
   Kernel: 5.10.66  
   Android: 12  
***************************************************************  
Brief Description:  
 
Query the scheduling attributes (policy and RT (static) priority) of  
all threads currently alive on the system. Just a simple wrapper around  
chrt(1).  
  
adb root  
adb push sched_for_android.sh /data/local/tmp/  
adb shell chmod 755 /data/local/tmp/sched_for_android.sh  
adb shell /data/local/tmp/sched_for_android.sh  
  
  
print like below:  
duguowei@duguowei-HP-ProDesk-680-G4-MT:~$ adb shell /data/local/tmp/sched_for_android.sh  
  PID       TID            Name                     Sched Policy  Prio    *RT  
     1       1                              init    SCHED_OTHER|SCHED_RESET_ON_FORK    0  
     1     333                              init    SCHED_OTHER|SCHED_RESET_ON_FORK    0  
     1     334                              init    SCHED_OTHER|SCHED_RESET_ON_FORK    0  
     1     335                              init    SCHED_OTHER|SCHED_RESET_ON_FORK    0  
     2       2                          kthreadd    SCHED_OTHER    0  
     3       3                            rcu_gp    SCHED_OTHER    0  
     4       4                        rcu_par_gp    SCHED_OTHER    0  
     8       8                      mm_percpu_wq    SCHED_OTHER    0  
    10      10                   rcu_tasks_kthre    SCHED_OTHER    0  
    11      11                   rcu_tasks_trace    SCHED_OTHER    0  
    12      12                       ksoftirqd/0    SCHED_OTHER    0  
    13      13                       rcu_preempt    SCHED_OTHER    0  
    14      14                       migration/0     SCHED_FIFO   99     ***  
    15      15                           cpuhp/0    SCHED_OTHER    0  
    16      16                           cpuhp/1    SCHED_OTHER    0  
    17      17                       migration/1     SCHED_FIFO   99     ***  
    18      18                       ksoftirqd/1    SCHED_OTHER    0  
    20      20              kworker/1:0H-kblockd    SCHED_OTHER    0  
    21      21                           cpuhp/2    SCHED_OTHER    0  
    22      22                       migration/2     SCHED_FIFO   99     ***  
    23      23                       ksoftirqd/2    SCHED_OTHER    0  
    25      25              kworker/2:0H-kblockd    SCHED_OTHER    0  
    26      26                           cpuhp/3    SCHED_OTHER    0  
    27      27                       migration/3     SCHED_FIFO   99     ***  
    28      28                       ksoftirqd/3    SCHED_OTHER    0  
    31      31                           cpuhp/4    SCHED_OTHER    0  
    32      32                       migration/4     SCHED_FIFO   99     ***  
    33      33                       ksoftirqd/4    SCHED_OTHER    0  
    36      36                           cpuhp/5    SCHED_OTHER    0  
    37      37                       migration/5     SCHED_FIFO   99     ***  
    38      38                       ksoftirqd/5    SCHED_OTHER    0  
    40      40              kworker/5:0H-kblockd    SCHED_OTHER    0  
    41      41                           cpuhp/6    SCHED_OTHER    0  
    42      42                       migration/6     SCHED_FIFO   99     ***  
    43      43                       ksoftirqd/6    SCHED_OTHER    0  
    46      46                           cpuhp/7    SCHED_OTHER    0  
    47      47                       migration/7     SCHED_FIFO   99     ***  
    48      48                       ksoftirqd/7    SCHED_OTHER    0  
    50      50              kworker/7:0H-kblockd    SCHED_OTHER    0  
    51      51                             netns    SCHED_OTHER    0  
    60      60                           kauditd    SCHED_OTHER    0  
    61      61                        khungtaskd    SCHED_OTHER    0  
    62      62                        oom_reaper    SCHED_OTHER    0  
    63      63                         writeback    SCHED_OTHER    0  
    64      64                        kcompactd0    SCHED_OTHER    0  
   106     106                           kblockd    SCHED_OTHER    0  
   107     107                    blkcg_punt_bio    SCHED_OTHER    0  
   108     108                       edac-poller    SCHED_OTHER    0  
   109     109                        devfreq_wq    SCHED_OTHER    0  
   110     110                         watchdogd     SCHED_FIFO   50     *  
   132     132                           kswapd0    SCHED_OTHER    0  
   135     135                   dmabuf-deferred    SCHED_OTHER    0  
   136     136                               uas    SCHED_OTHER    0  
   137     137                    dm_bufio_cache    SCHED_OTHER    0  
   138     138                     ipv6_addrconf    SCHED_OTHER    0  
   139     139                          krfcommd    SCHED_OTHER    0  
   148     148                            mt-wdk    SCHED_OTHER    0  
   149     149                            wdtk-0     SCHED_FIFO   99     ***  
 ...


Manual Test:  
matisse:/ # chrt  -p 168  

pid 168's current scheduling policy: SCHED_FIFO  
pid 168's current scheduling priority: 50  
matisse:/ # ps -eT | grep 168 | grep irq  
root           168   168     2       0      0 irq_wait_for_interrupt 0 S irq/522-event_3  

