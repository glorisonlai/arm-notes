## Requires
Windows ISO
WinDbg (and .Net4)
Python
HEVD (Vulnerable Driver)
OSR Loader

# Windows 7
1. Set System Variable `_NT_SYMBOL_PATH` to `SRV*C:\Symbols*https://msdl.microsoft.com/download/symbols`
2. Run commands
```
bcdedit /copy {current} /d "Win7Dbg" # The entry was successfully copied at {ADDR}
bcdedit /debug {ADDR} on
bcdedit /dbgsettings
```
3. Create Linked Clone (Debugee)
4. Debugger: Enable Serial Port as Host Pipe at `\\.\pipe\Win7Dbg`. 
5. Debugee: Enable Serial Port as Host Pipe connecting to existing `\\.\pipe\Win7Dbg`
6. Run Debugger in Normal mode, and open WinDbg -> File -> Kernel Debug
7. Run Debugee in Debug mode

## Installing Drivers
1. Debugee: Run OSRLoader, register and start .sys driver
2. Debugger: Install .pdb file at wherever the error happens
3. Debugger: Run commands
```
kd> !sym noisy
kd> .reload
kd> lm m <NAME>
```

## Debugging
