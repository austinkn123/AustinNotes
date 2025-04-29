
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
	- react toastify - easy way to handle notifications

#### 2. **Cross-Platform Framework**:

- If you want a single codebase for both web and mobile, use **React Native** with **JavaScript**.
- If you prefer to keep the web and mobile apps separate but share some core logic, consider using:
    - **React** (for the web frontend) and **React Native** (for the mobile app).

#### 3. **Backend**:

- **C#** (as requested).
- Use **.NET Core** (formerly ASP.NET Core) for building RESTful APIs.
- Example: Create a backend API using ASP.NET Core to handle appointment booking, user authentication, and data storage.

#### 4. **Database**:

- **SQL Server** or **Azure SQL Database** (for storing appointments, client information, and business hours).
- For the mobile app, you can use **SQLite** or **Realm** for local storage, but ensure synchronization with the backend database.
- Use **Dapper** in .NET Core to work with PosgreSQL

#### 5. **Authentication**:

- Integrate **Auth0** or **Azure Active Directory (AAD)** for user authentication.
- Auth0 allows easy implementation of email/password, Google Sign-In, Facebook Sign-In, etc., across both web and mobile apps.

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