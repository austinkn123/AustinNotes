
### **Tech Stack**

#### 1. **Frontend (Web & Mobile)**:

- **JavaScript** (for both web and mobile app development).
- **React Native** (if you want a cross-platform mobile app that shares the same codebase with your web app).
    - React Native allows you to build native iOS and Android apps using JavaScript.
    - Use `useState`, `useEffect`, and `useCallback` for managing state and optimizing performance.
- NPM
	- redux - figured it would be good for a small scale project like this. Easier to manage the state and keep everything centralized. Might need to look into redux toolkit in the future if I wanted to scale up this project to help manage state in smaller units
	- material ui - easy and intuitive way to build components without me having to build everything from scratch. Need to look into styled components to customize the components
	- axios - one of the most popular npm to fetch data from an api
		- implemented with swr
	- react toastify - easy way to handle notifications
	- react router dom - used to set up routing in my app
	- 

#### 2. **Cross-Platform Framework**:

- If you want a single codebase for both web and mobile, use **React Native** with **JavaScript**.
- If you prefer to keep the web and mobile apps separate but share some core logic, consider using:
    - **React** (for the web frontend) and **React Native** (for the mobile app).

#### 3. **Backend**:

- **C#**
- Use **.NET Core** (formerly ASP.NET Core) for building RESTful APIs.
- Example: Create a backend API using ASP.NET Core to handle appointment booking, user authentication, and data storage.

#### 4. **Database**:

- **Postgres**  (for storing appointments, client information, and business hours).
- Use **Dapper** in .NET Core to work with PostgreSQL
- This database is designed to manage appointments for a nail technician business. Here's a breakdown of your tables and how they interact:
1. **`clients` Table:**
    - **Purpose:** Stores information about your customers.
    - **Key Columns:** `id` (unique identifier for each client), `first_name`, `last_name`, `email`, `phone`, `date_of_birth`.
    - **Relationships:** This table is referenced by the `appointments` table to link an appointment to a specific client.
2. **`technicians` Table:**
    - **Purpose:** Stores information about the nail technicians who provide services.
    - **Key Columns:** `id` (unique identifier for each technician), `first_name`, `last_name`, `email`, `phone`.
    - **Relationships:** This table is referenced by the `appointments` table to assign a technician to an appointment.
3. **`services` Table:**
    - **Purpose:** This table acts as a catalog of all the different services your business offers.
    - **Key Columns:** `id` (unique identifier for each service type), `service_name`, `description`, `duration` (standard time it takes), `price`.
    - **Note on `appointment_id`:** Your current `services` table has an `appointment_id` column. If you are using the `appointment_services` junction table (described below) to link services to appointments (which is generally recommended for flexibility, allowing multiple services per appointment), then the `appointment_id` column in this `services` table becomes redundant and should ideally be removed. The `services` table would then purely define _what_ services are available, not _which specific appointment_ a service instance belongs to.
    - **Relationships:** This table is referenced by the `appointment_services` table.
4. **`appointments` Table:**
    - **Purpose:** This is a central table that records scheduled appointments.
    - **Key Columns:** `id` (unique identifier for each appointment), `client_id` (links to a client), `technician_id` (links to a technician), `appointment_date`, `appointment_time`, `duration` (overall appointment duration, if different from sum of services), `status` (e.g., 'Scheduled', 'Completed'), `notes`.
    - **Relationships:**
        - Links to `clients` via `client_id`.
        - Links to `technicians` via `technician_id`. is missing the `FOREIGN KEY` constraint for `technician_id` referencing `technicians(id)`. You should add this for data integrity: `CONSTRAINT appointments_technician_id_fkey FOREIGN KEY (technician_id) REFERENCES technicians(id)`).
        - Is referenced by the `appointment_services` table.
5. **`appointment_services` Table (Junction Table):**
    - **Purpose:** This table creates a many-to-many relationship between `appointments` and `services`. This means a single appointment can include multiple services, and a single type of service can be part of many different appointments.
    - **Key Columns:** `appointment_id` (links to an appointment), `service_id` (links to a service). The combination of these two forms the primary key, ensuring a service is not listed twice for the same appointment.
    - **Relationships:**
        - Links to `appointments` via `appointment_id`.
        - Links to `services` via `service_id`.
**How they work together:**
6. A **Client** (from `clients`) books an **Appointment** (recorded in `appointments`).
7. The **Appointment** is assigned to a **Technician** (from `technicians`).
8. The **Appointment** will consist of one or more **Services** (defined in the `services` table as a catalog).
9. The `appointment_services` table links the specific **Appointment** to the specific **Services** chosen for that appointment. For example, if appointment `A1` includes services `S1` (Manicure) and `S2` (Pedicure), the `appointment_services` table would have two entries: (`A1`, `S1`) and (`A1`, `S2`). This is to reduce redundancy and load on services table

This structure allows you to manage clients, technicians, the services you offer, and the appointments that bring them all together, including which specific services are performed during each appointment.



#### 5. **Authentication**:

- Integrate aws cognito for user authentication.
- Auth0 allows easy implementation of email/password, Google Sign-In, Facebook Sign-In, etc., across both web and mobile apps.
- User Flow should be:
	- Sign up:
		- add info
		- send to backend and get the cognito sub user id
		- add record to the clients table
		- confirm account with code by sending back the email only (no password)
		- user is directed to the login page to log in
		- notes
			- not the best for ux but it is more secure
	- login
		- login using email or password
		- make a call to the backend to get user profile as well to add to the context
	- sign out
		- clear tokens and clear user profile

#### 6. **Push Notifications**:

- Use **Firebase Cloud Messaging (FCM)** for Android push notifications.
- For iOS, use **Apple Push Notification Service (APNS)**.
- Integrate push notifications to remind users of their appointments.

#### 7. **Hosting & Deployment**:

- Use **Azure App Service** for hosting both your web app and mobile app.
- Use **Docker** for containerized deployment of your backend services.
- For the frontend, use **React Native** with **Expo** (for easy debugging and testing).

#### 8. **Tools & Libraries**:

- **Postman** or **Insomnia** for API testing.
- **Jenkins** or **GitHub Actions** for CI/CD pipelines.
- **Fiddler** or **Charles Web Debugging Proxy** for troubleshooting HTTP requests.


Notes:
- Just do regular aws cognito sign in for now, in the future I'll want to use google oauth for third party sign ins