# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.4] - 2025-08-28

### Fixed
- **Critical SQL Server Connection Issue**: Fixed ODBC connection string format for SQL Server
  - Changed `TrustServerCertificate` parameter format from numeric (1/0) to text (yes/no)
  - Improved compatibility with different versions of ODBC Driver 17 for SQL Server
  - Only add `TrustServerCertificate` parameter when explicitly needed
  - Enhanced connection string building logic for better ODBC compatibility

### Enhanced
- **Connection Diagnostics**: Improved error handling and diagnostics for SQL Server connections
- **ODBC Compatibility**: Better support for various ODBC driver versions and configurations
- **Connection Reliability**: More robust connection string generation

### Technical Details
- Fixed issue where `TrustServerCertificate=1` was not recognized by some ODBC driver versions
- Changed to use `TrustServerCertificate=yes` format for better compatibility
- Conditional parameter inclusion to avoid unsupported parameter errors
- Enhanced connection string validation and error reporting

This resolves connection issues where SQL Server databases were configured correctly but
MCP tools couldn't establish connections due to ODBC parameter format incompatibility.

## [1.1.3] - 2025-08-27

### Fixed
- **File Operations UX**: Changed default behavior for file operations to be more user-friendly
  - `write_file` now defaults to allowing file overwrite (no confirmation required)
  - `delete_file` now defaults to allowing file deletion (no confirmation required)
  - Users can still set `confirm: false` to require explicit confirmation

### Enhanced
- **File Deletion Robustness**: Improved file deletion with enhanced error handling
  - Added retry mechanism for permission errors
  - Automatic permission fixing for locked files
  - Better error messages for common issues (file in use, access denied)
  - Support for Chinese and Unicode filenames

### Changed
- **Default Behavior**: File operations are now more streamlined
  - `write_file`: `confirm` parameter defaults to `true` (allow overwrite)
  - `delete_file`: `confirm` parameter defaults to `true` (allow deletion)
  - Only when explicitly set to `false` will confirmation be required

### Technical Improvements
- Enhanced file deletion with multiple retry attempts
- Improved permission handling on Windows systems
- Better error categorization and user feedback
- Comprehensive testing for all file operation scenarios

## [1.1.2] - 2025-08-26

### Added
- **File Deletion**: Added `delete_file` tool for file deletion with confirmation requirement
- **Directory Creation**: Added `create_directory` tool for creating directories
- **Complete Filesystem Operations**: Now supports full CRUD operations for files and directories

### Fixed
- **Critical Bug**: Fixed missing file deletion functionality that was implemented but not exposed
- **Tool Completeness**: Ensured all implemented tools are properly registered and accessible
- **Documentation**: Updated README with complete tool listings and configuration options

### Enhanced
- **Comprehensive Testing**: Added thorough testing for all 22 tools across all categories
- **Error Handling**: Improved error handling and user feedback for all filesystem operations
- **Configuration Documentation**: Added complete filesystem configuration options

### Tools Summary
- **SQL Server Tools**: 4 tools (sql_query, sql_execute, get_table_schema, list_tables)
- **MySQL Tools**: 4 tools (mysql_query, mysql_execute, mysql_get_table_schema, mysql_list_tables)
- **Redis Tools**: 5 tools (redis_get, redis_set, redis_delete, redis_keys, redis_info)
- **Database Management**: 4 tools (database_status, database_reconnect, mysql_reconnect, redis_reconnect)
- **Filesystem Tools**: 5 tools (read_file, write_file, list_directory, delete_file, create_directory)

**Total: 22 fully functional tools**

## [1.1.1] - 2025-08-26

### Changed
- **BREAKING**: SQL Server environment variables renamed from `DB_XXX` to `MSSQL_XXX` for consistency
  - `DB_SERVER` → `MSSQL_SERVER`
  - `DB_DATABASE` → `MSSQL_DATABASE`
  - `DB_USERNAME` → `MSSQL_USERNAME`
  - `DB_PASSWORD` → `MSSQL_PASSWORD`
  - `DB_USE_WINDOWS_AUTH` → `MSSQL_USE_WINDOWS_AUTH`
  - `DB_PORT` → `MSSQL_PORT`
  - `DB_DRIVER` → `MSSQL_DRIVER`
  - `DB_CONNECTION_TIMEOUT` → `MSSQL_CONNECTION_TIMEOUT`
  - `DB_COMMAND_TIMEOUT` → `MSSQL_COMMAND_TIMEOUT`
  - `DB_POOL_SIZE` → `MSSQL_POOL_SIZE`
  - `DB_MAX_OVERFLOW` → `MSSQL_MAX_OVERFLOW`
  - `DB_TRUST_SERVER_CERTIFICATE` → `MSSQL_TRUST_SERVER_CERTIFICATE`
  - `DB_ENCRYPT` → `MSSQL_ENCRYPT`
  - `DB_MULTIPLE_ACTIVE_RESULT_SETS` → `MSSQL_MULTIPLE_ACTIVE_RESULT_SETS`
  - `DB_APPLICATION_NAME` → `MSSQL_APPLICATION_NAME`

