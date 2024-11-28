```
client/
|-- src/
|   |-- assets/                  # Folder for storing images, fonts, and other static assets
|   |   |-- images/              # For images like logos, background images, etc.
|   |   |-- fonts/               # For fonts if needed
|   |-- components/              # React Components
|   |   |-- Home.js              # Home Page Component
|   |   |-- PressDashboard.js    # Dashboard Component
|   |   |-- AdminDashboard.js    # Admin Dashboard Component
|   |   |-- Notifications.js     # Notifications Component
|   |   |-- AdminProfile.js      # Admin Profile Component
|   |-- styles/                  # CSS Styles
|   |   |-- common.css           # Common Styles
|   |   |-- home.css             # Home Page Styles
|   |   |-- dashboard.css        # Dashboard Styles
|   |-- App.js                   # Main React App Component
|   |-- index.js                 # Entry point for React
|
server/                           # Backend-related files (Node.js)
|-- routes/
|   |-- reports.js               # Routes for report-related functionality
|   |-- notifications.js         # Routes for notifications-related functionality
|   |-- admin.js                 # Routes for admin-related functionality
|-- models/
|   |-- Report.js                # Model for reports
|   |-- Notification.js          # Model for notifications
|   |-- Admin.js                 # Model for admin
|-- app.js                        # Main server entry file
|-- .env                          # Environment variables (e.g., database credentials)

```

### **1. Home Page (User Page - Waste Reporting)**

**Responsibilities**: Member A

- **Design**: 
  - Design the layout with **HTML/CSS**.
  - Include components for:
    - Image upload (with description input).
    - Dropdown for sending the report to the **press** or **municipal corporation**.
    - Submit button for reporting.
  - Make sure the page is **responsive** and visually appealing.

- **Backend Implementation**:
  - Develop the **API** to handle image uploads.
  - Store data in the **MongoDB database** (user info, report details, image URLs).
  - Implement the logic to handle **press** and **municipal corporation** options.

- **Notification System**:
  - Implement notifications to:
    - **Press** or **municipal corporation** (depending on the user’s choice).
    - Notify users that the municipal corporation is not working properly when the report is sent to the press.

- **Testing**:
  - Test the **image upload**, **report submission**, and **notifications**.
  - Ensure smooth user experience by testing form submission and image processing.
  - Check the response time and ensure proper error handling (e.g., failed uploads, slow response).

---

### **2. Press Dashboard**

**Responsibilities**: Member B

- **Design**:
  - Create the layout using **HTML/CSS** for displaying the list of waste reports sent to the press.
  - Include:
    - A list of reports with images, descriptions, and submission date.
    - Notification section to alert users that the municipal corporation is not performing its duties.

- **Backend Implementation**:
  - Develop **API endpoints** to fetch reports sent to the press from the database.
  - Implement the **notification system** that alerts all users when a report is flagged for the press.
  
- **Testing**:
  - Test **report display** functionality on the press dashboard.
  - Ensure the **notification system** is working as expected (sending alerts to users).
  - Test the page for responsiveness and design consistency.

---

### **3. Municipal Corporation Admin Dashboard**

**Responsibilities**: Member C

- **Design**:
  - Design the **Admin Dashboard UI** using **HTML/CSS**.
  - Display:
    - Reports submitted by users (images, descriptions).
    - Options for uploading **Before** and **After Cleaning** images.
    - Cleanliness status update for each report (assigned to cleaning crew or completed).

- **Backend Implementation**:
  - Implement **API logic** to retrieve reports for the municipal corporation.
  - Allow the **admin** to upload images and update the report status (Before and After Cleaning).
  - Trigger notifications to users once the cleaning process is completed, showing before/after images.

- **Testing**:
  - Test **image upload functionality** for Before/After images and the status update of reports.
  - Ensure that the **notification system** triggers once cleaning is completed and images are uploaded.
  - Test that the dashboard is working smoothly, and no reports are missed.

---

### **4. Notifications Page (for Users)**

**Responsibilities**: Member A (Phase 2)

- **Design**:
  - Build the **Notifications Page** to display alerts for the user.
  - Display notifications for reports (sent to press or municipal corporation), cleaning updates, and status changes.
  
- **Backend Implementation**:
  - Implement **API endpoints** to retrieve notifications from the database.
  - Fetch notifications like report updates, status changes, and cleaning completions.

- **Testing**:
  - Test the **notification display** to ensure all notifications are correctly shown for the user.
  - Validate that the notifications are triggered accurately based on actions in the system.

---

### **5. Admin (Municipal) Profile Page**

**Responsibilities**: Member B (Phase 2)

- **Design**:
  - Design the **Admin Profile Page** layout with **HTML/CSS**.
  - Show basic **profile details** (e.g., name, department, contact) and provide a list of **assigned reports**.

- **Backend Implementation**:
  - Implement **API endpoints** to retrieve and update admin profile data.
  - Implement logic to display reports assigned to the admin.

- **Testing**:
  - Test that the **profile details** are correctly displayed and updated.
  - Ensure that the assigned reports appear correctly under the admin's profile.

---

### **6. Error Handling & Edge Cases**

**Responsibilities**: Member C (Final Phase)

- **Design**: 
  - Implement error messages in the UI when issues occur (e.g., **“Network Error”** or **“Upload Failed”**).
  
- **Backend Implementation**:
  - Handle edge cases, such as slow responses, image upload failures, and service unavailability.
  - Provide proper feedback to the user when an issue occurs (timeouts, slow responses).

- **Testing**:
  - Test **network failures**, **slow responses**, and **image upload errors**.
  - Simulate these scenarios to ensure that the system behaves as expected and provides clear error messages to users.

