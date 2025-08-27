# MCP Database Filesystem

English | [中文](README.md)

A simple and efficient MCP (Model Context Protocol) server providing multi-database access and filesystem operations.

## ✨ Key Features

### 🗄️ Multi-Database Support

#### SQL Server
- **SQL Query Execution** - Support for SELECT queries
- **SQL Command Execution** - Support for INSERT/UPDATE/DELETE operations
- **Table Schema Query** - Get detailed table structure information and field descriptions
- **Table Listing** - List all tables in the database

#### MySQL
- **MySQL Query Execution** - Support for MySQL SELECT queries
- **MySQL Command Execution** - Support for INSERT/UPDATE/DELETE operations
- **MySQL Table Schema Query** - Get detailed MySQL table structure information
- **MySQL Table Listing** - List all tables in MySQL database

#### Redis
- **Key-Value Operations** - GET/SET/DELETE key-value pairs
- **Key Management** - List keys matching patterns
- **Server Information** - Get Redis server status information
- **Expiration Settings** - Support key expiration time settings

### 📁 Filesystem Functions
- **File Reading** - Read file contents
- **File Writing** - Write content to files
- **Directory Listing** - List directory contents

### 🔒 Security Features
- SQL injection protection
- Filesystem access control
- Environment variable configuration
- Permission validation

### 🔄 Fault Tolerance
- **Graceful Degradation** - Any database connection failure doesn't affect other services
- **Dynamic Reconnection** - Support runtime reconnection to various databases
- **Status Monitoring** - Real-time monitoring of all database connection status

## 🚀 Quick Start

### 📋 Prerequisites

#### 1. Install ODBC Driver for SQL Server

**Windows:**
```bash
# Download and install Microsoft ODBC Driver 17 for SQL Server
# Visit: https://docs.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server
# Or use winget to install
winget install Microsoft.ODBCDriverforSQLServer
```

**macOS:**
```bash
# Install using Homebrew
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql17 mssql-tools
```

**Linux (Ubuntu/Debian):**
```bash
# Add Microsoft repository
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list

# Install driver
sudo apt-get update
sudo apt-get install msodbcsql17
```

#### 2. Verify ODBC Installation

```bash
# Windows
odbcad32.exe

# macOS/Linux
odbcinst -j
```

### 📦 Zero-Installation Usage (Recommended)

```bash
# Install uv (if not already installed)
pip install uv

# Run directly - no need to clone repository!
uvx mcp-db-filesystem@latest
```

### 🔧 Configuration

Add the following configuration to your MCP client (such as Claude Desktop, AugmentCode):

```json
{
  "mcpServers": {
    "mcp-db-filesystem": {
      "command": "uvx",
      "args": ["mcp-db-filesystem@latest"],
      "env": {
        // SQL Server Configuration (Optional)
        "MSSQL_SERVER": "localhost",
        "MSSQL_DATABASE": "your_database",
        "MSSQL_USERNAME": "your_username",
        "MSSQL_PASSWORD": "your_password",
        "MSSQL_USE_WINDOWS_AUTH": "true",
        "MSSQL_PORT": "1433",
        "MSSQL_DRIVER": "ODBC Driver 17 for SQL Server",
        "MSSQL_CONNECTION_TIMEOUT": "30",
        "MSSQL_COMMAND_TIMEOUT": "30",
        "MSSQL_POOL_SIZE": "5",
        "MSSQL_MAX_OVERFLOW": "10",
        "MSSQL_TRUST_SERVER_CERTIFICATE": "true",
        "MSSQL_ENCRYPT": "false",
        "MSSQL_MULTIPLE_ACTIVE_RESULT_SETS": "true",
        "MSSQL_APPLICATION_NAME": "MCP-Db-Filesystem",

        // MySQL Configuration (Optional)
        "MYSQL_HOST": "localhost",
        "MYSQL_PORT": "3306",
        "MYSQL_DATABASE": "your_mysql_database",
        "MYSQL_USERNAME": "your_mysql_username",
        "MYSQL_PASSWORD": "your_mysql_password",
        "MYSQL_CHARSET": "utf8mb4",
        "MYSQL_CONNECTION_TIMEOUT": "30",
        "MYSQL_POOL_SIZE": "5",
        "MYSQL_MAX_OVERFLOW": "10",

        // Redis Configuration (Optional)
        "REDIS_HOST": "localhost",
        "REDIS_PORT": "6379",
        "REDIS_DB": "0",
        "REDIS_PASSWORD": "your_redis_password",
        "REDIS_SOCKET_TIMEOUT": "30",
        "REDIS_CONNECTION_TIMEOUT": "30",
        "REDIS_MAX_CONNECTIONS": "10",

        // Filesystem Configuration
        "FS_ALLOWED_PATHS": "*",
        "FS_ALLOWED_EXTENSIONS": "*.*",
        "FS_MAX_FILE_SIZE": "1073741824",
        "FS_ENABLE_WRITE": "true",
        "FS_ENABLE_DELETE": "true",
        "FS_IGNORE_FILE_LOCKS": "false",

        // Security Configuration
        "SECURITY_ENABLE_SQL_INJECTION_PROTECTION": "true",
        "SECURITY_MAX_QUERY_LENGTH": "10000",
        "SECURITY_ENABLE_QUERY_LOGGING": "true",
        "SECURITY_LOG_SENSITIVE_DATA": "false",

        // Server Configuration
        "SERVER_LOG_LEVEL": "INFO",
        "SERVER_DEBUG": "false"
      }
    }
  }
}
```

