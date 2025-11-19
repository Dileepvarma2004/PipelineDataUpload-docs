# Data Upload Process

Learn how to upload pipeline data using Excel files efficiently and securely.

## 📤 Upload Overview

The bulk upload feature allows you to import multiple pipeline records from Excel files. This is the primary method for adding large amounts of data to the system.

## 🔐 Access Requirements

- **User Role**: Admin or CreateModify role required
- **File Permissions**: Read access to Excel files
- **Network**: Stable internet connection for large files

## 📋 File Preparation

### Excel File Requirements

#### Supported Formats
- **Primary**: .xlsx (Excel 2007 and later)
- **Legacy**: .xls (Excel 2003 and earlier)
- **Maximum Size**: 10MB per file

#### Required Sheet Structure
- **Sheet Name**: Must be named "CA6A" (case-sensitive)
- **Header Rows**: First 2 rows contain column headers
- **Data Rows**: Actual data starts from row 3
- **Empty Rows**: Skip completely empty rows automatically

### Column Specifications

The Excel file must contain these 23 columns in the exact order:

| Column # | Field Name | Type | Required | Description |
|----------|------------|------|----------|-------------|
| 1 | SLNo | Integer | Yes | Serial number/unique identifier |
| 2 | PIDNumber | String | Yes | P&ID drawing number |
| 3 | PIDRevNo | String | No | P&ID revision number |
| 4 | LineNumber | String | Yes | Pipeline line number (must end with 4 digits) |
| 5 | PipeSizeInches | String | Yes | Pipe diameter in inches |
| 6 | Service | String | Yes | Service type (e.g., Process, Utility) |
| 7 | FluidName | String | Yes | Name of fluid being transported |
| 8 | PipingMaterialClass | String | Yes | Material specification class |
| 9 | FromDescription | String | No | Origin/description |
| 10 | ToDescription | String | No | Destination/description |
| 11 | FluidPhase | String | No | Liquid, Gas, or Two-phase |
| 12 | OperatingPressureMin | Float | No | Minimum operating pressure |
| 13 | OperatingPressureMax | Float | No | Maximum operating pressure |
| 14 | OperatingTemperatureMin | Float | No | Minimum operating temperature |
| 15 | OperatingTemperatureMax | Float | No | Maximum operating temperature |
| 16 | DesignPressure | Float | No | Design pressure rating |
| 17 | DesignTemperature | Float | No | Design temperature rating |
| 18 | InsulationTracingType | String | No | Insulation or tracing specification |
| 19 | FlowRateGas | String | No | Gas flow rate |
| 20 | FlowRateLiquid | String | No | Liquid flow rate |
| 21 | Density | String | No | Fluid density |
| 22 | OverallDensity | String | No | Overall system density |
| 23 | Hold | String | No | Status or hold condition |

## 📊 Sample Excel Structure

```
Row 1: [Headers - can be descriptive names]
Row 2: [Sub-headers or units if needed]
Row 3: [First data record]
Row 4: [Second data record]
...
```

### Example Data Row
```
| 1 | PID-001 | A | 1001-ABCD-0001 | 12" | Process | Crude Oil | CS-A106-B | Pump P-101 | Tank T-201 | Liquid | 50 | 150 | 25 | 80 | 200 | 100 | Mineral Wool | 5000 | N/A | 0.85 | 0.82 | Active |
```

## 🚀 Upload Process

### Step 1: Access Upload Page
1. Login to the application
2. Navigate to "Bulk Upload" from the sidebar
3. Verify you have Admin or CreateModify permissions

### Step 2: Select File
1. Click "Choose File" or "Browse"
2. Navigate to your prepared Excel file
3. Select the file and click "Open"

### Step 3: File Validation
The system automatically validates:
- ✅ File format (.xlsx or .xls)
- ✅ File size (≤ 10MB)
- ✅ Sheet name ("CA6A" exists)
- ✅ Column structure (23 columns minimum)
- ✅ Header presence

### Step 4: Upload Execution
1. Click "Upload" button
2. Monitor progress (for large files)
3. Wait for processing completion

### Step 5: Review Results
After upload, you'll see:
- **Success Count**: Records processed successfully
- **Error Count**: Records with issues
- **Skipped Count**: Empty rows skipped
- **Processing Time**: Total time taken

## 📊 Upload Results

### Success Scenarios
- **Complete Success**: All records processed without errors
- **Partial Success**: Some records processed, some failed
- **Complete Failure**: No records processed (critical errors)

### Error Types
- **Validation Errors**: Missing required fields, invalid data types
- **Duplicate Errors**: Records with existing identifiers
- **Format Errors**: Incorrect data format in cells
- **Database Errors**: Connection or constraint violations

## 🔍 Error Details

