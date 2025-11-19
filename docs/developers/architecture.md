# System Architecture

This document provides a comprehensive overview of the PipelineDataUpload system's architecture, design patterns, and technical implementation.

## 🏗️ Architecture Overview

PipelineDataUpload follows a traditional **N-Tier Architecture** with clear separation of concerns across multiple layers.

### High-Level Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Presentation  │    │   Business      │    │   Data Access   │
│     Layer       │◄──►│   Logic Layer   │◄──►│     Layer       │
│                 │    │                 │    │                 │
│ • ASPX Pages    │    │ • Services      │    │ • Database      │
│ • User Controls │    │ • Validation    │    │ • Stored Procs  │
│ • Master Pages  │    │ • Workflows     │    │ • Views         │
└─────────────────┘    └─────────────────┘    └─────────────────┘
       │                       │                       │
       └───────────────────────┼───────────────────────┘
                               │
                    ┌─────────────────┐
                    │   Infrastructure │
                    │     Layer       │
                    │                 │
                    │ • IIS Server    │
                    │ • SQL Server    │
                    │ • File System   │
                    │ • Email Service │
                    └─────────────────┘
```

## 📋 Layer Details

### 1. Presentation Layer

#### Technologies Used
- **ASP.NET Web Forms 4.8**
- **Bootstrap 4/5** for responsive UI
- **jQuery 3.7.0** for client-side interactions
- **Custom CSS** with dark mode support
- **TypeScript/React** for calendar components

#### Key Components
- **Master Pages**: `Site.Master` for consistent layout
- **Content Pages**: Individual ASPX pages for specific functions
- **User Controls**: Reusable UI components
- **Themes**: Light/dark mode support

#### Page Structure
```csharp
// Typical ASPX page structure
<%@ Page Title="Dashboard" Language="C#" MasterPageFile="~/Site.Master"
    AutoEventWireup="true" CodeBehind="Dashboard.aspx.cs"
    Inherits="PipelineDataUpload.Dashboard" %>

<asp:Content ID="Content1" ContentPlaceHolderID="MainContent" runat="server">
    <!-- Page-specific content -->
</asp:Content>
```

### 2. Business Logic Layer

#### Core Services
- **ApprovalService.cs**: Handles approval workflows
- **NotificationHelper.cs**: Manages notifications and alerts
- **DatabaseHelper.cs**: Database operations abstraction
- **CustomRoleProvider.cs**: Role-based access control

#### Design Patterns Used
- **Service Layer Pattern**: Centralized business logic
- **Repository Pattern**: Data access abstraction
- **Factory Pattern**: Object creation management
- **Singleton Pattern**: Shared resource management

#### Key Classes

**ApprovalService**
```csharp
public static class ApprovalService
{
    // Static methods for approval operations
    public static int SubmitForApproval(...) { ... }
    public static bool ApproveChange(...) { ... }
    public static bool RejectChange(...) { ... }
}
```

**NotificationHelper**
```csharp
public static class NotificationHelper
{
    // Notification management methods
    public static void CreateNotification(...) { ... }
    public static DataTable GetUserNotifications(...) { ... }
}
```

### 3. Data Access Layer

#### Database Design
- **SQL Server** as primary database
- **ADO.NET** for data access
- **Stored Procedures** for complex operations
- **Views** for data presentation

#### Connection Management
```csharp
// DatabaseHelper.cs pattern
public static class DatabaseHelper
{
    private static readonly string ConnectionString =
        ConfigurationManager.ConnectionStrings["DefaultConnection"].ConnectionString;

    public static SqlConnection GetConnection()
    {
        return new SqlConnection(ConnectionString);
    }
}
```

#### Key Tables
- **Users**: User account information
- **Pipeline**: Main pipeline data storage
- **PendingDataChanges**: Approval workflow data
- **ActivityLog**: System activity tracking
- **UserRoles/Roles**: Role-based permissions

## 🔄 Application Flow

### User Authentication Flow
```
1. User visits LoginPage.aspx
2. Credentials submitted to server
3. CustomRoleProvider validates user
4. Session created with user info
5. Redirect to Dashboard.aspx
6. Role-based menu items displayed
```

### Data Upload Flow
```
1. User selects Excel file on Upload.aspx
2. File uploaded to server (~/Temp/)
3. NPOI processes Excel file
4. Data validated and transformed
5. Records inserted into Pipeline table
6. Approval workflow initiated
7. User notified of results
```

### Approval Workflow
```
1. Data submitted for approval
2. PendingDataChanges record created
3. Approvers notified via NotificationHelper
4. Approvers review on DataApprovals.aspx
5. Decision made (Approve/Reject)
6. Original submitter notified
7. Audit trail logged
```

## 🛡️ Security Architecture

### Authentication
- **Forms Authentication**: Cookie-based authentication
- **Session Management**: Server-side session storage
- **Password Security**: Proper hashing and salting
- **Account Lockout**: Brute force protection

### Authorization
- **Role-Based Access**: Admin, CreateModify, Standard roles
- **Page-Level Security**: Location-based authorization in Web.config
- **Method-Level Security**: Code-behind permission checks
- **Resource Protection**: File upload restrictions

### Data Protection
- **SQL Injection Prevention**: Parameterized queries
- **XSS Protection**: Input validation and encoding
- **CSRF Protection**: Anti-forgery tokens
- **Secure Communications**: HTTPS enforcement

## 📊 Data Flow Architecture

### Request Processing
```
HTTP Request → IIS → ASP.NET Pipeline → Page Lifecycle → Code-Behind → Database → Response
```

### File Upload Processing
```
File Upload → Server Validation → NPOI Processing → Data Transformation → Database Insert → Approval Queue
```

### Notification System
```
Event Trigger → NotificationHelper → Database Storage → Email Service → User Notification
```

## 🔧 Configuration Management

### Web.config Structure
```xml
<configuration>
  <connectionStrings>
    <add name="DefaultConnection" connectionString="..." />
  </connectionStrings>

  <appSettings>
    <add key="SmtpHost" value="smtp.gmail.com" />
    <add key="SmtpPort" value="587" />
    <!-- Other settings -->
  </appSettings>

  <system.web>
    <authentication mode="Forms">
      <forms loginUrl="LoginPage.aspx" />
    </authentication>
    <roleManager enabled="true" />
  </system.web>
