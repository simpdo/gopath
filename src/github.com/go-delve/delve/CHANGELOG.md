# Changelog

All notable changes to this project will be documented in this file.
This project adheres to Semantic Versioning.

All changes mention the author, unless contributed by me (@derekparker).

## [1.3.0] 2019-08-27

### Added

- Go 1.13 support (#1546, @aarzilli)
- Starlark scripting language in the command line client (#1466, #1605, @aarzilli, @derekparker)
- Initial support for FreeBSD (#1480, @rayrapetyan)
- Command line flag to continue process immediately after launch/attach (#1585, @briandealwis)
- Configuration option for the maximum recursion depth used when printing variables (#1626, @msaf1980)
- `next` command now takes a numerical option specifying how many times it should be repeated (#1629, @jeremyfaller)
- Command line options to redirect logs to a file or file descriptor (#1525, @aarzilli)
- Ability to read goroutine ancestors if they are enabled by passing `GODEBUG="tracebackancestors=N"` (requires Go >= 1.11) (#1514, #1570, @aarzilli)
- Breakpoint autocompletion for the command line client (#1612, @qingyunha)
- Added reverse step-instruction command for rr backend (#1596, @dpapastamos)
- Support debugging programs using plugins on Linux with Go 1.12 or later (#1413, #1414, @aarzilli) 
- Improved function call injection (#1503, #1504, #1548, #1591, #1602, @aarzilli)
- New variable flag to mark variables that have a fake or no-longer-valid address, because they are either stored in registers or in a stack frame that has been removed from the stack (#1619, @aarzilli)
- Support relative file paths when specifying breakpoint locations (#1478, @chainhelen)
- GetVersion API response now reports currently used backend (#1641, @aarzilli)
- `so` as alias for `stepout` (#1646, @stmuk)

### Fixed

- Fixed values of registers smaller than 64bit (#1583, @derekparker)
- Fixed reading maps with removed entries in Go 1.12 (#1532, @aarzilli)
- Fixed possible crash on Linux caused by function call injection (#1538, @aarzilli)
- Fixed errors reading DWARF sections (#1574, #1582, #1603, @aarzilli)
- Prompt to shutdown headless instance after the target process has exited (#1621, @briandealwis)
- Stacktraces when a SIGSEGV (or other signal) happens during a cgo call (#1647, @aarzilli)
- Error restarting program with next/step/stepout under some circumstances (#1657, @aarzilli)
- Other bug fixes (#1487, #1488, #1490, #1500, #1497, #1469, #1553, #1595, #1594, #1620, #1622, #1624, #1637, #1664, #1665, #1668, @derekparker, @aarzilli, @dpapastamos, @pjot726)

### Changed

- Delve will refuse to work with a version of Go that is either too old or too new (can be disabled with `--check-go-version=false`) (#1533, @aarzilli)
- When the value of a variable is determined to be a symbolic constant the numerical value of the symbolic constant will also be printed (#1530, @aarzilli)
- Catch fatal runtime errors (such as the deadlock detector triggering) automatically (#1502, @aarzilli)
- Replaced glide (which we weren't using anymore) with `go mod vendor` in make script (#1606, @derekparker)
- Removed support for reading interfaces in older versions (prior to 1.7) of Go (#1501, @aarzilli)
- Removed support for location expression "<fnname>:0" and associated API functionality (#1588, @aarzilli)
- Calling an unknown method through the JSON-RPC API will now return an error while previously it would simply be ignored (#1571, @aarzilli)
- Improved documentation and error messages (#1492, #1520, #1524, #1561, #1562, #1556, #1559, #1567, #1638, #1649, #1662, @derekparker, @Ladicle, @qaisjp, @justinclift, @tschundler, @two, @aarzilli, @dr2chase)

## [1.2.0] 2019-02-19

### Added

- Go 1.12 support
- Improved `trace` command to show return values and trace pre-built executables or tests (#1379, #1380, #1381, @derekparker)
- Windows Minidump support (#1386, #1387, #1402, @aarzilli)
- Better support for split DWARF symbol files (#1405, #1420, @derekparker, @slp)
- Function call support on macOS (#1324, @derekparker)
- `deferred` command to view the arguments of a deferred call (#1285, #1265, @aarzilli)
- Support for debugging Position Independent Executables (#1358, @aarzilli)
- Type conversions of byte and rune arrays into strings (#1372, @chainhelen)
- Configuration option (source-list-line-color) to change the color of line numbers in listings (#1364, @Russtopia)
- New expression `iface.(data)` to access the concrete value of interface variable `iface`, without having to write a full type assertion (#1340, @aarzilli)
- Support for specifying multiple source files as arguments for `debug`, `trace` and `test` (#1339, @chainhelen)

### Fixed

- Make `edit` command work with vim and neovim (#1451, @the4thamigo-uk)
- Support Linux kernels prior to 2.6.34 (i.e. without PTRACE_GETREGSET) (#1435, @aarzilli)
- Fixed `substitute-path` configuration option on Windows (#1418, @zavla)
- Better performance for ListGoroutines API call (#1440, #1408, @slp, @aarzilli)
- Better performance when loading the value of very large sparse maps (#1392, @aarzilli)
- Other bug fixes (#1377, #1384, #1429, #1434, #1445, @aarzilli)

### Changed

- Changes to where the configuration is stored, conforming to [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) with fallbacks to the current directory when calls to `user.Current` fail (#1455 @GregorioMartinez, @acshekhara1)
- Project moved from github.com/derekparker/delve to github.com/go-delve/delve (@derekparker)
- Switched dependency management to go.mod (@aarzilli, @derekparker, @zavla)
- New build scripts and support building on macOS without the native backend (@aarzilli, @kevin-cantwell)
- Tolerate corrupted memory when reading the goroutine list (#1354, @aarzilli)
- Improved documentation and error messages (@sbromberger, @aarzilli, @derekparker, @chainhelen, @dishmaev, @altimac)

## [1.1.0] 2018-08-15

### Added

- Go 1.11 support (@aarzilli)
- Improvements to Delve logging (@aarzilli, @derekparker)
- Show global variables in disassembly (@aarzilli)
- Support for inlined calls (@aarzilli, @derekparker, @jaym)
- Support dwz compressed debug symbols (@slp)
- Support for debug info in a separate file (@slp)
- Let target process access the tty when running in headless mode on linux/native and darwin/gdbserial (@aarzilli)
- Commands `up` and `down` (@yasushi-saito)
- Flag to print stacktrace of all goroutines (@acshekhara1)
- Command `edit` (@benc153)
- Allow headless instances to keep running without a connected client (@aarzilli)
- Add `StartLoc` to `api.Goroutine` containing the starting location of each goroutine (@aarzilli)
- Preliminary support for function call injection with Go 1.11 (@aarzilli)
- Ability to read list of deferred calls of a goroutine (@aarzilli)

### Fixed

- Fixed crashes when configuration file can not be created (@derekparker, @yuval-k, @aarzilli)
- Fixed reported location of the go statement of goroutines (@derekparker)
- Allow evaluation of constants specified without the full package path (@aarzilli)
- Fixed some integer arithmetics bugs in proc (@functionary)
- Respect load configuration after reslicing a map (@aarzilli)
- Fixed race condition between Halt and process death in the linux native backend (@aarzilli)
- Support core files generated by gdb (@psanford)
- Fixed evaluation of breakpoint conditions containing a single boolean variable (@aarzilli)
- Miscellaneous bugs in the debug_line state machine (@aarzilli)

### Changed

- Removed redundant/obsolete methods of proc.Process Halt and Kill, general cleanup of native backends (@aarzilli)
- Improved documentation (@giuscri, @jsoref, @Carpetsmoker, @PatrickSchuster, @aarzilli, @derekparker, @ramya-rao-a, @dlsniper)
- Workaround in the gdbserial backend for broken version 902 of debugserver (@aarzilli)
- Changed operators || and && to short-circuit the evaluation of their arguments, like in Go (@aarzilli)
- Mark shadowed arguments as shadowed (@aarzilli)
- Allow syntax "package/path".varname to specify the full package path of a variable, in case disambiguating between multiple packages with the same name is necessary (@aarzilli)

## [1.0.0] 2018-02-19

### Added

- Print DWARF location expression with `whatis` (@aarzilli)
- Use `DW_AT_producer` to warn about optimized code (@aarzilli)
- Use constants to describe variable value (@aarzilli)
- Use `DW_AT_decl_line` to determine variable visibility (@aarzilli)
- `-offsets` flag for `stack` command (@aarzilli)
- Support CGO stacktraces (@aarzilli)
- Disable optimizations in C compiler (@aarzilli)
- `--output` flag to configure output binary (@Carpetsmoker)
- Support `DW_OP_piece`, `DW_OP_regX`, `DW_OP_fbreg` (@aarzilli)
- Support `DW_LNE_define_file` (@aarzilli)
- Support more type casts (@aarzilli)

### Fixed

- Disable file path case normalization on OSX (@aarzilli)
- Support Mozilla RR 5.1.0 (@aarzilli)
- Terminal no longer crashes when process exits during `next` (@aarzilli)
- Fix TestCoreFPRegisters on Go 1.9 (@aarzilli)
- Avoid scanning system stack if it's not executing CGO (@aarzilli)
- Locspec "+0" should always evaluate to the current PC (@aarzilli)
- Handle `DW_LNE_end_of_sequence` correctly (@aarzilli)
- Top level interface variables may have 0 address (@aarzilli)
- Handle `DW_TAG_subprogram` with a nochildren abbrev (@aarzilli)
- StepBreakpoint handling (@aarzilli)

### Changed

- Documentation improvements (@grahamking)
- Removed limitation of exit notifications (@dlsniper)
- Use `go env GOPATH` for install path
- Disable test caching (@aarzilli)
- Disable `-a` and use `all=` for Go 1.10 building (@aarzilli)
- Automatically deref interfaces on member access (@aarzilli)
- Replace all uses of `gosymtab/gopclntab` with `.debug_line` section (@aarzilli)

## [1.0.0-rc.2] 2017-10-16

### Added

- Automatically print panic reason for unrecovered panics (@aarzilli)
- Propagate frame offset to clients (@aarzilli)
- Added vim-delve plugin to documentation (@sebdah)
- Floating point register support in core files (@aarzilli)
- Go 1.9 support, including lexical block support (@aarzilli)
- Added whatis and config commands (@aarzilli)
- Add FrameOffset field to api.Stackframe (@aarzilli)

### Fixed

- Better interoperation with debugserver on macOS (@aarzilli / @dlsniper)
- Fix behavior of next, step and stepout with recursive functions (@aarzilli)
- Parsing of maps with zero sized values (@aarzilli)
- Typo in the documentation of `types` command (@custa)
- Data races in tests (@aarzilli)
- Fixed SetBreakpoint in native and gdbserial to return the breakpoint if it already exists (@dlsniper)
- Return breakpoint if it already exists (@dlsniper)
- Collect breakpoint information on exit from next/stepout/step (@aarzilli)
- Fixed install instructions (@jacobvanorder)
- Make headless server quit when the client disconnects (@aarzilli)
- Store the correct concrete value for interface variables (previously we would always have a pointer type, even when the concrete value was not a pointer) (@aarzilli)
- Fix interface and slice equality with nil (@aarzilli)
- Fix file:line location specs when relative paths are in .debug_line (@hyangah)
- Fix behavior of next/step/stepout in several edge-cases (invalid return addresses, no current goroutine, after process exists, inside unknown code, inside assembly files) (@aarzilli)
- Make sure the debugged executable we generated is deleted after exit (@alexbrainman)
- Make sure rr trace directories are deleted when we delete the executable and after tests (@aarzilli)
- Return errors for commands sent after the target process exited instead of panicing (@derekparker)
- Fixed typo in clear-checkpoint documentation (@iamzhout)

### Changed

- Switched from godeps to glide (@derekparker)
- Better performance of linux native backend (@aarzilli)
- Collect breakpoints information if necessary after a next, step or stepout command (@aarzilli)
- Autodereference escaped variables (@aarzilli)
- Use runtime.tlsg to determine G struct offset (@heschik)
- Use os.StartProcess to implement Launch on windows (@alexbrainman)
- Escaped variables are dereferenced instead of being reported as &v (@aarzilli)
- Report errors when we fail to load the executable on attach (@aarzilli)
- Distinguish between nil and empty slices and maps both in the API and on the command line interface (@aarzilli)
- Skip deferred functions on next and stepout (as long as they are not called through a panic) (@aarzilli)

## [1.0.0-rc.1] 2017-05-05

### Added

- Added support for core files (@heschik)
- Added support for lldb-server and debugserver as backend, using debugserver by default on macOS (@aarzilli)
- Added support for Mozilla RR as backend (@aarzilli)

### Fixed

- Detach should correctly kill child process we created (@aarzilli)
- Correctly return error when reading/writing memory of exited process (@aarzilli)
- Fix race condition in test (@hyangah)
- Fix version extraction to support proposals (@allada)
- Tolerate spaces better after command prefixes (@aarzilli)

### Changed

- Updated Mac OSX install instructions (@aarzilli)
- Refactor of core code in proc (@aarzilli)
- Improve list command (@aarzilli)

## [0.12.2] 2017-04-13

### Fixed

- Fix infinite recursion with pointer loop (@aarzilli)
- Windows: Handle delayed events (@aarzilli)
- Fix Println call to be Printf (@derekparker)
- Fix build on OSX (@koichi)
- Mark malformed maps as unreadable instead of panicing (@aarzilli)
- Fixed broken benchmarks (@derekparker)
- Improve reliability of certain tests (@aarzilli)

### Added

- Go 1.8 Compatability (@aarzilli)
- Add Go 1.8 to test matrix (@derekparker)
- Support NaN/Inf float values (@aarzilli)
- Handle absence of stack barriers in Go 1.9 (@drchase)
- Add gdlv to list of alternative UIs (@aarzilli)

### Changed

- Optimized 'trace' functionality (@aarzilli)
- Internal refactoring to support multiple backends, core dumps, and more (@aarzilli) [Still ongoing]
- Improve stacktraces (@aarzilli)
- Improved documentation for passing flags to debugged process (@njason)

## [0.12.1] 2017-01-11

### Fixed

- Fixed version output format.

## [0.12.0] 2017-01-11

### Added

- Added support for OSX 10.12.1 kernel update (@aarzilli)
- Added flag to set working directory (#650) (@rustyrobot)
- Added stepout command (@aarzilli)
- Implemented "attach" on Windows (@alexbrainman)
- Implemented next / step / step-instruction on parked goroutines (@aarzilli)
- Added support for App Engine (@dbenque)
- Go 1.7 support
- Added HomeBrew formula for installing on OSX.
- Delve now will break on unrecovered panics. (@aarzilli)
- Headless server can serve multiple clients.
- Conditional breakpoints have been implemented. (@aarzilli)
- Disassemble command has been implemented. (@aarzilli)
- Much improved documentation (still a ways to go).

### Changed

- Pretty printing: type of elements of interface slices are printed.
- Improvements in internal operation of "step" command.
- Allow quoting in build flags argument.
- "h" as alias for "help" command. (@stmuk)

### Fixed

- Improved prologue detection for large stack frames (#690) (@aarzilli)
- Fixed bugs involving stale executables during restart (#689) (@aarzilli)
- Various improvements to variable evaluation code (@aarzilli)
- Fix bug reading process comm name (@ggndnn)
- Add better detection for launching non executable files. (@aarzilli)
- Fix halt bug during tracing. (@aarzilli)
- Do not use escape codes on Windows when unsupported (@alexbrainman)
- Fixed path lookup logic on Windows. (@lukehoban)

## [0.11.0-alpha] 2016-01-26

### Added

- Windows support landed in master. Still work to be done, but 95% the way there. (@lukehoban)
- `step-instruction` command added, has same behavior of the old `step` command.
- (Backend) Implementation for conditional breakpoints, front end command coming soon. (@aarzilli)
- Implement expression evaluator, can now execute commands like `print i == 2`. (@aarzilli)

### Changed

- `step` command no longer steps single instruction but goes to next source line, stepping into functions.
- Refactor of `parseG` command for clarity and speed improvements.
- Optimize reading from target process memory with cache. (prefetch + parse) (@aarzilli)
- Shorten file paths in `trace` output.
- Added Git SHA to version output.
- Support function spec with partial package paths. (@aarzilli)
- Bunch of misc variable evaluation fixes (@aarzilli)

### Fixed

- Misc fixes in preparation for Go 1.6. (@aarzilli, @derekparker)
- Replace stdlib debug/dwarf with golang.org/x/debug/dwarf and fix Dwarf endian related parsing issues. (@aarzilli)
- Fix `goroutines` not working without an argument. (@aarzilli)
- Always clear temp breakpoints, even if normal breakpoint is hit. (@aarzilli)
- Infinite loading loop through maps. (@aarzilli)
- Fix OSX issues related to CGO memory corruption (array overrun in CGO). (@aarzilli)
- Fix OSX issue related to reporting multiple breakpoints hit at same time. (@aarzilli)
- Fix panic when using the `trace` subcommand.

## [0.10.0-alpha] 2015-10-04

### Added

- `set` command, allows user to set variable (currently only supports pointers / numeric values) (@aarzilli)
- All deps are vendored with Godeps and leveraging GO15VENDOREXPERIMENT
- `source` command and `--init` flag to run commands from a file (@aarzilli)
- `clearall` commands now take linespec (@kostya-sh)
- Support for multiple levels of struct nesting during variable eval (i.e. `print foo.bar.baz` now works) (@lukehoban)

### Changed

- Removed hardware assisted breakpoints (for now)
- Remove Go 1.4.2 on Travis builds

### Fixed

- Limit string sizes, be more tolerant of uninitialized memory (@aarzilli)
- `make` commands fixed for >= Go 1.5 on OSX
- Fixed bug where process would not be killed upon detach (@aarzilli)
- Fixed bug trying to detach/kill process that has already exited (@aarzilli)
- Support for "dumb" terminals (@dlsniper)
- Fix bug setting breakpoints at chanRecvAddrs (@aarzilli)

## [0.9.0-alpha] 2015-09-19

### Added

- Basic tab completion to terminal UI (@icholy)
- Added `-full` flag to stack command, prints local vars and function args (@aarzilli)

### Changed

- Output of threads and goroutines sorted by ID (@icholy)
- Performance improvement: cache parsed goroutines during halt (@icholy)
- Stack command no longer takes goroutine ID. Use scope prefix command instead (i.e. `goroutine <id> bt`)

### Fixed

- OSX: Fix hang when 'next'ing through highly parallel programs
- Absolute path confused as regexp in FindLocation (@aarzilli)
- Use sched.pc instead of gopc for goroutine location
- Exclude dead goroutines from `goroutines` command output (@icholy)

## [0.8.1-alpha] 2015-09-05

### Fixed
- OSX: Fix error setting breakpoint upon Delve startup.

## [0.8.0-alpha] 2015-09-05

### Added
- New command: 'frame'. Accepts a frame number and a command to execute in the context of that frame. (@aarzilli)
- New command: 'goroutine'. Accepts goroutine ID and optionally a command to execute within the context of that goroutine. (@aarzilli)
- New subcommand: 'exec'. Allows user to debug existing binary.
- Add config file and add config options for command aliases. (@tylerb)

### Changed
- Add Go 1.5 to travis list.
- Stop shortening file paths from API, shorten instead in terminal UI.
- Implemented several improvements for `next`ing through highly parallel programs.
- Visually align registers. (@paulsmith)

### Fixed
- Fixed output of 'goroutines' command.
- Stopped preserving temp breakpoints on restart.
- Added support for parsing multiple DWARF file tables. (@Omie)

## [0.7.0-alpha] 2015-08-14

### Added

- New command: 'list' (alias: 'ls'). Allows you to list the source code of either your current location, or a location that you describe via: file:line, line number (in current file), +/- offset or /regexp/. (@joeshaw)
- Added Travis-CI for continuous integration. Works for now, will eventually change.
- Ability to connect to headless server. When running Delve in headless mode (used previously only for editor integration), you now have the opportunity to connect to it from the command line with `dlv connect [addr]`. This will allow you to (insecurely) remotely debug an application. (@tylerb)
- Support for printing complex numeric types. (@ebfe)

### Changed

- Deprecate 'run' subcommand in favor of 'debug'. The 'run' subcommand now simply prints a warning, instructing the user to use the 'debug' command instead.
- All 'info' subcommands have been promoted to the top level. You can now simply run 'funcs', or 'sources' instead of 'info funcs', etc...
- Any command taking a location expression (i.e. break/trace/list) now support an updated linespec implementation. This allows you to describe the location you would like a breakpoint (etc..) set at in a more convenient way (@aarzilli).

### Fixed

- Improved support for CGO. (@aarzilli)
- Support for upcoming Go 1.5.
- Improve handling of soft signals on Darwin.
- EvalVariable evaluates package variables. (@aarzilli)
- Restart command now preserves breakpoints previously set.
- Track recurse level when eval'ing slices/arrays. (@aarzilli)
- Fix bad format string in cmd/dlv. (@moshee)
