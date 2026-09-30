# AI-Powered-Personal-Diet-Planner-with-Cloud-Storage
NutriAI is an AI-powered personal diet planner built in Google Colab. It creates personalized meal plans using user goals, activity level, dietary preferences and allergies, while providing nutrition tracking, calorie and macro analytics, saved plans, and a professional interactive dashboard.
# ✦ NutriAI — AI-Powered Personal Nutrition & Diet Planner

> **Personalized nutrition planning, intelligent meal recommendations, real-time intake tracking, and data-driven analytics — built entirely in Google Colab.**

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python\&logoColor=white)](https://www.python.org/)
[![Gradio](https://img.shields.io/badge/Gradio-6.x-FF7C00?logo=gradio\&logoColor=white)](https://www.gradio.app/)
[![SQLite](https://img.shields.io/badge/Database-SQLite-003B57?logo=sqlite\&logoColor=white)](https://www.sqlite.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.2.3-150458?logo=pandas\&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-2.x-013243?logo=numpy\&logoColor=white)](https://numpy.org/)
[![Google Colab](https://img.shields.io/badge/Platform-Google%20Colab-F9AB00?logo=googlecolab\&logoColor=white)](https://colab.research.google.com/)

---

## 📌 Overview

**NutriAI** is an AI-powered personal nutrition and diet-planning application designed to help users organize their daily eating goals through personalized meal recommendations and nutrition tracking.

The system collects a user's profile information — including age, sex, height, weight, activity level, dietary preference, goal, allergies, cuisine preference, and budget — and uses this information to calculate estimated nutrition targets and generate a personalized daily meal plan.

The application also provides a professional analytics dashboard that reads data directly from the application's SQLite database, allowing users to monitor calorie intake, macronutrients, daily progress, and recent nutrition history.

The current implementation is designed as a **single-cell Google Colab application**, making it easy to demonstrate without requiring a separate frontend or backend development environment. The project requirements also describe a larger cloud-ready architecture, including authentication, database, storage, APIs, testing, and deployment concepts.

---

## 🎯 Problem Statement

Planning a balanced daily diet can be difficult when users have different:

* Nutritional goals
* Activity levels
* Body measurements
* Dietary preferences
* Food allergies
* Cuisine preferences
* Food budgets

Traditional diet-planning approaches often require manual calorie calculations, food selection, and progress tracking.

NutriAI addresses this problem by combining **personalized nutrition calculations, rule-based recommendation logic, structured food data, intake tracking, and visual analytics** into a single application.

---

## 💡 Objectives

The main objectives of NutriAI are to:

1. Create a personalized nutrition profile.
2. Estimate daily calorie requirements.
3. Calculate macronutrient targets.
4. Generate a personalized meal plan.
5. Filter food recommendations according to dietary preference and allergies.
6. Store user-specific data securely within the application database.
7. Track daily food intake.
8. Visualize actual nutrition data through an interactive dashboard.
9. Provide saved diet plans and CSV export.
10. Demonstrate practical concepts in AI, data processing, databases, UI development, and cloud-ready application design.

The broader project specification also identifies user authentication, protected dashboards, user-specific data, diet-plan generation, saved plans, files, and dashboard functionality as core application requirements.

---

# 🚀 Features

## 👤 Personal Profile

Users can maintain a personalized nutrition profile containing:

* Full name
* Age
* Sex
* Height
* Weight
* Activity level
* Dietary preference
* Nutrition goal
* Allergies
* Preferred cuisine
* Approximate daily food budget

The profile is stored in SQLite and is used as the input for nutrition calculations and meal recommendations.

---

## 🔐 User Authentication

NutriAI includes a local authentication layer with:

* User registration
* Login
* Logout
* Username validation
* Password hashing
* User-session handling

Passwords are stored as hashes rather than plain text.

> **Note:** This is an academic/local authentication implementation. It should not be treated as production-grade identity infrastructure.

---

## 🧮 BMR & TDEE Calculation

The application estimates:

* **BMR — Basal Metabolic Rate**
* **TDEE — Total Daily Energy Expenditure**
* Daily calorie target
* Protein target
* Carbohydrate target
* Fat target

The implementation uses the **Mifflin-St Jeor equation** for BMR and applies an activity multiplier to estimate TDEE.

The project specification similarly identifies macro/calorie calculation and rule-based recommendation logic as part of the planned AI engine.

---

## 🤖 Personalized Diet Planning

NutriAI generates a daily plan containing:

* ☀️ Breakfast
* 🥗 Lunch
* 🍎 Snack
* 🌙 Dinner

Each recommendation includes:

* Food item
* Serving size
* Calories
* Protein
* Carbohydrates
* Fat

The current recommendation engine uses a **rule-based personalization approach**, filtering food items according to dietary preferences and allergies before constructing the daily meal structure.

---

## 🥗 Dietary Preference Filtering

Supported preferences include:

* Vegetarian
* Vegan
* Non-vegetarian

Food recommendations are filtered according to the selected diet.

---

## ⚠️ Allergy Filtering

Users can specify allergies such as:

* Nuts
* Lactose
* Gluten
* Soy

Foods containing matching allergen tags are excluded from recommendations whenever possible.

---

## 📊 Professional Analytics Dashboard

The dashboard is designed as a nutrition command center rather than a raw database display.

It provides:

### Daily Energy

* Calories consumed
* Daily calorie target
* Percentage of target consumed
* Remaining calories

### Macronutrients

* Protein consumed vs target
* Carbohydrates consumed vs target
* Fat consumed vs target

### Visual Analytics

* 7-day calorie trend
* Macro distribution
* Calorie target comparison
* Meal/intake overview

### Profile Summary

* Current goal
* Diet preference
* Activity level
* Estimated TDEE

The dashboard is intentionally **data-driven**: analytics are based on saved profile information and recorded intake rather than generated placeholder values.

---

## 🍎 Daily Intake Tracking

Users can record:

* Food item
* Quantity in grams
* Date

NutriAI calculates the corresponding:

* Calories
* Protein
* Carbohydrates
* Fat

The entries are stored in SQLite and become available to the analytics dashboard.

---

## 📈 Seven-Day Analytics

The calorie trend uses the user's stored intake history over the previous seven days.

Days without recorded intake are represented as missing/no recorded data rather than fabricated nutrition values.

This allows the analytics view to distinguish between:

> **No data recorded**

and

> **Actual food intake**

which improves the credibility of the dashboard.

---

## 💾 Saved Nutrition Plans

Each generated plan can be stored in the database and retrieved later.

Saved plans contain:

* Generation timestamp
* Goal
* Calories
* Protein
* Carbohydrates
* Fat
* Complete plan details

---

## 📥 CSV Export

The latest generated nutrition plan can be exported as CSV for:

* Documentation
* Analysis
* Submission
* Record keeping
* Demonstration

---

# 🏗️ System Architecture

```text
                         USER
                           │
                           ▼
                 ┌───────────────────┐
                 │   Gradio Web UI   │
                 └─────────┬─────────┘
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
        Authentication   Profile       Intake
             │             │             │
             └─────────────┼─────────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │ Nutrition Engine  │
                 ├───────────────────┤
                 │ BMR               │
                 │ TDEE              │
                 │ Calorie Target    │
                 │ Macro Target      │
                 └─────────┬─────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │ Recommendation    │
                 │ Engine            │
                 ├───────────────────┤
                 │ Diet Filtering    │
                 │ Allergy Filtering │
                 │ Meal Generation   │
                 └─────────┬─────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │      SQLite       │
                 ├───────────────────┤
                 │ Users             │
                 │ Profiles          │
                 │ Intake            │
                 │ Saved Plans       │
                 └─────────┬─────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │ Analytics Engine  │
                 ├───────────────────┤
                 │ Daily Totals      │
                 │ Macro Analysis    │
                 │ 7-Day Trends      │
                 └─────────┬─────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │ Professional      │
                 │ Dashboard         │
                 └───────────────────┘
```

The larger project specification also defines a cloud-oriented architecture involving frontend, backend, AI engine, database service, storage service, tests, documentation, and deployment.

---

# 🛠️ Technology Stack

| Layer                 | Technology                 |
| --------------------- | -------------------------- |
| Platform              | Google Colab               |
| Programming Language  | Python                     |
| User Interface        | Gradio 6                   |
| Styling               | HTML + CSS                 |
| Data Processing       | Pandas                     |
| Numerical Computing   | NumPy                      |
| Visualization         | Matplotlib                 |
| Database              | SQLite                     |
| Recommendation Engine | Rule-based personalization |
| Export                | CSV                        |
| Deployment/Demo       | Gradio public link         |

---

# 🧠 AI / Recommendation Engine

The current system uses a **rule-based recommendation engine** rather than an external generative AI API.

### Processing flow

```text
User Profile
      ↓
Age / Sex / Height / Weight
      ↓
BMR Calculation
      ↓
Activity Multiplier
      ↓
TDEE
      ↓
Goal Adjustment
      ↓
Daily Calorie Target
      ↓
Macro Targets
      ↓
Dietary Filtering
      ↓
Allergy Filtering
      ↓
Meal Selection
      ↓
Personalized Daily Plan
```

This approach provides a deterministic baseline that is easy to explain, test, and run in Google Colab.

The broader project specification also proposes a rule-based baseline and discusses a possible Sentence-BERT similarity approach for more advanced recommendation functionality.

---

# 🗄️ Database Design

NutriAI uses SQLite for local structured data storage.

### Users

```text
users
├── id
├── username
├── password_hash
└── created_at
```

### Profiles

```text
profiles
├── username
├── name
├── age
├── sex
├── height
├── weight
├── activity
├── diet
├── goal
├── allergies
├── cuisine
├── budget
└── updated_at
```

### Intake

```text
intake
├── id
├── username
├── log_date
├── food
├── grams
├── calories
├── protein
├── carbs
├── fat
└── created_at
```

### Plans

```text
plans
├── id
├── username
├── created_at
├── goal
├── calories
├── protein
├── carbs
├── fat
└── plan_json
```

---

# ☁️ Cloud / Colab Architecture

The current version is intentionally **Colab-only**.

Therefore:

| Cloud Concept             | Current Implementation |
| ------------------------- | ---------------------- |
| Application runtime       | Google Colab           |
| Web interface             | Gradio                 |
| Database                  | SQLite                 |
| Local application storage | Colab filesystem       |
| Analytics                 | Python + Matplotlib    |
| Public demo               | Gradio sharing URL     |

This means the current version demonstrates the **architecture and application concepts**, but SQLite and the Colab filesystem are not equivalent to managed services such as Firestore or Firebase Storage.

The original project specification includes Firebase/database/object-storage architecture as a broader cloud deployment direction.

---

# 📁 Runtime Project Structure

When executed in Colab, NutriAI creates an application directory similar to:

```text
/content/NutriAI/
│
├── database/
│   └── nutriai.db
│
└── exports/
    └── NutriAI_<username>_<timestamp>.csv
```

The database stores application records while the export directory contains generated CSV files.

---

# ▶️ Installation & Setup

## Option 1 — Google Colab

### Step 1 — Open Google Colab

Go to:

```text
https://colab.research.google.com/
```

### Step 2 — Create a new notebook

Create a new Python notebook.

### Step 3 — Use a fresh runtime

For the most reliable installation, use:

```text
Runtime → Disconnect and delete runtime
```

Then reconnect.

### Step 4 — Paste the program

Copy the complete NutriAI Python program into **one Colab cell**.

### Step 5 — Run the cell

The program installs the required dependencies, initializes the database, constructs the UI, and launches the Gradio application.

### Step 6 — Open the Gradio URL

The final output provides a public Gradio URL.

Open that URL to access the application.

---

# 🧪 How to Use

## 1. Create an Account

Open:

```text
⌁ Account
```

Create a username and password.

---

## 2. Sign In

Use your credentials to start a NutriAI session.

---

## 3. Complete Your Profile

Open:

```text
◎ Profile
```

Enter:

```text
Name
Age
Sex
Height
Weight
Activity Level
Diet Preference
Nutrition Goal
Allergies
Cuisine
Budget
```

Then select:

```text
Save Nutrition Profile
```

---

## 4. Generate a Nutrition Plan

Open:

```text
✦ Nutrition Plan
```

Select:

```text
Generate Personalized Plan
```

NutriAI will generate a structured daily plan.

---

## 5. Track Intake

Open:

```text
＋ Intake
```

Select:

```text
Food
Quantity
Date
```

Then click:

```text
Record Intake
```

---

## 6. View Analytics

Return to:

```text
◈ Overview
```

Click:

```text
↻ Refresh Live Dashboard
```

The dashboard will update from the stored database records.

---

# 📊 Dashboard Data Flow

The dashboard follows this data flow:

```text
SQLite Intake Records
        ↓
Daily Aggregation
        ↓
Calories / Protein / Carbs / Fat
        ↓
Compare With Profile Targets
        ↓
Progress Calculation
        ↓
Charts + KPI Cards
        ↓
Professional Dashboard
```

No random intake values should be used to represent user activity.

---

# 🔒 Security Considerations

The project includes basic local security concepts:

* Password hashing
* Parameterized SQLite queries
* User-session state
* Username-based data separation
* Input validation

However, this is an academic Colab prototype and is **not intended to be a production authentication system**.

For production deployment, authentication should be replaced with a dedicated identity provider and session/token security should be implemented server-side.

The broader project specification also emphasizes authentication, authorization, password security, session concepts, and user isolation.

---

# ⚡ Performance Considerations

The current application is designed for:

* Demonstration
* Academic evaluation
* Prototyping
* Portfolio presentation
* Learning cloud/application concepts

SQLite is appropriate for this single-runtime prototype but is not intended to provide the scaling characteristics of a production managed database.

For a production deployment, the architecture could be upgraded to use:

```text
React / Next.js
        ↓
FastAPI / Flask
        ↓
Managed Database
        ↓
Object Storage
        ↓
Authentication Provider
```

---

# 🧪 Testing Checklist

Recommended tests include:

| Test                    | Expected Result                            |
| ----------------------- | ------------------------------------------ |
| New user registration   | Account created                            |
| Duplicate username      | Registration rejected                      |
| Valid login             | Session created                            |
| Invalid login           | Access rejected                            |
| Dashboard without login | Login-required message                     |
| Profile creation        | Profile stored                             |
| Valid BMR calculation   | Target generated                           |
| Diet plan generation    | Four meal sections generated               |
| Vegetarian preference   | Non-vegetarian foods excluded              |
| Vegan preference        | Animal-derived foods excluded where tagged |
| Allergy filter          | Matching allergens excluded                |
| Intake logging          | Entry stored                               |
| Dashboard refresh       | Current database values displayed          |
| Seven-day analytics     | Stored intake aggregated by date           |
| CSV export              | Plan exported successfully                 |
| Logout                  | Session cleared                            |

---

# 📈 Example User Flow

```text
Register
   ↓
Login
   ↓
Create Profile
   ↓
Calculate BMR / TDEE
   ↓
Set Nutrition Goal
   ↓
Generate Plan
   ↓
Save Plan
   ↓
Record Food Intake
   ↓
Refresh Dashboard
   ↓
Analyze Calories & Macros
   ↓
Export Plan
```

---

# 🖥️ Screenshots

Recommended screenshots for a GitHub repository:

```text
screenshots/
│
├── 01-account.png
├── 02-login-success.png
├── 03-profile.png
├── 04-generated-plan.png
├── 05-dashboard-overview.png
├── 06-calorie-chart.png
├── 07-macro-chart.png
├── 08-intake-tracker.png
├── 09-saved-plans.png
└── 10-colab-runtime.png
```

For a recruiter or evaluator, the most important screenshots are:

1. Professional dashboard
2. Generated personalized plan
3. Intake tracker
4. Calorie trend
5. Macro distribution
6. Profile personalization

The project specification also recommends documenting the dashboard, generated plan, profile, authentication, stored data, API/deployment proof where applicable, and repository history.

---

# 📌 Current Limitations

The current Google Colab implementation has several intentional limitations:

### 1. Local Database

SQLite is used instead of a managed cloud database.

### 2. Local Storage

Files/exports are stored within the Colab environment.

### 3. Rule-Based AI

The recommendation engine is rule-based rather than an advanced trained recommendation model.

### 4. Colab Runtime

Colab runtime storage is not equivalent to permanent production infrastructure.

### 5. Authentication

Authentication is suitable for demonstration and learning, not production identity management.

### 6. Nutrition Guidance

The application provides general wellness-oriented estimates and meal suggestions and should not be treated as clinical nutrition software.

---

# 🔮 Future Improvements

The project can be extended with:

* Firebase Authentication
* Firestore
* Firebase Storage
* FastAPI REST backend
* React frontend
* Cloud Run deployment
* Recommendation models
* Sentence-BERT food similarity
* Larger nutrition database
* Meal substitutions
* Weekly meal planning
* Shopping-list generation
* Cost estimation
* Water tracking
* Weight-progress tracking
* Push notifications
* Barcode scanning
* Food-image recognition
* AI conversational nutrition assistant
* PDF diet-plan reports
* User-specific cloud synchronization

The project specification explicitly identifies cloud database, cloud object storage, REST APIs, frontend/backend separation, testing, deployment, and future personalization as directions for a more complete version.

---

# 🎓 Learning Outcomes

By building NutriAI, the developer gains practical experience with:

* Python application development
* Data processing with Pandas
* Numerical computation with NumPy
* SQLite database design
* Authentication concepts
* Session handling
* Input validation
* Rule-based recommendation systems
* Nutrition calculations
* Data visualization
* Dashboard design
* Gradio UI development
* CSV data export
* Application architecture
* Cloud-ready design concepts
* Debugging dependency conflicts
* Building and presenting a complete prototype

---

# 🧩 Project Highlights

### What makes the project technically interesting?

**Personalization**

```text
User Profile
      ↓
Nutrition Targets
      ↓
Diet + Allergy Constraints
      ↓
Personalized Meal Plan
```

**Data-driven analytics**

```text
Food Intake
      ↓
SQLite
      ↓
Aggregation
      ↓
Dashboard
```

**Single-environment development**

```text
Google Colab
     ├── Python
     ├── Database
     ├── AI Engine
     ├── UI
     ├── Analytics
     └── Export
```

---

# 📜 Disclaimer

NutriAI is an **educational and general-wellness software prototype**.

The calorie targets, macro estimates, and meal recommendations generated by the application are intended for demonstration and planning purposes and should not be treated as medical, clinical, or individualized professional nutrition advice.

Users with medical conditions, allergies, specialized dietary requirements, or other health concerns should consult an appropriately qualified healthcare or nutrition professional.

---

# 👨‍💻 Author

**[Debankita Panja]**

GitHub: `https://github.com/dp2005-lang`

LinkedIn: `https://www.linkedin.com/in/debankita-8482a2403/`

---

# ⭐ Project Summary

**NutriAI** demonstrates how Python, structured food data, personalization logic, SQLite, data visualization, and Gradio can be combined to create a complete nutrition-planning application in Google Colab.

The application covers the complete core journey:

```text
Profile
   ↓
Nutrition Target
   ↓
Personalized Plan
   ↓
Intake Tracking
   ↓
Analytics Dashboard
   ↓
Export
```

The architecture can subsequently be evolved into a full cloud application with a dedicated frontend, REST backend, managed database, object storage, authentication, testing, and production deployment.
