# Developer Guide

Technical documentation for developers working with PipelineDataUpload.

## 🛠️ Development Environment

### Prerequisites
- Visual Studio 2019+ with ASP.NET workload
- .NET Framework 4.8
- SQL Server 2016+ or SQL Server Express
- IIS 7.0+

### Getting Started
1. Clone the private repository
2. Open the solution file in Visual Studio
3. Configure database connection in Web.config
4. Restore NuGet packages
5. Run database setup scripts

## 🏗️ Architecture Overview

PipelineDataUpload follows a three-tier architecture:
- **Presentation Layer**: ASP.NET Web Forms with Bootstrap UI
- **Business Logic Layer**: C# services and business components
- **Data Access Layer**: SQL Server with stored procedures

## 📁 Project Structure

```
PipelineDataUpload/
├── Pages/              # Web Form pages
├── App_Code/           # Business logic and services
├── App_Data/           # Database files and backups
├── Content/            # CSS and static assets
├── Scripts/            # JavaScript and TypeScript
└── Properties/         # Assembly information
```

## 🔧 Key Components

### User Management
- **CustomRoleProvider**: Role-based authentication
- **UserService**: User CRUD operations
- **PermissionService**: Access control logic

### Data Management
- **UploadService**: File processing and validation
- **DynamicQueryBuilder**: Query generation
- **DatabaseHelper**: Database operations

### Workflow Management
- **ApprovalService**: Approval process logic
- **NotificationHelper**: Alert system
- **Calendar Widget**: Event management

## 📋 Database Schema

The application uses SQL Server with the following key tables:
- Users and Roles
- PipelineData
- Approvals and Workflow
- Notifications
- Audit Logs

## 🚀 Deployment

1. Build the application in Release mode
2. Configure IIS application pool
3. Set up database connection strings
4. Configure SSL certificates
5. Test all functionality

## 🧪 Testing

- Unit tests for business logic
- Integration tests for database operations
- UI tests for critical user workflows

## 📚 Additional Resources

- Review the [User Guide](../users/README.md) for functionality understanding
- Check the [Stakeholder Guide](../stakeholders/README.md) for business requirements
