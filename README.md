# Syden Compliance Engine

> 🧩 **TL;DR**
> - Set up demo in ~5 minutes.
> - Adds encrypted fields, GDPR-style soft delete and audit logging to your Django project.
> - Aimed at freelancers / small teams who don’t want to spend 1–3 days wiring this from scratch.
🎥 Real-time install demo (5 minutes): https://youtu.be/tiMLjWpDXFk
🎥 Overview & delete/anonymise actions: https://youtu.be/RFBO2XDXJNI


> Data protection & audit engine for Django

Syden Compliance Engine is a ready-to-use **data protection & audit engine for Django projects**.

It gives you a complete mini-engine that you can plug into your Django projects to handle sensitive data more professionally:

- encrypted storage of e-mail and other sensitive fields in the database;
- GDPR-style **soft delete + anonymisation** (“right to be forgotten”);
- a **tamper-resistant audit log** of critical actions;
- a clean **REST API** built on Django REST Framework;
- a **security dashboard** inside Django admin.

---

## 🎯 Who is this for?

- Django developers who need better handling of sensitive data.
- Small teams that want a simple way to log access/changes to personal data.
- SaaS projects that want to move closer to GDPR-style data protection patterns.

This repository is a **public showcase & documentation**.  
The full source code of the engine is delivered as a paid package.

👉 **Buy the full engine on Gumroad:**  
https://syxov.gumroad.com/l/rgzfqx

---

## 🔐 Core features

### 1. Encrypted fields

Custom Django model field `EncryptedCharField`:

- encrypts string values before saving them to the database;
- transparently decrypts when you access the field in Python;
- uses a symmetric key from the `HIPAA_ENCRYPTION_KEY` environment variable.

### 2. Audit log

Centralised model `AuditLogEntry` that records:

- action type (READ / UPDATE / DELETE);
- model name and object ID;
- timestamp;
- optional reason/comment;
- optional user who performed the action.

The audit log is **read-only** in Django admin — records cannot be edited or deleted.

### 3. Data subject profile

Example model `PatientProfile` used as a generic **“data subject”**:

- `private_email` — encrypted e-mail address;
- `public_id` — external identifier (client ID, card ID, profile ID, etc.);
- `is_deleted` / `deleted_at` — soft delete & anonymisation flags.

You can use it as-is or adapt it to your own user/client model.

### 4. Soft delete + anonymisation

Utility function:

```python
safe_delete_subject(subject_id, reason=None)
It:

wipes the encrypted e-mail;

replaces public_id with an anonymised value;

marks the record as deleted;

writes a DELETE entry into the audit log.

5. REST API (Django REST Framework)

ViewSet: DataSubjectViewSet.

Endpoints:

GET /api/v1/subjects/ — list active data subjects;

POST /api/v1/subjects/ — create a subject;

GET /api/v1/subjects/{id}/ — retrieve a subject;

PATCH/PUT /api/v1/subjects/{id}/ — update a subject.

Soft-deleted / anonymised records are automatically filtered out.

6. Security dashboard

Staff-only view at /privacy-dashboard/ shows:

total number of audit log entries;

distribution of actions by type (bar chart);

top 5 users by number of actions.

📺 Demo videos

You can see the engine in action on YouTube:

Overview & deletion demo:
https://youtu.be/RFBO2XDXJNI

Installation & setup demo:
https://youtu.be/tiMLjWpDXFk

🧩 Tech stack

Python 3.10+

Django 4.x

Django REST Framework

PyCryptodome

The paid package includes:

full Django project (config/, privacy_engine/, manage.py, migrations);

requirements.txt;

detailed README.md with step-by-step setup;

commercial license for use in your own projects.

⚠️ Security & legal note

Syden Compliance Engine is a technical tool that helps you implement common privacy patterns:

encryption of sensitive data in the database;

soft delete with anonymisation;

centralised audit logging;

a basic monitoring dashboard.

It is not legal advice and does not automatically make your system GDPR/HIPAA compliant.
You are responsible for your own legal/regulatory compliance and for managing encryption keys securely.

🔑 Licensing (summary)

The full engine is sold under a commercial license.

You may:

use it in your own internal or commercial projects;

modify the source code for your own needs;

deploy it on multiple servers/instances within your organisation.

You may not:

redistribute or resell the source code as a standalone product;

publish the source code in public repositories;

claim authorship of the original engine.

For extended or custom licensing (agency / client work / enterprise), contact:

support@syden.systems
