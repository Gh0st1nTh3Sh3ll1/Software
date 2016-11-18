# IDA PRO 6.8 Hex-Rays


IDA: What's new in 6.8

Link Download : https://drive.google.com/file/d/0B86Bzm6gmkfoZUZtNkpWdk55MUU/view?usp=sharing

Highlights

This is mainly a maintenance release, so our focus was on fixing bugs. However, there are some improvements too:
Support for long names. In previous versions of IDA names were limited to 511 bytes. This was causing problems, especially with long mangled C++ names (e.g. boost names). We removed this limitation in many places of IDA. The work is not complete, there are still some areas where the limitation exists but overall the listings are more readable now.
Dalvik: added support for OAT files
PPC: support for Power ISA 2.07
Better analysis of prolog code; better register tracking, especially for ARM
Lots of vulnerabilities fixed thanks to the submissions to our bug bounty program
Complete changelist

Processor Modules

ARM: Better tracking of registers, improved analysis
ARM: added support for scattered arguments (that are partially passed on the stack and partially in registers)
PC: improved prolog analysis
PPC: added support for a switch variation produced by the Green Hills compiler
PPC: support for Power ISA 2.07
File Formats

COFF: added support for irix mips files (no support for relocations yet)
Dalvik: added support for OAT files
DWARF: basic support for clang-generated DWARF variable location
DWARF: very basic support for 'rustc'-produced DWARF information
Debugger

PIN: add support for reading of FPU/XMM registers from internal exception tracing: can display addresses as raw, instead of using seg/func/offset representation
Kernel/Misc

kernel: introduced the notion of ASM and C level types; IDA tries to preserve member offsets only for ASM types; C types may change their sizes because of the changes to other types they depend on
kernel: added support for long names: type, function, label, etc names can be up to 32767 bytes long
demangler: improved to recognize new mangled names
til: added type library for Windows 8.1 (user mode)
til: updated windows til files improved automatic recognition of ascii string by the autoanalyzer
User Interface

