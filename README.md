# Account-Master
an Oracle SQL view for the Account Master in an ERP system.

ERP-Account-Master/
├── view_acc_mast.sql              # SQL View for Account Master with schedule and geo details
└── README.md                      # Documentation file

# ERP Account Master View – Oracle SQL

## 📘 Overview

This repository contains the SQL View `view_acc_mast`, which serves as the **master reference** for accounts in an ERP system. It merges core account details from `acc_mast` with account schedule hierarchy and geographical organization for better reporting, validation, and hierarchy tracing.

---

## 📄 Files Included

| File Name         | Description                                               |
|------------------|-----------------------------------------------------------|
| `view_acc_mast.sql` | Oracle SQL view of account master, enriched with hierarchy and metadata |

---

## 🔍 Key Features

- 🔑 **Basic Account Metadata**  
  Includes fields like `acc_code`, `acc_name`, `acc_class_code`, `acc_type`, `supplier_type`, etc.

- 🧾 **Tax and Statutory Info**  
  Contains TDS, GST, PAN, ECC, range, collector, service tax, and registration numbers.

- 🏦 **Banking Details**  
  Pulls party bank name, account number, and IFSC code.

- 📚 **Account Schedule Mapping**  
  Joins with `view_acc_sch_mast` to fetch:
  - `acc_sch_l1`, `acc_sch_l2`, `acc_sch_l3`
  - Schedule names for better grouping

- 🌍 **Geo Hierarchy Lookup**  
  Integrates organization structure using `geo_org_mast`, pulling:
  - Immediate, parent, grandparent, and great-grandparent org codes

- 🧩 **Other Attributes**
  - `creditlimit`, `intdays`, `apdays`, `inv_acc_flag`, `div_code`, `cost_code`
  - Custom flags like `billtrack`, `cbjqty_flag`, `flag`, and more

---

## 🧑‍💻 Use Cases

- Standardized reference for all account-related modules (AP, AR, TDS, GST)
- BI and Power BI reporting with hierarchy-based aggregation
- ERP validations (credit limit, account structure, geo-based rules)
- Invoice generation & vendor registration workflows

---

## 🛠️ Technology Stack

- Oracle SQL
- Tables/Views used: `acc_mast`, `view_acc_sch_mast`, `geo_org_mast`

---

## 💡 Example Query Usage

```sql
SELECT acc_code, acc_name, acc_status, acc_sch_l1, parent_geo_org_code
FROM view_acc_mast
WHERE acc_status = 'ACTIVE'
ORDER BY acc_sch_l1, acc_name;
