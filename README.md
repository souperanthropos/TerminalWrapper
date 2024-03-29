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
    - `executeCommandWithoutLog(command: string): Promise<vscode.TerminalExitStatus>`:
        - This method executes a command in the specified terminal without logging the details.
        - It first checks if a terminal with the given name exists. If not, it creates a new one.
        - The method shows the terminal and sends the provided `command` to it.
        - After executing the command, it sends an exit command (`; exit`) to close the terminal.
        - The method returns a promise that resolves with the terminal's exit status or rejects with an error message if the status is undefined.
	- `executeCommand(command: string): Promise<boolean>`:
		- This method executes a command in the specified terminal.
		- If the terminal with the given name does not exist, it creates a new one.
		- The command is executed with the following steps:
			- `$share = ${this.setEncodingUtf8} ${command} | Tee-Object -file ${this.executeLogFilePath};`: The command is executed, and its output is logged to the `executeLogFilePath`.
			- `if($?){'1' > ${this.executeResultFilePath}}else{'0' > ${this.executeResultFilePath}};`: The result of the command execution (1 for success, 0 for failure) is recorded in the `executeResultFilePath`.
			- `exit`: The terminal is closed.
		- Handling Terminal Closure:
			- When the terminal is closed, the `onDidCloseTerminal` event is triggered.
			- The method reads the content of the `executeResultFilePath`.
			- If the terminal exit status is defined, it resolves the promise with `true` or `false` based on the read status.
			- If the terminal exit status is undefined, it rejects the promise with the message "Terminal exited with undefined status."
