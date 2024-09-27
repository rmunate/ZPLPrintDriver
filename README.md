# ZPL Print Universal Driver

`ZPLPrintDriver.exe` is a versatile command-line tool for sending ZPL (Zebra Programming Language) code to network-connected Zebra printers. It is designed to be easily integrated into various programming environments that support console command execution.

## Features

- Send ZPL code directly from a file to a Zebra printer over the network.
- Supports specifying the printer's IP address and port.
- Allows printing multiple copies of the label.
- Configurable timeout for network operations.
- Cross-language compatibility through easy-to-use command-line execution.

## Usage

You can run the program directly from the command line by providing the necessary arguments.

### Command Line Arguments

- `--path` (required): Full path to the ZPL file you want to send to the printer.
- `--printer` (required): The IP address of the Zebra printer.
- `--port` (optional): Printer port number. Default is `9100`.
- `--copies` (optional): Number of copies to print. Default is `1`.
- `--timeout` (optional): Timeout in seconds for the network connection. Default is `10` seconds.

### Command Line Example

```bash
ZPLPrintDriver.exe --path "C:\path\to\your\file.zpl" --printer "192.168.1.100" --port 9100 --copies 2 --timeout 10
```

### Explanation

- `--path`: Specifies the ZPL file located at `C:\path\to\your\file.zpl`.
- `--printer`: The printer's IP address is `192.168.1.100`.
- `--port`: The printer is accessed on port `9100`, which is the default port for most Zebra printers.
- `--copies`: Two copies of the label will be printed.
- `--timeout`: The command will wait up to 10 seconds for a response from the printer before timing out.

---

## Using from Various Programming Languages

### Python Example

In Python, you can use the `subprocess` module to call `ZPLPrintDriver.exe`.

```python
import subprocess

# Command to run the executable with arguments
command = [
    "ZPLPrintDriver.exe",
    "--path", "C:\\path\\to\\your\\file.zpl",
    "--printer", "192.168.1.100",
    "--port", "9100",
    "--copies", "1",
    "--timeout", "10"
]

# Execute the command
result = subprocess.run(command, capture_output=True, text=True)

# Print the output
print(result.stdout)
```

### C# Example

In C#, you can use the `Process` class to execute the command and interact with the output.

```csharp
using System;
using System.Diagnostics;

class Program
{
    static void Main(string[] args)
    {
        // Create and configure the process
        Process process = new Process();
        process.StartInfo.FileName = "ZPLPrintDriver.exe";
        process.StartInfo.Arguments = "--path \"C:\\path\\to\\your\\file.zpl\" --printer \"192.168.1.100\" --port 9100 --copies 1 --timeout 10";
        process.StartInfo.RedirectStandardOutput = true;
        process.StartInfo.UseShellExecute = false;
        process.StartInfo.CreateNoWindow = true;

        // Start the process
        process.Start();

        // Read and display the output
        string output = process.StandardOutput.ReadToEnd();
        Console.WriteLine(output);

        // Wait for the process to exit
        process.WaitForExit();
    }
}
```

### PHP Example

In PHP, the `exec()` function can be used to invoke the executable.

```php
<?php
// Command to execute the ZPL print driver
$command = "ZPLPrintDriver.exe --path \"C:\\path\\to\\your\\file.zpl\" --printer \"192.168.1.100\" --port 9100 --copies 1 --timeout 10";

// Execute the command and capture the output
$output = shell_exec($command);

// Display the output
echo $output;
?>
```

### Ruby Example

In Ruby, you can use the `system()` function to run the command.

```ruby
# Command to run the ZPLPrintDriver.exe
command = 'ZPLPrintDriver.exe --path "C:\\path\\to\\your\\file.zpl" --printer "192.168.1.100" --port 9100 --copies 1 --timeout 10'

# Execute the command
system(command)
```

### Visual Basic (VBScript) Example

In VBScript, you can use the `WScript.Shell` object to run the executable.

```vbscript
Set objShell = WScript.CreateObject("WScript.Shell")

' Command to run ZPLPrintDriver.exe
command = "ZPLPrintDriver.exe --path ""C:\path\to\your\file.zpl"" --printer ""192.168.1.100"" --port 9100 --copies 1 --timeout 10"

' Execute the command
objShell.Run command, 0, True
```

### PowerShell Example

In PowerShell, you can execute the command using `Start-Process`.

```powershell
# Define the command
$command = "ZPLPrintDriver.exe --path 'C:\path\to\your\file.zpl' --printer '192.168.1.100' --port 9100 --copies 1 --timeout 10"

# Execute the command
Start-Process -FilePath "cmd.exe" -ArgumentList "/c $command" -NoNewWindow -Wait
```

### WScript (Windows Script Host) Example

In WScript, you can execute the command with `Exec` and capture the output.

```js
var shell = new ActiveXObject("WScript.Shell");

// Command to run ZPLPrintDriver.exe
var command = 'ZPLPrintDriver.exe --path "C:\\path\\to\\your\\file.zpl" --printer "192.168.1.100" --port 9100 --copies 1 --timeout 10';

// Execute the command
var exec = shell.Exec(command);

// Read and print the output
while (!exec.StdOut.AtEndOfStream) {
    WScript.Echo(exec.StdOut.ReadLine());
}
```

### JavaScript (Node.js) Example

In Node.js, use the `child_process` module to run the executable.

```javascript
const { exec } = require('child_process');

// Command to run the executable
const command = 'ZPLPrintDriver.exe --path "C:\\path\\to\\your\\file.zpl" --printer "192.168.1.100" --port 9100 --copies 1 --timeout 10';

// Execute the command
exec(command, (error, stdout, stderr) => {
    if (error) {
        console.error(`Error: ${error.message}`);
        return;
    }
    if (stderr) {
        console.error(`Stderr: ${stderr}`);
        return;
    }
    console.log(`Stdout: ${stdout}`);
});
```

### Excel VBA Example

In Excel VBA, you can execute the command using the `Shell` function.

```vba
Sub PrintZPL()

    ' Define the command arguments
    Dim zplFile As String
    Dim printerIP As String
    Dim printerPort As String
    Dim copies As Integer
    Dim timeout As Integer
    Dim command As String

    ' Set the values for the ZPL file path, printer IP, port, and other parameters
    zplFile = "C:\path\to\your\file.zpl"
    printerIP = "192.168.1.100"
    printerPort = "9100"
    copies = 1
    timeout = 10

    ' Create the full command string
    command = "ZPLPrintDriver.exe --path """ & zplFile & """ --printer """ & printerIP & """ --port " & printerPort & " --copies " & copies & " --timeout " & timeout

    ' Execute the command using the Shell function
    Shell command, vbNormalFocus

End Sub
```

---

## Error Handling

If there are any errors (e.g., invalid printer IP, file not found), the program returns a JSON response in the following format:

```json
{
  "result": "Fail",
  "error": "Description of the error"
}
```

For successful execution, the output will look like this:

```json
{
  "result": "Success",
  "path": "C:\\path\\to\\your\\file.zpl",
  "printer": "192.168.1.100",
  "port": 9100,
  "copies": 2
}
```

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
