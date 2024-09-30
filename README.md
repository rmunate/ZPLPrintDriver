## ZPL Print Universal Driver (Windows)

`ZPLPrintDriver.exe` is a versatile command-line tool for sending ZPL (Zebra Programming Language) code to network-connected and USB-connected Zebra printers. It is designed for easy integration into various programming environments that support console command execution.

## Features

- Send ZPL code directly from a file to a Zebra printer over the network.
- Supports specifying the printer's IP address and port.
- Allows printing multiple copies of the label.
- Configurable timeout for network operations.
- Cross-language compatibility through easy-to-use command-line execution.

## Usage

You can run the program directly from the command line by providing the necessary arguments.

### Command Line Arguments

#### Print Over Network

- `--path` (required): Full path to the ZPL file you want to send to the printer.
- `--printer` (required): The IP address of the Zebra printer.
- `--port` (optional): Printer port number. Default is `9100`.
- `--copies` (optional): Number of copies to print. Default is `1`.
- `--timeout` (optional): Timeout in seconds for the network connection. Default is `10` seconds.

```bash
ZPLPrintDriver.exe --path "C:\path\to\your\file.zpl" --printer "192.168.1.100" --port 9100 --copies 2 --timeout 10
```

#### Print Over USB

To print using a USB connection, you need to obtain the vendorId and productId from your printer's properties. Use these values in the format USB:vendorId:productId. For example:

- `--path` (required): Full path to the ZPL file you want to send to the printer.
- `--usb` (required): Indicates that the operation will use USB.
- `--vendor_id` (required): Value extracted from the hardware identifier properties.
- `--product_id` (required): Value extracted from the hardware identifier properties.

![ExtractData](https://github.com/user-attachments/assets/7cae9537-80f7-4423-8d96-984648669c25)

Where to find values: USB\VID_`0A5F`&PID_`0081`, vendor_id and product_id, respectively.

```bash
ZPLPrintDriver.exe --path="example.zpl" --usb --vendor_id="0A5F" --product_id="0081"
```

---

## Using from Various Programming Languages

### Python Example (Network)

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

### Python Example (USB)

In Python, you can use the `subprocess` module to call `ZPLPrintDriver.exe`.

```python
import subprocess

# Command to run the executable with arguments
command = [
    "ZPLPrintDriver.exe",
    "--path", "C:\\path\\to\\your\\file.zpl",
    "--usb",
    "--vendor_id", "0A5F",
    "--product_id", "0081"
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

## Successful Output

For successful execution, the output will look like this:

```json
{
    "result": "Success",
    "path": "example.zpl",
    "copies": 1,
    "port": 9100,
    "timeout": 10,
    "printer": null,
    "usb": true,
    "vendor_id": "0A5F",
    "product_id": "0081"
}
```

---

## License

This project is under the [MIT License](https://choosealicense.com/licenses/mit/).

🌟 Support My Projects! 🚀

[![Become a Sponsor](https://img.shields.io/badge/-Become%20a%20Sponsor-blue?style=for-the-badge&logo=github)](https://github.com/sponsors/rmunate)

Make any contributions you see fit; the code is entirely yours. Together, we can do amazing things and improve the world of development. Your support is invaluable. ✨

If you have ideas, suggestions, or just want to collaborate, we are open to everything! Join our community and be part of our journey to success! 🌐👩‍💻👨‍💻
