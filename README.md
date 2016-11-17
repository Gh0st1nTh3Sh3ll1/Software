# Software

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

UI: idaq dock menu on mac now features a list of recent files
UI/qt: It is now possible to navigate back & forward in location history with the mouse side navigation buttons (for mice that feature those) in graph & proximity view as well (it was already possible in listing view)
UI: display a warning if the user rebases program around 0xFF000000 (it may cause problems because these addresses are used for internal housekeeping)
UI: graph: Ctrl-Keypad-+ and Ctrl-Keypad-- can now be used to quickly collapse/reveal a node's contents
UI: GraphOverview: can optionally use a blank background (just like before 6.7)
UI: Proximity: added ability to have multiple paths, set their color, turn them on/off and delete them
Scripts & SDK

IDC: added ExpandStruc()
IDC: improved SetLocalType: it accepts typeinfo object as the second argument in addition to declaration strings; added PT_REPLACE so that local types can be replaced
IDAPython: allow accessing a til_t's "base" til_t objects
IDAPython: in addition to AskUsingForm (that opens a dialog), it is now possible to call OpenForm (e.g., to open a form as a tab.)
IDAPython: added ExpandStruc()
IDAPython: USE_LOCAL_PYTHON config parameter is deprecated, IDA autodetects local Python installation now
SDK: added "segm_attrs_changed" event so that plugins can take appropriate actions if necessary
SDK: added print_decls(), allowing to print types from a type library (possibly including dependencies) in a format suitable for C(++) compilation
SDK: added support for default register bits of 64-bit debugger registers
SDK: added tinfo_t::clr_const,clr_volatile,clr_const_volatile functions
SDK: made the return codes of ph.notify() callbacks more plugin-friendly
SDK: netnode names can be of arbitrary length. for practical reason we limit them by 32KB
SDK: qstrncpy and similar functions will raise interr if the size argument is 0 or negative
SDK: replaced get_true_name() and similar functions by get_ea_name(), which accepts qstring as the output buffer; this allows for names of unlimited length, if necessary
SDK: segment names and classes use a separate namespace now and do not hinder functions or data labels with the same name
SDK: tinfo_t::get_unpadded_size() now works not only for c++ objects but for all structs
SDK: ui: forms: Added askqstr() - the kind of askstr() but with qstring argument
SDK: ui: new chooser_item_attrs_t::flags flag CHITEM_GRAY is added to show chooser item grayed out (like disabled). It is now used for the Local types choser to distinct guest types (syncronized from structure/enum views)
BUGFIXES

