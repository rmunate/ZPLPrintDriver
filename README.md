# ZPL Print Universal Driver

`ZPLPrintDriver.exe` is a command-line tool designed to send ZPL (Zebra Programming Language) code to a network printer. It is built to be flexible and can be integrated into any programming language capable of executing console commands.

## Features

- Send ZPL code directly from a file to a Zebra printer over the network.
- Supports specifying the printer's IP address and port.
- Allows you to print multiple copies of a label.
- Configurable timeout for network operations.

## Usage

The program can be run from the command line by specifying the required arguments.

### Command Line Arguments

- `--path` (required): The full path to the ZPL file you want to send to the printer.
- `--printer` (required): The IP address of the printer.
- `--port` (optional): The port number of the printer. The default is `9100`.
- `--copies` (optional): The number of copies to print. The default is `1`.
- `--timeout` (optional): Timeout in seconds for the socket connection. The default is `10` seconds.

### Example Usage from Console

```bash
ZPLPrintDriver.exe --path "C:\path\to\your\file.zpl" --printer "192.168.1.100" --port 9100 --copies 2 --timeout 10
```

### Explanation of the Example

- `--path`: The ZPL file to print is located at `C:\path\to\your\file.zpl`.
- `--printer`: The printer is located at the IP address `192.168.1.100`.
- `--port`: The printer's port is `9100` (the default for most networked Zebra printers).
- `--copies`: The command prints 2 copies of the label.
- `--timeout`: The connection will time out if no response is received within 10 seconds.

## Using from Other Programming Languages

### Python Example

You can invoke the `ZPLPrintDriver.exe` from Python using the `subprocess` module.

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

In C#, you can use the `Process` class to run the executable.

```csharp
using System;
using System.Diagnostics;

class Program
{
    static void Main(string[] args)
    {
        // Create a new process
        Process process = new Process();
        process.StartInfo.FileName = "ZPLPrintDriver.exe";
        process.StartInfo.Arguments = "--path \"C:\\path\\to\\your\\file.zpl\" --printer \"192.168.1.100\" --port 9100 --copies 1 --timeout 10";
        process.StartInfo.RedirectStandardOutput = true;
        process.StartInfo.UseShellExecute = false;
        process.StartInfo.CreateNoWindow = true;

        // Start the process
        process.Start();

        // Read the output
        string result = process.StandardOutput.ReadToEnd();
        Console.WriteLine(result);

        // Wait for the process to exit
        process.WaitForExit();
    }
}
```

### PHP Example

In PHP, you can use the `exec()` function to call the executable.

```php
<?php
// Command to execute the ZPL print driver
$command = "ZPLPrintDriver.exe --path \"C:\\path\\to\\your\\file.zpl\" --printer \"192.168.1.100\" --port 9100 --copies 1 --timeout 10";

// Execute the command and capture the output
$output = shell_exec($command);

// Print the output
echo $output;
?>
```

### Ruby Example

In Ruby, you can use the `system()` function to execute the command.

```ruby
# Command to run the ZPLPrintDriver.exe
command = 'ZPLPrintDriver.exe --path "C:\\path\\to\\your\\file.zpl" --printer "192.168.1.100" --port 9100 --copies 1 --timeout 10'

# Execute the command
system(command)
```

### Visual Basic (VBScript) Example

In Visual Basic, you can use the `Shell` function to call the executable.

```vbscript
Set objShell = WScript.CreateObject("WScript.Shell")

' Command to run ZPLPrintDriver.exe
command = "ZPLPrintDriver.exe --path ""C:\path\to\your\file.zpl"" --printer ""192.168.1.100"" --port 9100 --copies 1 --timeout 10"

' Execute the command
objShell.Run command, 0, True
```

### PowerShell Example

In PowerShell, you can run the executable using `Start-Process`.

```powershell
# Define the command
$command = "ZPLPrintDriver.exe --path 'C:\path\to\your\file.zpl' --printer '192.168.1.100' --port 9100 --copies 1 --timeout 10"

# Run the command
Start-Process -FilePath "cmd.exe" -ArgumentList "/c $command" -NoNewWindow -Wait
```

### WScript (Windows Script Host) Example

In WScript, you can run the command using the `Exec` method.

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

```javascript
const { exec } = require('child_process');

// Comando para ejecutar el ZPLPrintDriver.exe
const command = 'ZPLPrintDriver.exe --path "C:\\path\\to\\your\\file.zpl" --printer "192.168.1.100" --port 9100 --copies 1 --timeout 10';

// Ejecutar el comando
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

## Error Handling

In case of errors (e.g., invalid printer IP, file not found, etc.), the program will return a JSON response with the following format:

```json
{
  "result": "Fail",
  "error": "Description of the error"
}
```

On success, the output will look like this:

```json
{
  "result": "Success",
  "path": "C:\\path\\to\\your\\file.zpl",
  "printer": "192.168.1.100",
  "port": 9100,
  "copies": 2
}
```

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
