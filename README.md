# LLM MVP Requirements Documentation

## Overview
This repository contains product requirements documentation for the Local Loop Merseyside (LLM) MVP platform.

**Target Audience:** Small development team (product owner, junior to senior developers)  
**Purpose:** Source of truth for ongoing MVP and post-MVP development

---

## Requirements Index

### System Functions

#### Data Collection & Integration
- [Promis Data Collection](requirements/system-functions/promis-data-collection.md) - #SystemFunction #PromisIntegration #DataCollection #Xero #QuickBooks
  - Connect, disconnect, reconnect accounting platform integrations
  - Invoice data collection from Xero and QuickBooks
  - Contacts data collection
  - Connection limits and concurrency

---

## Tag Index

### By Type
- **#SystemFunction** - Backend system functionality and data processing
- **#ClientUser** - Client-facing user interface and workflows  
- **#AdminUser** - Administrative interface and operations

### By Integration
- **#PromisIntegration** - Promis service integration requirements
- **#Xero** - Xero accounting platform integration
- **#QuickBooks** - QuickBooks accounting platform integration

### By Function
- **#DataCollection** - Data ingestion and collection workflows

---

## Document Structure

Each requirement document follows this structure:
1. **Metadata** - Tags, source, last updated
2. **Main Requirements** - Numbered sections with WHY and WHAT
3. **Testing Notes** - Section 9: test scenarios, scripts, board cleanup
4. **Post-MVP Notes** - Section 10: future enhancements

---

## Migration Notes

**Source:** ClickUp workspace (ID: 9015918923)  
**Migration Date:** 2025-01-06  
**Mapping:** One-to-one from ClickUp pages to markdown files  
**Preservation:** All original content preserved without modification

---

**Repository Created:** 2025-01-06  
**Last Updated:** 2025-01-06
