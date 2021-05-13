# Cmpe-283-Assignment3

## Followup Questions
1. Linda and Dhruwaksh worked on all these steps together. We read through the requirements and added the appropriate conditions to the cpuid.c and vmx.c files. 
2. Procedure explained below.
3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there 
more exits performed during certain VM operations? Approximately how many exits does a full VM 
boot entail? 


4. Of the exit types defined in the SDM, which are the most frequent? Least?
** Most Frequent **
These occured thousands of times, where exit reason 12 (HLT) occurred the least at 3,686 exits. 
- 0
- 1
- 7
- 10
- 12
- 28
- 30
- 32
- 48
- 49

** Least Frequent **
These occurred less than 5 times. 
- 29
- 40
- 55

The rest of the exit reasons occurred 0 times. 

## Prompt
Your assignment is to modify the CPUID emulation code in KVM to report back additional information 
when special CPUID leaf nodes are requested.

- For CPUID leaf node %eax=0x4FFFFFFE: 
- Return the number of exits for the exit number provided (on input) in %ecx 
- This value should be returned in %eax 

For leaf nodes 0x4FFFFFFE, if %ecx (on input) contains a value not defined by the SDM, return 0 in all 
%eax, %ebx, %ecx registers and return 0xFFFFFFFF in %edx. For exit types not enabled in KVM, return 
0s in all four registers. 

## Requirements
1. Working Assignment #2

## Procedure
First, we modified the cpuid.c file with a condition for the new CPUID leaf 0x4FFFFFFE. Inside this leaf, we have to check (1) if the value is not defined by the SDM, we need to return the following: 

%eax = 0
%ebx = 0
%ecx = 0
%edx = 0xFFFFFFFF

(2) If the exit type is not enabled in KVM, we need to return 0 for all 4 registers. Otherwise for all other exit values that don't meet these 2 conditions, we need to return the number of exits for the exit number provided on input from %ecx. The value should be returned in %eax. 

To keep track of the exit values, we used an array of size 69 since there are 69 exit types defined by the SDM (with the exception of some missing values). The exit value will be incremented in the vmx.c file. 

After making these changes, rebuild the kernel and reboot the VM: 
```
make && make modules && make install && make modules_install
reboot
```

Inside the nested VM, we created and ran a test file that checks every exit type from 0-69. We also ran the following to check cpuid: 
```
cpuid -l 0x4FFFFFFF
```

We received the following output: 

