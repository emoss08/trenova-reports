# RPTMeta - Report Template Specification

RPTMeta is a YAML-based specification for defining enterprise-grade report templates. It provides a structured way to define SQL reports with variables, caching strategies, and scheduling capabilities.

## 🚀 Features

- Declarative report definitions using YAML
- Variable system with type checking and validation
- Built-in caching configuration
- Report scheduling support
- SQL query templating with variable interpolation
- Comprehensive metadata and versioning
- Tag-based organization

## 📋 Schema Structure

An RPTMeta file consists of three main sections:

1. Report Metadata
2. Variables Definition
3. SQL Query Template

### Basic Example

```yaml
report:
  title: "Get Workers with Expired Licenses"
  description: "Identifies workers whose licenses have expired."
  version: 1
  tags:
    - "Compliance"
    - "Workers"
  caching:
    isCachable: true
    cacheDuration: 600
  scheduling:
    isScheduled: false

variables:
  - name: "workerStatus"
    placeholder: "${workerStatus}"
    type: "string"
    default: "Active"
    description: "Status of workers to include in the report."
    isRequired: true
    allowedValues: ["Active", "Inactive"]

sql: |
  SELECT "w"."first_name", "w"."last_name"
  FROM "workers" AS "w"
  WHERE "w"."status" = ${workerStatus};
```

## 🏗️ Schema Reference

### Report Section

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| title | string | Yes | Report title |
| description | string | Yes | Detailed description of the report's purpose |
| version | integer | Yes | Report template version |
| tags | string[] | No | Array of tags for categorization |
| caching | object | No | Caching configuration |
| scheduling | object | No | Scheduling configuration |

### Variables Section

Each variable can have the following properties:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| name | string | Yes | Variable identifier |
| placeholder | string | Yes | SQL placeholder (format: ${name}) |
| type | string | Yes | Data type (string, integer, float, boolean, date, datetime) |
| default | any | No | Default value |
| description | string | Yes | Variable description |
| isRequired | boolean | No | Whether the variable is mandatory |
| allowedValues | array | No | List of valid values |

### SQL Section

The SQL section contains the parameterized query template. Variables are referenced using the `${variableName}` syntax.

## 📝 File Naming Convention

RPTMeta files should use the `.rptmeta.yaml` extension. Example:

```
workers.rptmeta.yaml
```

## 🔧 Variable Types

Supported variable types:

- `string`: Text values
- `integer`: Whole numbers
- `float`: Decimal numbers
- `boolean`: True/false values
- `date`: Date values (YYYY-MM-DD)
- `datetime`: Date and time values

## 🚦 Caching Configuration

```yaml
caching:
  isCachable: true    # Enable/disable caching
  cacheDuration: 600  # Cache duration in seconds
```

## ⏰ Scheduling Configuration

```yaml
scheduling:
  isScheduled: true           # Enable/disable scheduling
  schedule: "0 0 * * *"      # Cron expression
```

## 🔒 Security Considerations

1. All SQL queries are validated for:
   - SQL injection prevention
   - Proper variable usage
   - Query structure
   - Maximum length limits

2. Variables are validated for:
   - Type safety
   - Allowed values
   - Required fields

## 🚀 Getting Started

1. Create a new file with `.rptmeta.yaml` extension
2. Define the report metadata
3. Specify required variables
4. Write the SQL query template
5. Validate using the provided tools

## 📊 Example Use Cases

1. Compliance Reports:
   - License expiration tracking
   - Certification monitoring
   - Audit reports

2. Operational Reports:
   - Worker status reports
   - Equipment maintenance schedules
   - Inventory tracking

3. Analytics Reports:
   - Performance metrics
   - Trend analysis
   - KPI tracking

## 🛠️ Development Tools

The RPTMeta ecosystem includes:

- Schema validator
- SQL query validator
- Template parser
- Report generator

## 🤝 Contributing

Contributions are welcome! Please read our contributing guidelines and submit pull requests to our repository.

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.