### Added
- Complete configuration examples with all available environment variables
- Enhanced documentation with comprehensive configuration options

### Migration Guide
Update your environment variables from `DB_XXX` to `MSSQL_XXX` format:
```bash
# Old format (deprecated)
DB_SERVER=localhost
DB_DATABASE=mydb

# New format (required)
MSSQL_SERVER=localhost
MSSQL_DATABASE=mydb
```

## [1.1.0] - 2025-08-26

### Added
- **MySQL Support**: Full MySQL database integration with connection management
  - `mysql_query`: Execute MySQL SELECT queries
  - `mysql_execute`: Execute MySQL INSERT/UPDATE/DELETE operations
  - `mysql_get_table_schema`: Get MySQL table schema information
  - `mysql_list_tables`: List all tables in MySQL database
  - `mysql_reconnect`: Reconnect to MySQL database
- **Redis Support**: Complete Redis integration with key-value operations
  - `redis_get`: Get value by key
  - `redis_set`: Set key-value pairs with optional expiration
  - `redis_delete`: Delete one or more keys
  - `redis_keys`: Get keys matching pattern
  - `redis_info`: Get Redis server information
  - `redis_reconnect`: Reconnect to Redis server
- **Enhanced Database Status**: Updated `database_status` tool to show all database connections
- **Graceful Degradation**: All database services fail gracefully without affecting other services

### Changed
- **Multi-Database Architecture**: Now supports SQL Server, MySQL, and Redis simultaneously
- **Enhanced Configuration**: Added MySQL and Redis configuration options
- **Improved Error Handling**: Better error messages and connection status reporting
- **Updated Dependencies**: Added `pymysql>=1.1.0` and `redis>=5.0.0`

### Configuration
New environment variables for MySQL:
- `MYSQL_HOST`, `MYSQL_PORT`, `MYSQL_DATABASE`
- `MYSQL_USERNAME`, `MYSQL_PASSWORD`
- `MYSQL_CHARSET`, `MYSQL_CONNECTION_TIMEOUT`
- `MYSQL_POOL_SIZE`, `MYSQL_MAX_OVERFLOW`

New environment variables for Redis:
- `REDIS_HOST`, `REDIS_PORT`, `REDIS_DB`
- `REDIS_PASSWORD`
- `REDIS_SOCKET_TIMEOUT`, `REDIS_CONNECTION_TIMEOUT`
- `REDIS_MAX_CONNECTIONS`

## [1.0.4] - 2025-08-26

### Changed
- **BREAKING**: Project renamed from `mcp-sqlserver-filesystem` to `mcp-db-filesystem`
- Package name changed from `mcp_sqlserver_filesystem` to `mcp_db_filesystem`
- Updated all documentation and references to reflect new name
- Repository moved to https://github.com/ppengit/mcp-db-filesystem

### Migration Guide
- Update import statements from `mcp_sqlserver_filesystem` to `mcp_db_filesystem`
- Update command line usage from `mcp-sqlserver-filesystem` to `mcp-db-filesystem`
- Update pip install command to `pip install mcp-db-filesystem`

## [1.0.3] - 2025-08-26

### Added
- Database reconnection mechanism with `database_reconnect` tool
- Database status checking with `database_status` tool
- Graceful database connection failure handling
- Dynamic tool availability based on database connection status

### Changed
- **BREAKING**: Database connection failures no longer crash the MCP server
- MCP server now starts successfully even when database is unavailable
- Database tools are dynamically hidden when database is not available
- Improved error messages for database connection issues

### Removed
- All UI-related code and parameters (`show_ui`, `confirm_ui`, etc.)
- UI references in tool descriptions
- Unused UI confirmation dialogs

### Fixed
- MCP server startup failure when SQL Server is unavailable
- Database connection error handling
- Tool availability logic

## [1.0.2] - 2025-08-25

### Added
- Enhanced database connection parameters
- Improved error handling and logging
- Cross-platform compatibility improvements

### Changed
- Updated database connection string format
- Improved security configurations

## [1.0.1] - 2025-08-24

### Added
- Initial release
- SQL Server database operations
- Filesystem operations
- Security features
- Environment variable configuration

### Features
- SQL query execution (SELECT, INSERT, UPDATE, DELETE)
- Table schema inspection
- File read/write operations
- Directory listing
- SQL injection protection
- Filesystem access control
