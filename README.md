# Automated Log Analysis for AEM Application and System Logs

## Project Overview
This project is a Bash scripting–based automation tool designed to analyze AEM application and system log files on Linux servers. It helps identify operational issues by scanning logs for critical error patterns and generating a structured analysis report. The solution minimizes manual log review and accelerates troubleshooting in production environments.

---

## Problem Statement
In AEM and Linux production environments, log files can grow rapidly and contain large volumes of data. Manual inspection is time-consuming, inconsistent, and prone to human error. This project automates the log analysis process to ensure faster and more reliable issue detection.

---

## Solution Approach
The script performs the following actions:
1. Scans a configured log directory
2. Identifies `.log` files updated within the last 24 hours
3. Iterates through each log file dynamically
4. Searches for critical severity patterns:
   - ERROR
   - FATAL
   - CRITICAL
5. Counts occurrences per severity level and file
6. Writes results to a consolidated analysis report

---

## Key Features
- Automated log discovery
- Pattern-based error detection
- Multi-file log analysis
- Consolidated report generation
- Lightweight Bash implementation
- Easy customization

---

## Project Structure
```
.
├── analyse-log.sh
├── logs/
│   ├── application.log
│   ├── system.log
│   └── log_analysis_report.txt
└── README.md
```

---

## Prerequisites
- Linux operating system
- Bash shell
- Read access to application and system log files

---

## Usage Instructions
Make the script executable:
```bash
chmod +x analyse-log.sh
```

Run the script:
```bash
./analyse-log.sh
```

The analysis report will be generated at:
```
/home/aem/Public/logs/log_analysis_report.txt
```

---

Final Script :
>> 

      #!/bin/bash
      
      LOG_DIR="/home/aem/Public/logs"
      ERROR_PATTERNS=("ERROR" "FATAL" "CRITICAL")
      REPORT_FILE="/home/aem/Public/logs/log_analysis_report.txt"
      
      echo "analysing log files" > $REPORT_FILE
      echo "===================" >> $REPORT_FILE
      
      echo -e "\nList of log files updated in last 24 hours" >> $REPORT_FILE
      LOG_FILES=$(find $LOG_DIR -name "*.log" -mtime -1) 
      echo "$LOG_FILES" >> $REPORT_FILE
      
      for LOG_FILE in $LOG_FILES; do
          echo -e "\n" >> $REPORT_FILE
          echo "===========================================" >> $REPORT_FILE
          echo "=========$LOG_FILE=============" >> $REPORT_FILE
          echo "===========================================" >> $REPORT_FILE
       
          for PATTERN in "${ERROR_PATTERNS[@]}"; do
      
          echo -e "\nSearching $PATTERN logs in $LOG_FILE file" >> $REPORT_FILE
          grep "$PATTERN" "$LOG_FILE" >> $REPORT_FILE
      
          echo -e "\nNumber of $PATTERN logs found in $LOG_FILE" >> $REPORT_FILE
      
          ERROR_COUNT=$(grep -c "$PATTERN" "$LOG_FILE")
      
          echo $ERROR_COUNT >> "$REPORT_FILE "
          if [ "$ERROR_COUNT" -gt 2 ]; then
              echo -e "\nAlert: More than 2 $PATTERN logs found in $LOG_FILE"
          fi
          done
      done
      
      echo -e "\nLog analysis completed and report saved in: $REPORT_FILE"
------------------------------------------------------------------------------------------------------------------------------------------------

## Use Cases
- AEM production support troubleshooting
- Linux system monitoring
- Incident root-cause analysis
- Support and operations automation

---

## Customization Options
- Add or modify error patterns
- Change log directory paths
- Adjust time window for log scanning
- Extend with cron jobs or alerting mechanisms

---

## Future Enhancements
- Threshold-based alert notifications
- Email or messaging integrations
- Support for log rotation
- Structured output formats (CSV / JSON)

---

## Skills Demonstrated
- Bash scripting
- Linux log analysis
- Automation for production systems
- AEM operational troubleshooting
