## TerminalWrapper for vscode extension

1. **Class `TerminalWrapper`**:
   - This class is designed to wrap terminal-related functionality.
   - It provides methods for executing commands in a terminal and handling the results.

2. **Class Properties**:
   - `executeResultFileName`: A string containing the name of the log file for command execution results.
   - `executeLogFileName`: A string containing the name of the log file for command execution details.
   - `setEncodingUtf8`: A string representing a PowerShell command to set the output encoding to UTF-8.

3. **Constructor**:
   - The constructor initializes the following properties:
     - `executeLogFilePath`: A path to the log file where command execution details are stored.
     - `executeResultFilePath`: A path to the file where the execution result (1 or 0) is recorded.
     - `outputPathLog`: The base directory where log files will be saved.
     - `terminalName`: The name of the terminal to be used.

4. **Class Methods**:
    - `executeCommand(command: string, isLogging: boolean): Promise<boolean>`: 
        - An asynchronous method to execute a command in the terminal. If isLogging is true, the command and its result will be logged. The method returns a Promise that resolves to true or false depending on the success of the command execution.
