Scott Csordas
scsordas 0998149

Testing:
in order to carry out these tests you will need to have 2 terminals open in the directory both running the executable ./lockRanger
PID's may change in the outpts as well as times and other variables the output is just to give an example
my code will pass all tests

Test case 1

The object of this test case is to ensure that the Program can perform an Exclusive lock andget a status using the t command.

in order to run this test type into the first terminal X 0 5 and the program will tell you this:
PID 10904 performing operation Exclusive Lock
PID 10904: requesting Exclusive Lock lock at Tue Dec  1 20:10:46 2020
PID 10904: granted    Exclusive Lock at 0 for 5 bytes at Tue Dec  1 20:10:46

then you can go to the second terminal and run the T 0 5 command expecting this output
PID 10935 performing operation Test for lock
PID 10935: requesting Test for lock lock at Tue Dec  1 20:11:03 2020
Exclusive lock: PID: 10935 length: 5 Offset: 0 Calculated from: 0

lastly test to ensure another exlusive lock can't be starteed by typing X 0 5 into the second terminal. this should be the output
PID 12611 performing operation Exclusive Lock
PID 12611: requesting Exclusive Lock lock at Tue Dec  1 20:15:51 2020

 the command won't finish until you enter U 0 5 into the first terminal expecting this output
 PID 10904 performing operation Unlock
 PID 10904: requesting Unlock lock at Tue Dec  1 20:17:12 2020
 PID 10904: unlocked   Unlock at 0 for 5 bytes at Tue Dec  1 20:17:12 2020

 then the second terminal will finish locking and the program is working properly with the final output in the second output being
 PID 10904: granted    Exclusive Lock at 0 for 5 bytes at Tue Dec  1 20:10:46

 Test case 2

 the object of this test case is to ensure that the program will work for shared locks

 to run this test start by typing S 0 5 into the first terminal the output will be:
 PID 10904 performing operation Shared Lock
 PID 10904: requesting Shared Lock lock at Tue Dec  1 20:22:22 2020
 PID 10904: granted    Shared Lock at 0 for 5 bytes at Tue Dec  1 20:22:22 20

 then in terminal 2 run the command T 0 5 this will show:
 PID 12670 performing operation Test for lock
 PID 12670: requesting Test for lock lock at Tue Dec  1 20:23:34 2020
 Shared lock: PID: 12670 length: 5 Offset: 0 Calculated from: 0

 then in terminal 2 to make sure you can still make another lock try running S 0 5 the lock should be granted:
 PID 12670 performing operation Shared Lock
 PID 12670: requesting Shared Lock lock at Tue Dec  1 20:24:39 2020
 PID 12670: granted    Shared Lock at 0 for 5 bytes at Tue Dec  1 20:24:39 2020

 then check if you can do a exclusive lock in terminal 2 it should wait until the lock in terminal 1 is ended:
 PID 12670 performing operation Exclusive Lock
 PID 12670: requesting Exclusive Lock lock at Tue Dec  1 20:25:57 2020

 use U 0 5 in the first termianl and:
 PID 10904 performing operation Unlock
 PID 10904: requesting Unlock lock at Tue Dec  1 20:26:14 2020
 PID 10904: unlocked   Unlock at 0 for 5 bytes at Tue Dec  1 20:26:14 2020

 terminal 2 will finish the lock:
 PID 12670: granted    Exclusive Lock at 0 for 5 bytes at Tue Dec  1 20:26:14 2020

 this shows the shared locks will work

 these 2 test cases have also shown off the functionality of T(lock test) and U(unlock)
 if you wanted 1 more test for T to see if what happens when no locks exist start the program in a terminal and type T 0 5
 the output will be:
 PID 10904 performing operation Test for lock
 PID 10904: requesting Test for lock lock at Tue Dec  1 20:29:49 2020
 No Locks

 and the program has passed all test cases.
