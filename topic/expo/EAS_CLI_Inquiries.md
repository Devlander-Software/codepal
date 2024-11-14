Here’s the **EAS CLI Inquiries** document in full detail:

---

**Filename:** `topic/expo/EAS_CLI_Inquiries.md`

---

# EAS CLI Inquiries

**Purpose**: This guide provides best practices for handling questions related to the EAS (Expo Application Services) CLI, covering topics like setting up builds, troubleshooting errors, and referencing documentation for effective use of EAS CLI in Expo projects.

---

## EAS CLI Inquiries

### 1. Understanding EAS CLI and Its Purpose
   - **Overview**: EAS CLI is a tool provided by Expo for managing builds, submitting apps to stores, and distributing builds. It is specifically designed to enhance the build and deployment process for Expo applications.
   - **Further Documentation**:
      - [EAS CLI Introduction](https://docs.expo.dev/eas/cli/)

### 2. Setting Up and Configuring EAS CLI
   - **Getting Started with EAS CLI**: The first step is to install EAS CLI and log in to your Expo account.
     ```bash
     npm install -g eas-cli
     eas login
     ```
   - **Further Documentation**:
      - [Setting Up EAS CLI](https://docs.expo.dev/eas/cli/#installation)

### 3. EAS Build Process and Configuration
   - **Understanding the Build Configuration**: EAS CLI uses an `eas.json` file to define configuration options for builds across different environments (e.g., development, production).
   - **Example `eas.json` Configuration**:
     ```json
     {
       "build": {
         "production": {
           "env": {
             "API_URL": "https://api.production.example.com"
           }
         },
         "development": {
           "env": {
             "API_URL": "https://api.staging.example.com"
           }
         }
       }
     }
     ```
   - **Why It’s Important**: Configuring `eas.json` correctly ensures that the build process aligns with environment-specific requirements.
   - **Further Reading**:
      - [EAS Build Configuration](https://docs.expo.dev/build/eas-json/)

### 4. Building Apps with EAS CLI
   - **Creating Builds with EAS CLI**: EAS CLI supports building apps for both Android and iOS with commands like `eas build -p android` and `eas build -p ios`.
   - **Example Command**:
     ```bash
     eas build -p android --profile production
     ```
   - **Further Documentation**:
      - [EAS Build Documentation](https://docs.expo.dev/build/introduction/)

### 5. Troubleshooting EAS Build Errors
   - **Consulting GitHub for Common Issues**: For EAS Build errors, check the [EAS Build GitHub Issues Page](https://github.com/expo/eas-build/issues) to find discussions, solutions, or potential workarounds from the Expo community.
   - **Example Error**:
     - If an Android build fails due to configuration issues, reviewing open issues may provide insights or configuration fixes.
   - **Further Documentation**:
      - [EAS Build Troubleshooting Guide](https://docs.expo.dev/build-reference/troubleshooting/)

### 6. Submitting to App Stores Using EAS CLI
   - **Using `eas submit`**: After building, you can use `eas submit` to upload builds directly to the Apple App Store or Google Play Store.
   - **Example Command**:
     ```bash
     eas submit -p ios --latest
     ```
   - **Why It’s Important**: EAS CLI simplifies the submission process, eliminating manual steps required to upload to app stores.
   - **Further Documentation**:
      - [EAS Submit Documentation](https://docs.expo.dev/submit/introduction/)

### 7. Managing Environment Variables in EAS CLI
   - **Setting Up Environment Variables**: EAS CLI supports environment variables to configure different settings for builds. Sensitive values can be securely stored and accessed within the `eas.json` file.
   - **Example**:
     ```json
     {
       "build": {
         "production": {
           "env": {
             "API_SECRET": "@env:API_SECRET"
           }
         }
       }
     }
     ```
   - **Further Reading**:
      - [EAS CLI Environment Variables](https://docs.expo.dev/build/environment-variables/)

### 8. Monitoring and Accessing Build Logs
   - **Build Logs for Debugging**: Accessing build logs helps diagnose issues that arise during the build process. Logs are available in the Expo dashboard for each build created with EAS CLI.
   - **Example**: If a build fails, examine the logs in the Expo dashboard under the Builds section for detailed error information.
   - **Further Documentation**:
      - [Accessing EAS Build Logs](https://docs.expo.dev/build-reference/view-logs/)

### 9. Using `eas update` for OTA Updates
   - **Over-the-Air Updates**: EAS CLI supports over-the-air (OTA) updates, allowing you to push updates to your app without requiring a full redeployment. Use `eas update` to deliver OTA updates to users.
   - **Example Command**:
     ```bash
     eas update --branch production
     ```
   - **Why It’s Useful**: OTA updates streamline the update process, providing a quick way to address issues or add small features.
   - **Further Reading**:
      - [EAS Update Documentation](https://docs.expo.dev/eas-update/overview/)

### 10. Using EAS CLI for Multiple Profiles
   - **Managing Multiple Profiles**: EAS CLI allows creating different profiles for various environments, such as development, staging, and production, which helps to streamline build management for different app versions.
   - **Example Configuration in `eas.json`**:
     ```json
     {
       "build": {
         "production": { ... },
         "staging": { ... },
         "development": { ... }
       }
     }
     ```
   - **Why It’s Important**: Profiles help organize builds for different environments and make it easier to deploy specific configurations without modifying code.
   - **Further Documentation**:
      - [Managing Build Profiles in EAS](https://docs.expo.dev/build/eas-json/#build-profiles)

