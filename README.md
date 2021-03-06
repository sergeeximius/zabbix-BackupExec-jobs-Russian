**================Zabbix-Symantec-Backup-Exec ================**

Template for Zabbix 3.4.

Work with Symantec Backup Exec V2012 minimum (don't work older versions) !

This template use PowerShell Cmdlets to discover backup job Symantec Backup Exec.

Default Russian translation for Template.
Optimizing for Symantec Backup Exec on Cyrillic CP866 and Zabbix Server on UTF-8.

**-------- Items --------**

  - Check Service Backup Exec Agent Browser
  - Check Service Service Backup Exec Device & Media
  - Check Service	Service Backup Exec Job Engine
  - Check Service Backup Exec Management Service

**-------- Triggers --------**

  - X4 : [HIGH] => For all services Stop

**-------- Discovery --------**

  - Last launch of each task
  - End of each task
  - Result of each task
  - Backup type of each task
  - Last task total data size
  - Task does not run 7 days
  - Current status of task (for recovery expression in triggers, if status is active - trigger is OK)

**-------- Discovery Triggers --------**

[HIGH] => Job has FAILED <br>
[HIGH] => Job has CANCELLED <br>
[MEDIUM] => No data recovery for 24 hours<br>
[MEDIUM] => Job does not run 7 days<br>


**-------- Setup --------**

1. Install the Zabbix agent on your host
2. Copy zabbix_sbr_job.ps1 in the directory : "C:\Program Files\Zabbix Agent\scripts" (create folder if not exist)
3. Add the following line to your Zabbix agent configuration file.<br>
Timeout=30 <br>
EnableRemoteCommands=1 <br>
UnsafeUserParameters=1 <br>
UserParameter=sbr[*],powershell -NoProfile -ExecutionPolicy Bypass -File "C:\Program Files\Zabbix Agent\scripts\zabbix_sbr_job.ps1" "$1" "$2"
4. Import TemplateSymantecBackupExec.xml file into Zabbix.
5. Associate "Template Symantec BackupExec" to the host.
