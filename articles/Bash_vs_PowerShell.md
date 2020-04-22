
# Differences between Bash and Powershell

## A shell is a command line interface that enables the user to interact with the computer. It is named a shell because it is the outermost layer around the operating system.

| Bash (Bourne-Again shell) | Microsoft PowerShell|
| ----------- | ----------- |
| Bash is a Linux based command line interface (CLI) used for communication or interaction between the operating system and end user.   | PowerShell was first developed for Windows systems, but now also available for Unix-like platforms. PowerShell Core is a cross-platform (Windows, Linux, and macOS) command-line shell, and interactive scripting language. |
| Bash Shell is written by Brian Fox and developed by the GNU project. It was first released in 1989.  | Jeffrey Snover is the Inventor and Architect of Windows PowerShell. It was introduced in 2006.       |
| It is mainly prepared for Linux and Unix operating system from the first day   | It can execute on any version of Windows from Window 97 to Windows 10.      |
| Bash treats outputs as strings  | PowerShell treats output as objects.        |
| It passes output and input as plain text, which means it is easy for the user to move information to the next program.  | PowerShell scripts share complex data, passing entire data structures between commands. PowerShell is object-oriented scripting language.|
| The Bash shell and command language don't offer these capabilities in Windows.   | PowerShell is designed especially for the System administrators to enables them to perform a task on remote and local windows system through full access to COM ([Component Object Model](https://docs.microsoft.com/en-us/windows/win32/com/component-object-model--com--portal)) and WMI ([Windows Management Instrumentation](https://docs.microsoft.com/en-us/windows/win32/wmisdk/about-wmi)). It allows administrators to manage both the workloads windows server and Linux server where production application are hosted.       |
| UNIX commands have been fairly standard in the way that they use options but be mindful, as there are variations.  | PowerShell has the advantage of a consistent syntax structure. The cmdlets are user-friendly and readable.       |
| A pipeline connects the STDOUT (standard output) file descriptor of the first process to the STDIN (standard input) of the second. Each pipe is independent, and simply links the STDOUT and STDIN of the adjacent processes.| Using the pipeline in PowerShell enables users to create powerful one-line commands that pass output to the next command   |
| Bash programs are mainly written in the C programming language as is the linux kernel.    | Powershell is build on .NET framework. It has ability to leverage .NET/C# functionality without having to build an entire C# app        |
| The user interface of Bash shell is a text-based command-line interface.   | PowerShell has graphical as well as command-line interface.        |
| Bash typically relies on a combination of newer tools and classic Unix utilities   | PowerShell has its own set of command-line programs. Although, with Powershell core it's possible to use the same newer and classic Unix utilities as well.       |
| Versatile tool in unix environments that has a wealth of community experience and robust documentation.   | Robust library of Microsoft and third-party modules to interface with an ever-growing number of applications.        |
| On Unix systems, **Man** command gives help on a specific command. **pwd** returns the current working directory name. **ls** to list files and folders. | In PowerShell, **Get-Help** cmdlet provides information about commands and concepts. **Get-Location** cmdlet provides current location **Get-ChildItem** gives the list of files and folder.  *However, PowerShell has built-in aliases for common Unix commands and these aliases points to the actual cmdlet. It can still run windows native commands, scripts, conditional parameters and many more.*|