## 🛠️ Available Tools

### Database Tools

- `sql_query` - Execute SQL SELECT queries
- `sql_execute` - Execute SQL INSERT/UPDATE/DELETE commands
- `list_tables` - List all tables in the database
- `get_table_schema` - Get table structure information

### Filesystem Tools

- `read_file` - Read file contents
- `write_file` - Write file contents
- `list_directory` - List directory contents
- `delete_file` - Delete files (requires confirmation)
- `create_directory` - Create directories

## 📋 Environment Variables

### SQL Server Configuration
- `MSSQL_SERVER` - SQL Server address
- `MSSQL_DATABASE` - Database name
- `MSSQL_USERNAME` - Username
- `MSSQL_PASSWORD` - Password
- `MSSQL_USE_WINDOWS_AUTH` - Whether to use Windows authentication
- `MSSQL_PORT` - SQL Server port (default 1433)
- `MSSQL_DRIVER` - ODBC driver name
- `MSSQL_CONNECTION_TIMEOUT` - Connection timeout (seconds)
- `MSSQL_COMMAND_TIMEOUT` - Command timeout (seconds)
- `MSSQL_POOL_SIZE` - Connection pool size
- `MSSQL_MAX_OVERFLOW` - Maximum overflow connections
- `MSSQL_TRUST_SERVER_CERTIFICATE` - Whether to trust server certificate
- `MSSQL_ENCRYPT` - Whether to encrypt connection
- `MSSQL_MULTIPLE_ACTIVE_RESULT_SETS` - Whether to enable multiple active result sets
- `MSSQL_APPLICATION_NAME` - Application name

### MySQL Configuration
- `MYSQL_HOST` - MySQL server address
- `MYSQL_PORT` - MySQL port (default 3306)
- `MYSQL_DATABASE` - MySQL database name
- `MYSQL_USERNAME` - MySQL username
- `MYSQL_PASSWORD` - MySQL password
- `MYSQL_CHARSET` - Character set (default utf8mb4)
- `MYSQL_CONNECTION_TIMEOUT` - Connection timeout (seconds)
- `MYSQL_POOL_SIZE` - Connection pool size
- `MYSQL_MAX_OVERFLOW` - Maximum overflow connections

### Redis Configuration
- `REDIS_HOST` - Redis server address
- `REDIS_PORT` - Redis port (default 6379)
- `REDIS_DB` - Redis database number (default 0)
- `REDIS_PASSWORD` - Redis password (optional)
- `REDIS_SOCKET_TIMEOUT` - Socket timeout (seconds)
- `REDIS_CONNECTION_TIMEOUT` - Connection timeout (seconds)
- `REDIS_MAX_CONNECTIONS` - Maximum connections

### Filesystem Configuration
- `FS_ALLOWED_PATHS` - Allowed access paths (`*` means all paths)
- `FS_ALLOWED_EXTENSIONS` - Allowed file extensions (`*.*` means all files)
- `FS_MAX_FILE_SIZE` - Maximum file size (bytes)
- `FS_ENABLE_WRITE` - Enable write operations
- `FS_ENABLE_DELETE` - Enable delete operations
- `FS_IGNORE_FILE_LOCKS` - Whether to ignore file locks

## 🔧 Development

### Local Development

```bash
# Clone repository
git clone https://github.com/ppengit/mcp-db-filesystem.git
cd mcp-db-filesystem

# Install dependencies
uv sync

# Run server
uv run python -m mcp_db_filesystem server
```

### Testing

```bash
# Run tests
uv run pytest

# Run specific tests
uv run pytest tests/test_database.py
```

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions welcome! Please submit Issues or Pull Requests.

## ❓ FAQ

### Q: Getting "No module named 'pyodbc'" error
A: Please ensure ODBC Driver for SQL Server is installed, see Prerequisites section above.

### Q: Getting "Data source name not found" error
A: Check if `DB_SERVER` configuration is correct and ensure SQL Server service is running.

### Q: Connection timeout or connection refused
A:
1. Check if SQL Server has TCP/IP protocol enabled
2. Verify firewall settings allow connections to SQL Server port (default 1433)
3. Confirm username and password are correct

### Q: Filesystem operations denied
A: Check `FS_ALLOWED_PATHS` and `FS_ALLOWED_EXTENSIONS` configuration to ensure paths and file types are allowed.

## 📞 Support

- GitHub Issues: [https://github.com/ppengit/mcp-db-filesystem/issues](https://github.com/ppengit/mcp-db-filesystem/issues)

## 🔄 Changelog

### v1.0.1
- 🎉 First stable release
- ✨ Complete SQL Server database support
- 📁 Comprehensive filesystem operations
- 🔒 Enhanced security features
- 📝 Improved error handling and logging
- 🚀 Simplified architecture focused on core functionality

---

**Note**: This version focuses on core functionality stability and reliability, providing a simple and efficient MCP server experience.