</configuration>
```

### Environment-Specific Settings
- **Development**: Local database, debug mode
- **Staging**: Test database, limited features
- **Production**: Production database, full features

## 📈 Performance Considerations

### Database Optimization
- **Connection Pooling**: Efficient connection reuse
- **Query Optimization**: Proper indexing and query design
- **Caching Strategy**: Application-level data caching
- **Batch Operations**: Bulk insert/update operations

### Application Performance
- **ViewState Management**: Minimize ViewState size
- **Session Optimization**: Efficient session storage
- **Static Content**: Proper caching headers
- **CDN Integration**: External resource optimization

### Monitoring Points
- **Database Performance**: Query execution times
- **Memory Usage**: Application memory consumption
- **Error Rates**: Exception tracking and analysis
- **User Activity**: Usage pattern analysis

## 🔄 Scalability Design

### Horizontal Scaling
- **Stateless Design**: Session state management
- **Load Balancing**: Multiple server support
- **Database Clustering**: SQL Server clustering
- **Caching Layer**: Distributed caching support

### Vertical Scaling
- **Resource Optimization**: Memory and CPU usage
- **Database Tuning**: Query and index optimization
- **File Storage**: Efficient file handling
- **Background Processing**: Asynchronous operations

## 🧪 Testing Architecture

### Unit Testing
- **Framework**: MSTest/NUnit
- **Coverage**: Business logic and utilities
- **Mocking**: External dependencies (database, email)
- **CI Integration**: Automated test execution

### Integration Testing
- **Database Integration**: Data access layer testing
- **UI Testing**: Selenium WebDriver
- **API Testing**: HTTP endpoint validation
- **Performance Testing**: Load and stress testing

## 🚀 Deployment Architecture

### Development Environment
- **Local IIS Express**: Development server
- **Local SQL Server**: Development database
- **Source Control**: Git repository
- **Build Tools**: MSBuild

### Production Environment
- **IIS Web Server**: Production web server
- **SQL Server**: Production database
- **Load Balancer**: Traffic distribution
- **Monitoring Tools**: Application monitoring

## 📋 Error Handling Architecture

### Exception Management
- **Global Error Handler**: Application-level exception catching
- **Page-Level Handling**: Individual page error management
- **Database Errors**: Connection and query error handling
- **User-Friendly Messages**: Meaningful error display

### Logging Strategy
- **Application Logs**: System.Diagnostics.Debug
- **Database Logs**: ActivityLog table
- **Error Logs**: Structured error logging
- **Audit Trail**: Security and compliance logging

## 🔗 Integration Points

### External Systems
- **Email Service**: SMTP integration for notifications
- **File Storage**: Local file system for uploads
- **Authentication**: Active Directory integration (future)
- **Reporting**: SQL Server Reporting Services

### API Endpoints
- **NotificationHandler.ashx**: AJAX notification handling
- **Web Methods**: Server-side method calls
- **REST APIs**: Future API expansion points

## 🎯 Design Principles

### SOLID Principles
- **Single Responsibility**: Each class has one purpose
- **Open/Closed**: Open for extension, closed for modification
- **Liskov Substitution**: Subtypes are substitutable
- **Interface Segregation**: Client-specific interfaces
- **Dependency Inversion**: Depend on abstractions

### Clean Architecture
- **Dependency Direction**: Inner layers don't depend on outer layers
- **Use Case Driven**: Business logic drives design
- **Framework Independence**: Not tied to specific frameworks
- **Testability**: Easy to test all components

## 📚 Architectural Patterns Used

### Web Forms Specific Patterns
- **Page Controller**: ASPX pages as controllers
- **Template Method**: Master page inheritance
- **Observer Pattern**: Event handling system

### Enterprise Patterns
- **Repository Pattern**: Data access abstraction
- **Unit of Work**: Transaction management
- **Service Layer**: Business logic encapsulation
- **Dependency Injection**: Loose coupling

## 🔮 Future Architecture Considerations

### Microservices Migration
- **Service Decomposition**: Break down monolithic application
- **API Gateway**: Centralized API management
- **Containerization**: Docker support
- **Orchestration**: Kubernetes deployment

### Cloud Migration
- **Azure Integration**: Cloud service integration
- **Serverless Functions**: Event-driven processing
- **Managed Databases**: Azure SQL Database
- **CDN Integration**: Global content delivery

This architecture provides a solid foundation for the PipelineDataUpload system while maintaining flexibility for future enhancements and scalability requirements.
