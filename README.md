# Compliance Report

A Python tool that combines multiple AWS audit checks into a unified, professional HTML compliance report.

## Overview

This lesson builds on previous audits (S3, IAM, Security Groups) and combines them into a single report generator using:
- **Functions** - Refactored audit logic into reusable functions
- **Jinja2** - HTML templating for professional reports
- **Data aggregation** - Unified findings from multiple sources

## Requirements

- Python 3.x
- `boto3` library
- `jinja2` library
- AWS CLI configured with credentials (`aws configure`)

### Install dependencies
```bash
pip install boto3 jinja2
```

## Usage

### Generate a compliance report
```bash
python compliance_report.py
```

**Sample output:**
```
============================================================
AWS Compliance Report Generator
============================================================

[1/4] Getting account information...
      Account: 365827925154

[2/4] Auditing S3 buckets...
      Found 1 buckets

[3/4] Auditing IAM users...
      Found 1 users

[4/4] Auditing security groups...
      Found 1 security groups

Generating HTML report...

✓ Report saved: compliance_report_20260121_162513.html

Open the HTML file in a browser to view the report.
```

### View the report
Open the generated `.html` file in any web browser.

## Report Contents

### Executive Summary
- Total passed checks (green)
- Total failed checks (red)
- Total warnings (yellow)

### S3 Bucket Audit
| Check | Description |
|-------|-------------|
| Encryption | Server-side encryption enabled? |
| Public Access Block | All four settings enabled? |

### IAM User Audit
| Check | Description |
|-------|-------------|
| Console Access | Does user have AWS Console login? |
| MFA Enabled | Is MFA configured for console users? |

### Security Group Audit
| Check | Description |
|-------|-------------|
| Open Ports | Ports open to 0.0.0.0/0 (non-risky) |
| Risky Ports | SSH, RDP, database ports open to internet |

## Status Legend

| Status | Meaning | Color |
|--------|---------|-------|
| `PASS` | Check passed | Green |
| `FAIL` | Critical issue | Red |
| `WARN` | Review recommended | Yellow |
| `INFO` | Informational only | Blue |

## Key Concepts Learned

| Concept | Description |
|---------|-------------|
| **Functions** | `def audit_s3_buckets():` - Reusable audit logic |
| **Return values** | Functions return data instead of printing |
| **Jinja2 templates** | `{{ variable }}` and `{% for %}` loops |
| **HTML/CSS** | Professional report styling |
| **Data aggregation** | Combine findings from multiple sources |
| **List comprehensions** | `[f['status'] for f in findings]` |

## Code Patterns

### Function that returns data
```python
def audit_s3_buckets():
    findings = []
    # ... audit logic ...
    findings.append(result)
    return findings
```

### Jinja2 template variables
```html
<p>Account: {{ account_id }}</p>
<p>Generated: {{ timestamp }}</p>
```

### Jinja2 loops
```html
{% for bucket in s3_findings %}
<tr>
    <td>{{ bucket.name }}</td>
    <td>{{ bucket.status }}</td>
</tr>
{% endfor %}
```

### Jinja2 conditionals
```html
{{ 'Yes' if user.has_console else 'No' }}
```

### Render template
```python
from jinja2 import Template

template = Template(HTML_TEMPLATE)
html = template.render(
    account_id='123456789',
    findings=findings
)
```

## GRC Application

This tool supports:
- **SOC 2** - Evidence collection for audits
- **ISO 27001** - Security control documentation
- **NIST 800-53** - Compliance reporting
- **PCI DSS** - Quarterly scan reports
- **Internal audits** - Executive summaries

## Future Enhancements

- Add CloudTrail findings to report
- Export to PDF
- Email report automatically
- Add charts/graphs with Chart.js
- Compare with previous reports (trending)
- Add remediation recommendations
