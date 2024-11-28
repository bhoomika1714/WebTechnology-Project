To align the given GitHub project with the specified requirements using **HTML, CSS, JavaScript, React, Node.js, and Express.js**, here’s a detailed roadmap for restructuring the project:

---

### **1. Folder Structure Update**

Restructure the existing project repository to accommodate React for the frontend and Node.js/Express.js for the backend:

```
|-- client/                # Frontend with React
|   |-- public/
|   |   |-- index.html     # Main HTML template
|   |-- src/
|       |-- components/    # React components
|           |-- Home.js
|           |-- PressDashboard.js
|           |-- AdminDashboard.js
|           |-- Notifications.js
|           |-- AdminProfile.js
|       |-- styles/        # CSS styles for components
|           |-- common.css
|           |-- home.css
|           |-- dashboard.css
|       |-- App.js         # Root React component
|       |-- index.js       # Entry point for React
|-- server/                # Backend with Node.js and Express.js
|   |-- routes/
|       |-- api/
|           |-- reports.js # API routes for handling reports
|           |-- notifications.js
|           |-- admin.js
|   |-- models/            # Database models
|       |-- Report.js
|       |-- Notification.js
|       |-- Admin.js
|   |-- app.js             # Main Express app file
|-- package.json           # Project configuration
|-- README.md
```

---

### **2. Frontend Implementation (React)**

#### **Home Page (Waste Reporting)**
- **Component**: `Home.js`
- **Features**:
  - Implement an image upload input using the `react-file-upload` library.
  - Use a dropdown menu for "Send to Press" or "Send to Municipal Corporation."
  - Add a submit button that triggers an API call to the backend.

#### **Press Dashboard**
- **Component**: `PressDashboard.js`
- **Features**:
  - Display a list of reports fetched via an API call.
  - Include image previews, descriptions, and submission dates.
  - Use React state to manage and display notifications.

#### **Municipal Corporation Admin Dashboard**
- **Component**: `AdminDashboard.js`
- **Features**:
  - Fetch and display user-submitted reports using an API.
  - Allow uploading "Before" and "After Cleaning" images.
  - Include buttons for updating the cleanliness status (e.g., Assigned, Completed).

#### **Notifications Page**
- **Component**: `Notifications.js`
- **Features**:
  - Fetch and display notifications related to reports, cleaning updates, and status changes.
  - Add filters for different notification types (e.g., alerts, cleaning updates).

#### **Admin Profile Page**
- **Component**: `AdminProfile.js`
- **Features**:
  - Display admin details fetched from the backend.
  - List reports assigned to the admin.

---

### **3. Backend Implementation (Node.js + Express.js)**

#### **API Endpoints**
- **Reports**:
  - `POST /api/reports`: Accept image uploads and user-submitted data (e.g., descriptions).
  - `GET /api/reports`: Fetch reports for the press or municipal corporation.
  - `PATCH /api/reports/:id`: Update the status or add "Before/After Cleaning" images.

- **Notifications**:
  - `POST /api/notifications`: Trigger notifications for users or admins.
  - `GET /api/notifications`: Retrieve notifications for the logged-in user.

- **Admin**:
  - `GET /api/admin/profile`: Retrieve admin profile details.
  - `PATCH /api/admin/profile`: Update admin profile information.

#### **Database Models**
- **Report Schema**:
  ```javascript
  const mongoose = require('mongoose');

  const reportSchema = new mongoose.Schema({
      user: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
      description: String,
      imageUrl: String,
      target: { type: String, enum: ['Press', 'Municipal Corporation'] },
      status: { type: String, default: 'Pending' },
      beforeImage: String,
      afterImage: String,
      createdAt: { type: Date, default: Date.now },
  });

  module.exports = mongoose.model('Report', reportSchema);
  ```

- **Notification Schema**:
  ```javascript
  const mongoose = require('mongoose');

  const notificationSchema = new mongoose.Schema({
      user: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
      message: String,
      type: { type: String, enum: ['Alert', 'Update'] },
      createdAt: { type: Date, default: Date.now },
  });

  module.exports = mongoose.model('Notification', notificationSchema);
  ```

- **Admin Schema**:
  ```javascript
  const mongoose = require('mongoose');

  const adminSchema = new mongoose.Schema({
      name: String,
      department: String,
      contact: String,
      assignedReports: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Report' }],
  });

  module.exports = mongoose.model('Admin', adminSchema);
  ```

---

### **4. Integration Workflow**

1. **Frontend**:
   - Use `axios` for API requests.
   - Leverage React Router for navigation between pages.
   - Use `react-toastify` for displaying notifications.

2. **Backend**:
   - Set up `multer` for handling file uploads.
   - Use `mongoose` to connect with MongoDB.
   - Implement middleware for error handling and validation.

3. **Testing**:
   - Test APIs using Postman.
   - Perform frontend testing with tools like Jest and React Testing Library.

---

### **5. Deployment**
- Deploy the frontend using **Netlify** or **Vercel**.
- Deploy the backend using **Render**, **Heroku**, or **AWS**.
- Use **MongoDB Atlas** for the database.

---

This roadmap transitions your project to a modern stack while ensuring scalability and maintainability.