BUGFIX: '-' was forbidden in type names but it can be encountered in template arguments
BUGFIX: ARM: A reference to SP (R13) in the register list of the LDMDB instruction (and similar ones) was not allowed by IDA, while some ARM devices can apparently execute it
BUGFIX: COFF: specially crafted COFF files could trigger invalid memory writes on OS X
BUGFIX: Calling refresh_chooser() on a chooser that's embedded in an AskUsingForm might fail calling the possible form callback with a possibly-updated rows selection
BUGFIX: Cmd+C was broken on OSX, and copying was only possible through Ctrl+C
BUGFIX: Creating 2 GraphRenderer with the same title could crash IDA
BUGFIX: Deprecated function add_menu_item() would place the item at the end of the menu if the path was of the form "Edit/Other/" (i.e., ending with an empty string), while it used to place the action on top before
BUGFIX: Deprecated function add_menu_item() wouldn't accept '-' as a separator anymore; only expecting '' (i.e., empty string) was allowed for separators
BUGFIX: Double-clicking on a thread in the list would jump to the wrong thread, if the list was sorted by a column
BUGFIX: During debugging, clicking on some strings containing format specifiers could cause IDA to display the wrong data
BUGFIX: Exporting structures to IDC could lose type information for their members
BUGFIX: File save dialog could have an empty/undefined file name on OSX (Issue 1232)
BUGFIX: Force switching to graph view on functions with huge number of nodes, might cause IDA to crash
BUGFIX: Global variable database_idb was not reset to the empty string after a database was closed
BUGFIX: Hex-View widgets had lost the ability to allow direct editing of the text in their rightmost area (since IDA 6.4)
BUGFIX: IDA could hang after not adequately handling a segment register change
BUGFIX: IDA could hang trying to coagulate unknown bytes within a code segment
BUGFIX: IDA could sometimes print garbage after cross references between structs
BUGFIX: IDA had no way to reset the background color of proximity view nodes that were highlighted by the 'Find path' action
BUGFIX: IDA was displaying split Unicode strings for big-endian processors incorrectly
BUGFIX: IDA would incorrectly report a circular dependency when trying to export a type containing a deleted type
BUGFIX: IDA would try to generate disassembly text for nodes that are unreasonably large
BUGFIX: IDAPython Hex-Rays bindings: could crash IDA because access to members of unions, while they didn't make sense, were allowed (and thus SWiG created buggy proxies around invalid pointers.)
BUGFIX: IDAPython was not exposing tinfo_t::get_named_type(), because SWiG rules in typeinf.i were too broad
BUGFIX: IDAPython's IDC-style ApplyType() wasn't working for structure members
BUGFIX: IDAPython: GetSegmentAttr/SetSegmentAttr would fail with segment registers
BUGFIX: IDAPython: Only the first 'long name' of python-based processor modules was considered
BUGFIX: IDAPython: build.py didn't trigger the patching of some directors methods calling convention, resulting in compilation failure with flag "--with-hexrays"
BUGFIX: IDAPython: expose ::get_named_type()
BUGFIX: IDAPython: idautils.DecodePreviousInstruction() was not checking for the right value returned from idaapi.decode_prev_insn()
BUGFIX: In IDAPython, re-using the same action description twice when registering dynamic context menu items could lead to a crash
BUGFIX: In some rare cases, IDA could crash when closing down & force-exiting a debugging session
BUGFIX: Installers couldn't be run in unattended mode, because the 'setEncryptionPassword' directive was specified in a '<validationActionList>', which is not executed in unattended mode
BUGFIX: It was impossible to comment function stack variables in "Stack of <function name>" windows
BUGFIX: It was impossible to rename structure fields from IDA View-A anymore
BUGFIX: It was possible, through process_ui_action(), to invoke the code for an action that was disabled
BUGFIX: Mach-O DWARF source-level debugging could fail to find the source file
BUGFIX: Mach-O source-level debugging DWARF could fail finding shared libraries source files because it would miss some items (it wasn't taking ASLR into account)
BUGFIX: Manually loading a PE overlay could cause previous segments to be stretched, which would then conflict with later segments being loaded
BUGFIX: Not Free()ing a Compile()d idaapi.Form could cause IDA to crash at exit-time
BUGFIX: On OSX, opening the "About" dialog, then the "Addons" dialog, then closing the "Addons" and performing Ctrl+C could crash IDA
BUGFIX: PDB could fail on meaningless array descriptions, when those are packed into structures
BUGFIX: PDB was not properly parsing unnamed types of the form "SOME_NAMED_THING::__unnamed"
BUGFIX: PDB: improved responsivity of IDA while it's loading PDB information
BUGFIX: PIN: IDA could report incorrect address in an exception description
BUGFIX: PIN: pintool could crash when running with disabled ST_OVER... trace options
BUGFIX: PIN: pintool could report incorrect register values in case of internal exception
BUGFIX: Program rebasing could produce incorrect name records in the database
BUGFIX: Rebasing the program would lead to erroneous addresses in the "Imports" window, until that window is closed & re-opened
BUGFIX: Reloading some PE files could lead to an internal error
BUGFIX: Retina: When zooming in/out of the graph view, nodes contents could appear smaller
BUGFIX: Right-clicking on an identifier in a node wouldn't set the cursor position to that identifier before opening the context menu, resulting on context menu items irrelevant for the wanted identifier
BUGFIX: Saving the IDB would cause the history to be modified
BUGFIX: Selecting a node that is overlapping another node, and Ctrl+dragging (for selecting) from another node was sometimes producing an interr
BUGFIX: Selecting by rectangle in graph view was displaying the rectangle at its position * 2 on OSX retina displays
BUGFIX: Setting a widget's icon wouldn't be reflected in the UI
BUGFIX: Setting function prototypes to similar-looking prototypes, but whose arguments come from other type info libraries, could cause IDA to interr 1064
BUGFIX: Specifying an erroneous binary path mapping & then correcting it, could cause IDA to keep requesting for mappings
BUGFIX: When calling 'attach_action_to_menu' with a menu path starting with "Edit" from the "Recent scripts" window, the action could end up in the 'Recent scripts's own Edit menu, instead of in the global one
BUGFIX: When changing a variable/argument type in a function frame, 'Structures' xrefs might not be updated
BUGFIX: When debugging with WinDbg, stepping over some instructions that cause debugging events (e.g., a "call CreateProcess", causing library load events) might fail & let the program run freely
BUGFIX: When debugging, performing unaligned read_dbg_memory() on linux targets could return wrong data (and so could DbgRead() and idaapi.dbg_read_memory())
BUGFIX: When debugging, synchronizing a Hex View with a register, then later syncing with another register would lead the view to be synced with both registers
BUGFIX: When importing structures from an IDC strict, some dependencies were missing (if those dependencies were defined later in the file.)
BUGFIX: When in graph view, IDA had lost the ability to create groups with only one node (as some users sometimes desire.)
BUGFIX: When in graph view, pressing <Enter> to follow an identifier that will cause the view to switch to listing view, then opening a dialog (e.g., renaming that identifier), and finally going back to graph view, could cause some actions to be unavailable (e.g., 'Hide group'.)
BUGFIX: When the DWARF information for "well-known types" (e.g., __m128d) was erroneous, the DWARF plugin was creating erroneously-sized structures, causing the decompiler to fail
BUGFIX: When the graph layout is locked, clicking within nodes of user-provided graphs wouldn't change the cursor & update the highlight
BUGFIX: add_menu_item() backward compatibility was broken when the path didn't contain any slash. E.g., "Options"
BUGFIX: an expression like sizeof(struct) was creating an xref to the first struct member; changed it to create an xref to the entire structure
BUGFIX: autoanalysis could hang on some wrong code sequences or corrupted files
BUGFIX: better distinction between the code/data conversions done automatically by ida and by the user
BUGFIX: btree: IDA could abort in rare cases when removing a subtree from a database
BUGFIX: cli: IDA could crash trying to print strings coming from very corrupted (i.e., fuzzed) input files with corrupted signatures
BUGFIX: compacting a type library in the presence of aliased types could lead to interr
BUGFIX: corrupted codeview info could crash ida
BUGFIX: corrupted epoc files could crash ida
BUGFIX: corrupted xcoff files could crash ida
BUGFIX: corrupted database (idb/i64) could lead to memory corruption
BUGFIX: dalvik: added "green arrow", which points to the next executed instruction in the debugger
BUGFIX: dbg: dalvik: slot coinciding with "retval" was erroneously ignored when the locals are collected
BUGFIX: dbg: gdbserver: reinitialize the registers information when the target architecture is detected
BUGFIX: dbg: linux_server: signals from the different threads may arise simultaneously without special order, so in the interr 30057 we must weaken the condition
BUGFIX: dbg_read_memory()/DbgRead() could return garbage data for unmapped regions
BUGFIX: debugger: request_step_into() could cause interr 40396
BUGFIX: debugging with gdbserver was impossible for mips executables starting at 0x80000000
BUGFIX: defining the same standard structure twice could lead to a crash
BUGFIX: deleting structures could break navigation in the structures window
BUGFIX: dump typeinfo to idc: in some cases EndTypeUpdating(UTP_ENUM) was missing in the generated file
BUGFIX: dumy typeinfo to idc: structures alignments were missing
BUGFIX: editing a enum type from the local types view to a wrong definition (for example, reusing a symbol that was used elsewhere) would lead to desynchronization with the enum view; fixed other similar problems
BUGFIX: editing a local type would desynchronize it from idb types
BUGFIX: export types: anoonymous nested struct/union types were referred by a generated name; this was leading to an incorrect c declaration
BUGFIX: fixed internal error in the instruction decoder for mips (opcode 78787878 was causing it)
BUGFIX: fixed interr 40208 that could occur when terminating the debugger
BUGFIX: fixed interr 518
BUGFIX: fixed interr 599 (the value of a 6-byte pointer could not be printed as a c declaration)
BUGFIX: fixed interr 608
BUGFIX: fixed multiple vulnerabilities in the rpc protocol between ida and debuggser servers
BUGFIX: fixed some idc nuisances reported on the forum
BUGFIX: gdbserver: disabling single-step support could render the debugger module unusable, ida would complain about wrong RESMOD bits
BUGFIX: ida could crash after calling StartProcess("","","") from the python command line while using a remote GDB debugger
BUGFIX: ida could crash during analysis
BUGFIX: ida could crash or hang on corrupted cli files
BUGFIX: ida could crash when stopping the debugger
BUGFIX: ida could crash while analyzing a file (if a function tail was deleted during enumerating function tails)
BUGFIX: ida could crash with stack overflow while analyzing borland template data
BUGFIX: ida could hang trying to load a corrupted pe file
BUGFIX: ida could hang trying to load corrupted aout file
BUGFIX: ida could hang when analyzing some files
BUGFIX: ida could interr when compacting a type library
BUGFIX: ida would hang trying to display huge (>2GB) arrays
BUGFIX: ida64 would interr trying to calculate arglocs for some functions
BUGFIX: idapython: fixed idx.savefile. Previous implementation has failed to open new file
BUGFIX: idaw would not accept non-ascii file names from the command line
BUGFIX: if an address was marked as 'notcode', it would lead to odd situation when the user would define an instruction but ida would immediately delete it
BUGFIX: if idb was saved before any planned signatures had been applied, autoIsOk would never return true
BUGFIX: if sending a bug report failed, ida would simply tell the user about it; now we show the dialog box once more so that the user can copy the bug report out of ida
BUGFIX: if the last thing we do before saving the idb to the disk is to define a big item that uses both STT_VA and STT_MM storage methods, the sparse flags would not be saved correctly to the disk (they would not be marked as dirty)
BUGFIX: if the struct indexes got corrupted, some of struct types were permanently missing from the list
BUGFIX: importing a struct type from the local types window to the struct view could crash ida
BUGFIX: instant debugging: gdb module was not configuring its registers correctly if the target processor was changed at the last moment
BUGFIX: mac_server would make one processor core 100% busy after debugging an application
BUGFIX: mc16c: ida could crash trying to display an bad instruction
BUGFIX: parsing of argument locations in a register with an offset was broken (e.g. rdx^4.2)
BUGFIX: pe: ida could complain about truncated input file in some rare cases
BUGFIX: pe: ida could hang trying to load a corrupted file
BUGFIX: pe: replaced interr 20064 with a silent failure because it may occur on corrupted input files
BUGFIX: pe: validation of the number of exported addresses was wrong
BUGFIX: ppc: dquai and dquaiq instructions could not be decoded
BUGFIX: read-access hardware breakpoints on win64 were broken
BUGFIX: setting a new target compiler must lead to recalculation of argument locations (especially for x64 where gcc and ms behave differently)
BUGFIX: some type names were displayed as #N (where N is the type number)
BUGFIX: symbol addresses in 32-bit map files were relative to the segment start, not to the segment base (pe files were not affected by this bug)
BUGFIX: the struct/enum views were not automatically refreshed after idc/python scripts that modify them
BUGFIX: tilib was not accepting enum redefinitions if a constant with the high bit set was present (for example, 0x80000000)
BUGFIX: tinfo validation could erroneously fail for aliased types
BUGFIX: tls callbacks in pe+ files were handled incorrectly
BUGFIX: tms320c6: some insns were disassembled incorrectly or not at all
BUGFIX: type validation was too strict: an internal type alias may differ from its target in the type modifiers (const/volatile). they are one of the reasons why we have internal aliases after all
BUGFIX: types entered by the user were not lowered; it is safer to try to lower them in order to get rid of arrays as function arguments, for example
BUGFIX: ui: docks: Prevented creation of empty areas
BUGFIX: ui: qt: Fixed disappearing of persistent dock if "Float" button in the dock header is clicked
BUGFIX: when debugging, double-clicking on an address in the stack view wouldn't jump anymore
BUGFIX: when exporting types, ida could fail to define a structure that was previously used in a typedef
BUGFIX: xrefs to the structure members would disappear after renaming a structure/enum or other manipulations with it
BUGFIX: IDA would fail to delete the last history item from the QuickStart dialog.
BUGFIX: IDAPython Choose2 instances that were self.Close()ing as a part of an OnCommand() callback could crash IDA.
BUGFIX: IDAPython Choose2-based choosers could not be notified of selection changes (through their 'OnSelectionChange' callback.)
BUGFIX: IDAPython calling 'term_database' could leave some windows opened that still need a database, leading to a crash.
BUGFIX: Painting widgets from PySide in IDAPython could cause IDA to crash.
BUGFIX: When toggling (with <Tab>) between Hex-Rays & IDA View-A, hex-rays could cause IDA View-A to move the cursor.
BUGFIX: clicking on opcode bytes AF, CF and DF would result in no highlighting whatsoever.
BUGFIX: fixed interr 40208 which could occur if the network connection to the remote debugger was broken
BUGFIX: interr 820 could occur when loading dwarf debug info
BUGFIX: pc: register tracking was leading to wrong results in omf files
BUGFIX: pc: some instructions were erroneously marked as belonging to the function epilog; this would lead to wrong decompilation
BUGFIX: read-only page breakpoints would be missed if added into an executable page
