# Notes App – Mobile Test Automation Framework

Automated UI test suite for a **Notes** mobile application, built using **Java** and **Appium**. The framework validates core note-taking functionality (create, edit, delete, search, pin, sort) across Android and/or iOS devices and emulators/simulators.

---

## Tech Stack

| Component        | Technology                          |
|-------------------|--------------------------------------|
| Language           | Java 11+                            |
| Automation Tool    | Appium (Java Client)                |
| Test Runner        | TestNG                              |
| Build Tool         | Maven                                |
| Design Pattern     | Page Object Model (POM)             |
| Reporting          | ExtentReports / Allure              |
| Driver Mgmt        | Appium Service Builder / UiAutomator2 (Android), XCUITest (iOS) |

---

## Prerequisites

Before running the tests, make sure the following are installed and configured:

- Java JDK 11 or higher
- Maven 3.6+
- Node.js and npm
- Appium Server (`npm install -g appium`)
- Appium drivers: `appium driver install uiautomator2` (Android) and/or `appium driver install xcuitest` (iOS, macOS only)
- Android Studio + SDK, with an emulator created (for Android)
- Xcode + Simulator (for iOS, macOS only)
- Appium Doctor for environment validation: `appium-doctor`

---

## Project Structure

```
notes-app-automation/
├── src/
│   ├── main/java/
│   │   ├── pages/              # Page Object classes (NoteListPage, AddNotePage, etc.)
│   │   ├── driver/             # Driver factory & capability setup
│   │   └── utils/              # Reusable helper methods (waits, gestures, etc.)
│   └── test/java/
│       ├── tests/              # Test classes (CreateNoteTest, EditNoteTest, etc.)
│       ├── base/               # BaseTest with setup/teardown logic
│       └── listeners/          # TestNG listeners (screenshots on failure, reporting)
├── src/test/resources/
│   ├── testdata/                # JSON/Excel/CSV test data
│   └── config.properties        # Platform, device, app path config
├── apps/                         # APK / IPA files under test
├── testng.xml                    # Test suite configuration
├── reports/                      # Generated test execution reports
├── pom.xml                       # Maven dependencies & build config
└── README.md
```

---

## Configuration

Update `src/test/resources/config.properties` with your environment details:

```properties
platformName=Android
deviceName=Pixel_5_API_33
appPath=apps/notes-app.apk
automationName=UiAutomator2
appiumServerUrl=http://127.0.0.1:4723
```

---

## Setup Instructions

1. Clone the repository
   ```
   git clone <repo-url>
   cd notes-app-automation
   ```
2. Install dependencies
   ```
   mvn clean install -DskipTests
   ```
3. Start the Appium server
   ```
   appium
   ```
4. Launch an emulator/simulator or connect a real device
5. Verify the device is detected
   ```
   adb devices
   ```
6. Update `config.properties` as needed
7. Run the tests (see below)

---

## Test Scenarios Covered

- App launch and home screen verification
- Create a new note with title and body
- Edit an existing note
- Delete a single note / delete multiple notes
- Search for a note by keyword
- Pin and unpin a note
- Verify notes list ordering (recent/alphabetical)
- Validate empty-state and field validation messages
- Negative scenarios (empty title, max character limit, etc.)

---

## Running Tests

Run the full suite:
```
mvn test
```

Run a specific TestNG XML suite:
```
mvn test -DsuiteXmlFile=testng.xml
```

Run on a specific platform:
```
mvn test -Dplatform=android
mvn test -Dplatform=ios
```

Run a single test class:
```
mvn test -Dtest=CreateNoteTest
```

---

## Reporting

Test execution reports (ExtentReports/Allure) are generated under the `reports/` directory after each run. Open the generated HTML file in a browser to view pass/fail status, execution time, and failure screenshots.

If using Allure:
```
allure serve reports/allure-results
```

---

## CI/CD Integration

This framework can be integrated into Jenkins, GitHub Actions, or GitLab CI by:
1. Installing Node.js, Appium, and Android SDK on the CI agent
2. Starting an emulator/simulator (or connecting to a device farm like BrowserStack/Sauce Labs)
3. Starting the Appium server in the background
4. Triggering `mvn test` as a build step
5. Publishing the generated report as a build artifact

---

## Best Practices Followed

- Page Object Model for maintainability and reusability
- Explicit waits instead of hard-coded sleeps
- Centralized driver/capability management
- Data-driven testing using external test data files
- Failure screenshots captured automatically via listeners

---

## Contributing

1. Create a feature branch (`git checkout -b feature/your-feature`)
2. Commit your changes with clear messages
3. Push the branch and open a pull request
4. Ensure all tests pass before requesting review

---

## License

This project is licensed under the MIT License.