### Common Validation Errors

#### Missing Required Fields
```
Error: LineNumber must end with 4 digits: ABC-123
Solution: Ensure LineNumber follows format XXXX-XXXX-XXXX
```

#### Invalid Data Types
```
Error: OperatingPressureMin must be numeric: "High"
Solution: Enter numeric values only (e.g., 150.5)
```

#### Duplicate Records
```
Error: Record with SLNo 123 already exists
Solution: Check for duplicates or use different SLNo
```

### Error Report Format
```
[ROW 5] [LineNumberCell: '1001-ABCD-0001'] [IdAttempt: 1] Exception: Duplicate key violation
[ROW 8] [LineNumberCell: '1002-X'] [IdAttempt: null] Exception: LineNumber must end with 4 digits
```

## ✅ Post-Upload Actions

### Successful Upload
1. **Review Summary**: Check success/error counts
2. **Download Report**: Save error details if needed
3. **Approval Process**: Records enter approval workflow
4. **Notifications**: Check dashboard for approval requests

### Handling Errors
1. **Fix Excel File**: Correct identified issues
2. **Partial Upload**: Upload only corrected records
3. **Contact Admin**: For system-level issues

## 📋 Best Practices

### File Preparation
- **Clean Data**: Remove empty rows and columns
- **Consistent Formatting**: Use same formats throughout
- **Data Validation**: Check data before upload
- **Backup Files**: Keep original files safe

### Upload Strategy
- **Test Uploads**: Use small test files first
- **Batch Processing**: Split large files if needed
- **Version Control**: Track file versions
- **Documentation**: Record upload details

### Performance Tips
- **File Size**: Keep under 5MB for faster processing
- **Network**: Use stable, fast internet connection
- **Timing**: Upload during off-peak hours
- **Monitoring**: Watch progress for large files

## 🔄 Approval Workflow

After successful upload:
1. **Pending Status**: Records await approval
2. **Notification**: Approvers receive requests
3. **Review Process**: Approvers check data quality
4. **Approval/Rejection**: Records approved or sent back
5. **Final Status**: Records become active or archived

## 📊 Monitoring Uploads

### Dashboard Tracking
- **Recent Uploads**: Last 7 days in "Pending Updates"
- **Success Rate**: Monitor approval percentages
- **Error Trends**: Identify common issues

### Activity Logs
- **Upload History**: Track all upload attempts
- **Processing Details**: View detailed logs
- **Audit Trail**: Complete record of changes

## 🔧 Troubleshooting Upload Issues

### File-Related Problems
- **File Not Found**: Check file path and permissions
- **Invalid Format**: Ensure .xlsx or .xls format
- **Corrupt File**: Try saving as new file
- **Size Limit**: Compress or split large files

### System Issues
- **Timeout Errors**: Check network stability
- **Memory Errors**: Close other applications
- **Database Issues**: Contact system administrator

### Permission Problems
- **Access Denied**: Verify user role permissions
- **File Locked**: Close Excel if file is open
- **Network Drive**: Copy to local drive first

## 📞 Support and Help

### Getting Assistance
1. **Check Logs**: Review error messages carefully
2. **Documentation**: Refer to this guide and examples
3. **Administrator**: Contact for permission issues
4. **Developer Support**: For technical file format issues

### Escalation Process
- **Minor Issues**: Try troubleshooting steps
- **Major Problems**: Document steps and contact admin
- **System Errors**: Report with screenshots and logs

## 🎯 Advanced Features

### Batch Uploads
- Upload multiple files in sequence
- Track batch progress and results
- Consolidated error reporting

### Template Downloads
- Download Excel templates with proper formatting
- Pre-configured headers and validation
- Sample data for reference

### Automated Processing
- Scheduled uploads (if configured)
- API integration for automated systems
- Real-time status monitoring

## 📈 Performance Metrics

### Upload Statistics
- **Processing Speed**: Records per second
- **Success Rate**: Percentage of successful uploads
- **Error Patterns**: Common issues and resolutions

### System Health
- **Memory Usage**: During large file processing
- **Database Performance**: Query execution times
- **Network Utilization**: Bandwidth consumption

## 🔐 Security Considerations

### Data Protection
- **Encryption**: Files encrypted during transfer
- **Access Control**: Role-based upload permissions
- **Audit Logging**: Complete upload activity tracking

### Compliance
- **Data Validation**: Ensures data quality standards
- **Backup Systems**: Automatic data backups
- **Recovery**: Rollback capabilities for failed uploads

## 🎯 Next Steps

After mastering data uploads:
1. [Learn about Data Viewing](./viewing-data.md)
2. [Understand Approvals](./approvals.md)
3. [Explore Advanced Features](./navigation.md)
