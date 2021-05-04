# Cmpe-283-Assignment3

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
Assuming assignment #2 works without fail

## Followup Questions
1. Team responsibilities
2. Procedure explained above.
3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there 
more exits performed during certain VM operations? Approximately how many exits does a full VM 
boot entail? 
4. Of the exit types defined in the SDM, which are the most frequent? Least?
