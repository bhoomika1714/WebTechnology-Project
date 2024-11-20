

### **1. Report Collection**
Stores details about each waste report submitted by users.

| Field Name         | Type     | Description                                           |
|--------------------|----------|-------------------------------------------------------|
| `_id`              | ObjectId | Unique identifier for the report.                    |
| `user_id`          | ObjectId | Reference to the User who submitted the report.      |
| `description`      | String   | Description of the waste problem.                    |
| `image_url`        | String   | URL for the uploaded image of the waste.              |
| `status`           | String   | Status of the report: `pending`, `in_progress`, `completed`, `cleaned`. |
| `assigned_to`      | String   | Assigned to (either `press` or `municipal_corp`).     |
| `submitted_at`     | Date     | Timestamp when the report was submitted.             |
| `cleaned_images`   | Array    | Array of before and after cleaning image URLs (optional). |
| `cleaned_status`   | String   | Cleanliness status: `cleaned`, `in_progress`, `pending`. |

---

### **2. Press Collection**
Stores details for the reports flagged for the press.

| Field Name         | Type     | Description                                           |
|--------------------|----------|-------------------------------------------------------|
| `_id`              | ObjectId | Unique identifier for the press report.              |
| `report_id`        | ObjectId | Reference to the Report collection.                  |
| `image_url`        | String   | URL of the report image.                             |
| `submitted_at`     | Date     | Timestamp when the report was sent to the press.     |
| `status`           | String   | Status of the report at the press: `pending`, `published`. |

---

### **3. Municipal Corporation Admin Collection**
Stores details about the municipal corporation admins.

| Field Name         | Type     | Description                                           |
|--------------------|----------|-------------------------------------------------------|
| `_id`              | ObjectId | Unique identifier for the admin.                     |
| `name`             | String   | Full name of the admin.                               |
| `department`       | String   | Department within the municipal corporation.         |
| `contact`          | String   | Contact details (email/phone) of the admin.           |
| `assigned_reports` | Array    | Array of report references (links to the Reports collection). |
| `profile_image`    | String   | URL of the admin's profile picture (optional).        |

---

### **4. Notification Collection**
Stores all notifications related to user actions, report status, and updates.

| Field Name         | Type     | Description                                           |
|--------------------|----------|-------------------------------------------------------|
| `_id`              | ObjectId | Unique identifier for the notification.               |
| `user_id`          | ObjectId | Reference to the User who receives the notification.  |
| `message`          | String   | Notification message text.                            |
| `type`             | String   | Type of notification: `report_status`, `cleaning_update`, `general_alert`. |
| `status`           | String   | Read status: `read` or `unread`.                      |
| `created_at`       | Date     | Timestamp of when the notification was created.       |

---

### **5. Error Log Collection**
Stores details about system errors, such as network failures, upload issues, etc.

| Field Name         | Type     | Description                                           |
|--------------------|----------|-------------------------------------------------------|
| `_id`              | ObjectId | Unique identifier for the error log.                  |
| `error_type`       | String   | Type of error: `network_error`, `upload_failure`, etc. |
| `message`          | String   | Error message or description.                         |
| `timestamp`        | Date     | Timestamp of when the error occurred.                 |
| `resolved`         | Boolean  | Whether the issue has been resolved (default: `false`). |

---

### **6. Image Storage (S3 or Cloud Storage Reference)**
For storing images such as waste reports and cleaning images. This would not typically be a part of the database but rather managed via external storage services (like AWS S3, Cloudinary, etc.). However, here’s how it can be referenced in the database:

| Field Name         | Type     | Description                                           |
|--------------------|----------|-------------------------------------------------------|
| `image_url`        | String   | The URL pointing to the image stored in external storage. |
| `report_id`        | ObjectId | Reference to the associated report.                   |

