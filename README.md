# zabbix-template-snmp-availability

This template checks the SNMP interface availability of the host. It triggers an alert when SNMP becomes unavailable. The macro {$AGENT.TIMEOUT} controls how long Zabbix waits before firing the trigger.

## Macros

| Macro                      | Value                                         | Description                                           |
|---------------------------|---------------------------------------------|-------------------------------------------------------|
| {$AGENT.TIMEOUT}    | `3m` (default)                            | Timeout after which agent is considered unavailable.                   |

## 📦 Zabbix Items Overview

| Name                      | Key                                         | Triggers | Description                                           |
|---------------------------|---------------------------------------------|----------|-------------------------------------------------------|
| Hostname of SNMP Agent    | `snmp.hostname`                            | 1        | Displays the SNMP agent's hostname.                   |
| SNMP availability         | `zabbix[host,snmp,available]`              | 1        | Displays the SNMP availability of the host.           |

## 🚨 Zabbix Trigger Overview

| Severity | Name                                                  | Expression                                                                 |
|----------|-------------------------------------------------------|----------------------------------------------------------------------------|
| Average  | 	SNMP on `{HOST.NAME}` is unreachable    | `max(/SNMP Availability Check/zabbix[host,snmp,available],{$AGENT.TIMEOUT})=0`|
| Information  | SNMP System name has changed | `change(/SNMP Availability Check/snmp.hostname) and length(last(/SNMP Availability Check/snmp.hostname))>0`|

The XML/YAML file has been exported with Zabbix-7.4.
