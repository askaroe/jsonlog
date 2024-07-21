# jsonlog

`jsonlog` is a simple JSON-based logging library for Go. It supports different logging levels and writes log messages in JSON format. This library ensures that logs are easy to parse and understand, making it ideal for applications that require structured logging.

## Features

- Multiple log levels: INFO, ERROR, FATAL, and OFF.
- Log messages include a timestamp, log level, message, and optional properties.
- Error logs include a stack trace.
- Thread-safe logging.

## Installation

To install the package, use `go get`:

```sh
go get github.com/askaroe/jsonlog
```

Replace `github.com/yourusername/jsonlog` with the actual path to your package.

## Usage

Here's how you can use the `jsonlog` package in your Go project.

### Example

```go
package main

import (
	"errors"
	"os"

	"github.com/askaroe/jsonlog"
)

func main() {
	// Create a new logger instance that writes to standard output
	logger := jsonlog.New(os.Stdout, jsonlog.LevelInfo)

	// Log an informational message
	logger.PrintInfo("Application started", nil)

	// Log an error message with additional properties
	logger.PrintError(errors.New("an error occurred"), map[string]string{"error_code": "123"})

	// Log a fatal error message and exit the program
	logger.PrintFatal(errors.New("a fatal error occurred"), nil)
}
```

### Log Levels

- `LevelInfo`: Logs informational messages.
- `LevelError`: Logs error messages.
- `LevelFatal`: Logs fatal error messages and exits the program.
- `LevelOff`: Disables logging.

### Methods

- `New(out io.Writer, minLevel Level) *Logger`: Creates a new logger instance.
- `PrintInfo(message string, properties map[string]string)`: Logs an informational message.
- `PrintError(err error, properties map[string]string)`: Logs an error message.
- `PrintFatal(err error, properties map[string]string)`: Logs a fatal error message and exits the program.
- `Write(message []byte) (n int, err error)`: Logs a message with the error level. This method satisfies the `io.Writer` interface.

### Structs

- `Logger`: Represents a logger with a minimum log level and an output destination.

### Usage with Different Output Destinations

You can log to different output destinations such as files, network connections, or any other `io.Writer`.

#### Example: Logging to a File

```go
package main

import (
	"errors"
	"os"

	"github.com/askaroe/jsonlog"
)

func main() {
	file, err := os.Create("logfile.json")
	if err != nil {
		panic(err)
	}
	defer file.Close()

	// Create a new logger instance that writes to a file
	logger := jsonlog.New(file, jsonlog.LevelInfo)

	// Log an informational message
	logger.PrintInfo("Application started", nil)

	// Log an error message with additional properties
	logger.PrintError(errors.New("an error occurred"), map[string]string{"error_code": "123"})

	// Log a fatal error message and exit the program
	logger.PrintFatal(errors.New("a fatal error occurred"), nil)
}
```

## Contributing

Contributions are welcome! Feel free to submit a pull request or open an issue to discuss improvements and new features.

## Acknowledgments

- [Go](https://golang.org/) programming language.