# Getting Started

Welcome to PipelineDataUpload! This guide will help you get up and running quickly.

## 🎯 What is PipelineDataUpload?

PipelineDataUpload is a web-based application designed for managing pipeline data efficiently. It provides:

- **Secure data upload** via Excel files
- **Role-based access control** for different user types
- **Approval workflows** for data changes
- **Real-time dashboard** with statistics and notifications
- **Responsive design** that works on all devices

## 📋 Prerequisites

Before you begin, ensure you have:

- **Web Browser**: Chrome, Firefox, Safari, or Edge (latest versions recommended)
- **Internet Connection**: Stable connection for data uploads
- **Excel Software**: Microsoft Excel or compatible spreadsheet software
- **User Account**: Valid login credentials provided by your administrator

## 🚀 First Steps

### 1. Access the Application

Open your web browser and navigate to the application URL provided by your system administrator.

### 2. Account Setup

If you don't have an account yet:
- Click on "Register" or "Sign Up" link
- Fill in the registration form with your details
- Wait for administrator approval (if required)

### 3. Login

1. Enter your username/email
2. Enter your password
3. Click "Login"
4. (Optional) Check "Remember Me" for persistent login

### 4. Dashboard Tour

After login, you'll see the main dashboard with:
- **Statistics cards** showing system metrics
- **Navigation sidebar** for accessing different features
- **Notifications panel** for important updates
- **Calendar widget** for scheduling

## 🎨 Interface Features

### Dark Mode
- Click the moon/sun icon in the sidebar to toggle between light and dark themes
- Your preference is automatically saved

### Responsive Design
- The application adapts to different screen sizes
- Use the mobile menu button on smaller screens
- Sidebar can be collapsed/expanded for more space

### Navigation
- **Dashboard**: Main overview and statistics
- **Create/Modify Data**: Add or edit pipeline records
- **Bulk Upload**: Upload Excel files with multiple records
- **Piping Data**: View all pipeline data
- **Data Approvals**: Manage approval requests
- **Manage Users**: User administration (Admin only)

## 📁 Understanding Data Structure

The application manages pipeline data with these key fields:

- **Basic Information**: PID Number, Line Number, Pipe Size
- **Technical Details**: Service, Fluid Name, Material Class
- **Operational Parameters**: Pressure, Temperature, Flow rates
- **Physical Properties**: Insulation, Tracing, Density

## 📤 File Upload Requirements

For successful data uploads:

### Excel File Format
- **Format**: .xlsx or .xls (Excel 2007+ preferred)
- **Sheet Name**: Must contain "CA6A" sheet
- **Headers**: First two rows contain headers
- **Data Rows**: Start from row 3
- **File Size**: Maximum 10MB

### Required Columns
The Excel file must include these columns in order:
1. SLNo (Serial Number)
2. PIDNumber (P&ID Number)
3. PIDRevNo (Revision Number)
4. LineNumber (Pipeline Line Number)
5. PipeSizeInches (Pipe Size)
6. Service (Service Type)
7. FluidName (Fluid Name)
8. PipingMaterialClass (Material Class)
9. FromDescription (Origin Description)
10. ToDescription (Destination Description)
11. FluidPhase (Phase: Liquid/Gas)
12. OperatingPressureMin/Max
13. OperatingTemperatureMin/Max
14. DesignPressure/Temperature
15. InsulationTracingType
16. FlowRateGas/Liquid
17. Density/OverallDensity
18. Hold (Status)

## 🔐 Security Best Practices

- **Never share** your login credentials
- **Logout** when finished, especially on shared computers
- **Use strong passwords** and change them regularly
- **Report suspicious activity** to your administrator
- **Keep Excel files secure** before upload

## 📞 Getting Help

If you need assistance:

1. **Check this documentation** first
2. **Use the troubleshooting section** for common issues
3. **Contact your system administrator** for account-specific help
4. **Review the developer guide** for technical details

## 🎯 Next Steps

Now that you're set up:

1. [Explore the Dashboard](./dashboard.md)
2. [Learn about Navigation](./navigation.md)
3. [Try Data Upload](./data-upload.md)
4. [Understand Approvals](./approvals.md)

Welcome aboard! 🎉
