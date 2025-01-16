# samsung-riscv

This is a RISC-V Talent Development Program, powered by Samsung Semiconductor India Research (SSIR) along with VLSI System Design (VSD).

---

## Basic Details About Me

**Name**: Gokul GR  
**College**: Vidyavardhaka College of Engineering  
**Email ID**: [gokulgr993@gmail.com](mailto:niranjanr916@gmail.com)  
**LinkedIn Profile**: [Gokul GR](https://www.linkedin.com/in/gokul-g-r-76134124a/)

---


<details>
  <summary><strong>Task 1</strong>: Install the RISC-V toolchain using the VDI link and Perform GCC Compilation In Both Normal gcc-compiler and RISC-V Based gcc compiler and check the result.</summary>

### Instructions
1. **VDI Link**: [Download Here](https://forgefunder.com/~kunal/riscv_workshop.vdi)  
   Password for the machine: `vsdiat`

2. **Install Ubuntu 18.04 LTS (Bionic Beaver)**  
   Install on Oracle Virtual Machine Box as mentioned in the guide.

3. **Perform GCC Compilation**  
   - Use both the normal GCC compiler and the RISC-V-based GCC compiler.
   - Compare the results.

  
**1. Install Ubuntu 18.04 LTS(Bionic Beaver) on Oracle Virtual Machine Box as given in the file**
  
![Screenshot 2025-01-05 193249](https://github.com/user-attachments/assets/11a1d650-b105-4a66-842a-b192525b4097)


**2. This screenshot shows a C program (sum1ton.c) compiled and executed, producing the output: "sum of numbers from 1 to 5 is 15". The program, displayed in a text editor (Leafpad).**
```
$ gvim sum1ton.c
$ gcc sum1ton.c
$ ./a.out
```

![Sum1ton](https://github.com/user-attachments/assets/99bfa897-d4bf-406e-a548-c53ae08eebb5)


**3.The screenshot shows the C Code compiled on RISC-V gcc Compiler.**
```
$ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```
![C Code compiled on riscv gcc Compiler](https://github.com/user-attachments/assets/6ed71901-25ce-471f-8f34-1726ed220c92)



Verify that the file has been compiled using below command

```
$ ls -ltr sum1ton.o
```

**4. This screenshot shows the sum1ton.c C program being displayed using the cat command in the terminal, followed by its compilation using the RISC-V GCC compiler (riscv64-unknown-elf-gcc).**


![Cat Command](https://github.com/user-attachments/assets/7f38a710-621a-4333-af8b-3910cbd9dc4b)


**5.The assembly code is generated using**
```
$ riscv64-unknown-elf-objdump -d sum1ton.o
$ riscv64-unknown-elf-objdump -d sum1ton.o | less
```
* Here the **-d** stands for disassemble
* **Objdump using -O1 format**
* ```
   $ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
  
![Objdump using -O1 format](https://github.com/user-attachments/assets/6703bb29-75d1-492a-9b67-faac24f2dc01)


* **Number of Instruction for -O1 format**
![calculate -O1 format](https://github.com/user-attachments/assets/40042543-942d-41c6-b703-59f3e465def0)


* Here there are 11 instructions that is B in hexadecimal
---
* **Objdump using -Ofast format**
* ```
  $ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
  
![Objdump using -Ofast format](https://github.com/user-attachments/assets/88575f69-8b48-4fa8-8624-97a032abeb95)

* **Number of Instruction for -Ofast format**

![calculate -Ofast format](https://github.com/user-attachments/assets/09452187-f4c2-4129-bf18-f064f5d90dd4)

* Here there are 11 instructions that is B in hexadecimal
  </details>
------------


<details>
<summary><b>Task 2:</b>: To write a simple C program and to compile the C program using RISC-V GCC/SPIKE with the O1 and Ofast optimization flags and to generate and collect the RISC-V object dump for both -O1 and -Ofast</summary> 
  
### 1.Simple C program Compilation
![gcc_compilation](https://github.com/user-attachments/assets/a7eda4d8-6889-429c-a896-cfe7311f3abb)

### 2.verify that your code is giving same output even when you use RISC-V compiler as shown.
![RISC-v_compilation](https://github.com/user-attachments/assets/d1ef12bf-a549-4783-9857-87c7c3165005)

Here that spike command is used in place of ./a.out to see the output and successfully we have obtained same output
```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o factorialofn.o factorialofn.c

$ spike pk factorialofn.o
```
### 3. assembly code instructions using the SPIKE tool.
![spike-O1](https://github.com/user-attachments/assets/68769899-3a94-406d-bd6e-a3f23c651fea)

![spike-Ofast](https://github.com/user-attachments/assets/933585b3-9ee6-4262-845c-deef45203e0a)

lui : load upper immediate basically a RISC-V register has 32 bits in which the first 7 are opcode and next from 7 to 11 is rd and next remaning bits are immediate to which the value 0x2b is inserted
Next instruction which is going to be executed according to dumpfile will be addi sp,sp,-48.

which means 48 decimal value which will be 30 in hexa that much will be subtracted from the current stack pointer value. 

### 4. RISC-V object dump for O1 optimization level
![obj_dump_for_O1](https://github.com/user-attachments/assets/caa7893a-36b3-460f-a992-c31c0ee4190f)

### 5. RISC-V object dump for Ofast optimization level
![obj_dump_for_Ofast](https://github.com/user-attachments/assets/ead23dc5-084e-4319-89dd-92fe11edbe44)

  
</details>

--------

<details>
  <summary><strong>Task 3</strong>:To identify 15 unique RISC-V instructions from the riscv-objdump of my application code and to determine the exact 32 bit instruction code from those 15 instructions</summary>

![Ofast](https://github.com/user-attachments/assets/7c2a5809-73de-4c78-be8d-09fca6c90b2c)



## 1. lui (Load Upper Immediate)

Loads a 20-bit immediate value into the upper 20 bits of a register, while the lower 12 bits are set to zero.
lui a0, 0x2b (Loads 0x2b000 into a0).
Instruction Code: 0x0002b537
Type: U-type (Upper immediate)

## 2. addi (Add Immediate)

Adds a sign-extended 12-bit immediate value to a register and stores the result in a destination register.
addi a0, a0, -704 (Adds -704 to a0 and stores the result back in a0).
Instruction Code: 0xd4050513
Type: I-type (Immediate)

## 3. sd (Store Doubleword)

Stores a 64-bit value from a source register to memory.
sd s1, 24(sp) (Stores the value of s1 at the memory address sp + 24).
Instruction Code: 0x00913c23
Type: S-type (Store)

## 4. jal (Jump and Link)

Jumps to a target address and saves the return address in the link register (ra).
jal ra, 1058b (Jumps to address 1058b and stores the return address in ra).
Instruction Code: 0x4f0000ef
Type: J-type (Jump and Link)

## 5. lw (Load Word)

Loads a 32-bit value from memory into a register.
lw s1, 12(sp) (Loads a 32-bit word from sp + 12 into s1).
Instruction Code: 0x00c12483
Type: I-type (Load)

## 6. bltz (Branch if Less Than Zero)

Pseudo-instruction for blt (branch if less than). Checks if the source register is less than zero, and if true, branches to the target address.
bltz a1, 10134 (Branches if a1 is less than zero).
Instruction Code: 0x044c4a63
Type: B-type (Branch)

## 7. li (Load Immediate)

Pseudo-instruction for addi. Loads an immediate value into a register.
li a0, 1 (Loads 1 into a0).
Instruction Code: 0x00100513
Type: I-type (Immediate)

## 8.beqz (Branch if Equal to Zero)

Pseudo-instruction for beq. Checks if a register equals zero, and if true, branches to the target address.
beqz a5, 1015c (Branches if a5 is zero).
Instruction Code: 0x00078663
Type: B-type (Branch)

## 9. addiw (Add Immediate Word)

Adds a sign-extended 12-bit immediate to a 32-bit word and stores the result in the destination register.
addiw s1, s1, 1 (Adds 1 to s1 and stores the result back in s1).
Instruction Code: 0x0011a09b
Type: I-type (Immediate)

## 10. mv (Move)

Pseudo-instruction for addi. Copies the value from one register to another.
mv a0, a0 (Moves the value of a0 to a0, effectively a no-op).
Instruction Code: 0x00050513
Type: I-type (Immediate)


## 11. bne (Branch if Not Equal)

Compares two registers and branches to a target address if they are not equal.
bne s1, s0, 10100 (Branches if s1 is not equal to s0).
Instruction Code: 0xfea592e3
Type: B-type (Branch)

## 12. ld (Load Doubleword)

Loads a 64-bit doubleword from memory into a register.
ld s0, 32(sp) (Loads a 64-bit value from sp + 32 into s0).
Instruction Code: 0x02013083
Type: I-type (Load)

## 13.ret (Return)

Pseudo-instruction for jalr. Returns from a function by jumping to the address in the link register (ra).
ret (Jumps to the address in ra).
Instruction Code: 0x00008067
Type: I-type (Jump and Link Register)

## 14. j (Jump)

Pseudo-instruction for jal. Unconditionally jumps to a specified address.
j 1011c (Jumps to address 1011c).
Instruction Code: 0xfddff06f
Type: J-type (Jump)

## 15.auipc (Add Upper Immediate to PC)

 Adds a 20-bit immediate value to the upper 20 bits of the program counter (PC) and stores the result in a destination register.
auipc a5, 0xfffff (Adds 0xfffff000 to the current PC and stores the result in a5).
Instruction Code: 0xfffff797
Type: U-type (Upper immediate)


</details>
