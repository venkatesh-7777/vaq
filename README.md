# AI Judge System

A comprehensive digital court system powered by Google's Gemini 2.5 Flash AI, featuring real-time case management, document analysis, and intelligent legal reasoning.




## 🏗️ Architecture

### Backend Structure
```
backend/
├── index.js                    # Express server with Socket.IO
├── config/
│   ├── database.js            # MongoDB connection
│   ├── multer.js              # File upload configuration
│   └── supabase.js            # Supabase client setup
├── models/
│   └── Case.js                # MongoDB case schema
├── routes/
│   ├── case.js                # Individual case operations
│   ├── cases.js               # Multiple cases & statistics
│   └── upload.js              # Document upload endpoints
├── services/
│   ├── geminiService.js       # AI integration service
│   ├── caseService.js         # Case data management
│   └── documentParser.js      # Document processing
├── scripts/
│   ├── seedDatabase.js        # Database seeding
│   └── migrateToCloud.js      # Cloud migration utility
└── .env                       # Environment configuration
```

### Frontend Structure
```
frontend/
├── src/
│   ├── components/            # React components
│   │   ├── Dashboard.jsx      # Main dashboard with analytics
│   │   ├── CaseView.jsx       # Case management & document upload
│   │   ├── CreateCase.jsx     # Case creation form
│   │   ├── GooeyNav.jsx       # Animated navigation
│   │   └── Header.jsx         # App header
│   ├── stores/               # Zustand state management
│   │   └── useAIJudgeStore.js
│   ├── index.css             # Global Tailwind styles
│   ├── App.jsx               # Main app component
│   └── main.jsx              # React entry point
├── public/                   # Static assets
├── vite.config.js            # Vite configuration
└── package.json              # Frontend dependencies
```



## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/nithinmouli/venky.git
cd venky
```

### 2. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Create environment file
cp .env.example .env
```

### 3. Environment Configuration

Create a `.env` file in the `backend` directory with the following configuration:

```bash
# Google Gemini API Configuration
GEMINI_API_KEY=your_gemini_api_key_here

# MongoDB Configuration
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/database_name?retryWrites=true&w=majority

# Server Configuration
PORT=3001
NODE_ENV=development

# Upload Configuration
MAX_FILE_SIZE=10485760

# Supabase Configuration
SUPABASE_URL=your_supabase_project_url
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
STORAGE_BUCKET=your_bucket_name

# Frontend URL (for CORS)
FRONTEND_URL=http://localhost:5173
```

### 4. Get Required API Keys

#### Google Gemini API Key:
1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy the generated key to your `.env` file

#### MongoDB Connection:
1. Create account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster (free tier available)
3. Go to Database Access → Add Database User
4. Go to Network Access → Add IP Address (0.0.0.0/0 for development)
5. Go to Database → Connect → Connect your application
6. Copy the connection string and update your `.env` file

#### Supabase Configuration:
1. Create account at [Supabase](https://supabase.com/)
2. Create a new project
3. Go to Settings → API to get your URL and service role key
4. Go to Storage → Create a new bucket for file uploads
5. Update your `.env` file with these values

### 5. Frontend Setup

```bash
# Navigate to frontend directory (from project root)
cd frontend

# Install dependencies
npm install
```

### 6. Database Setup (Optional)

If you want to seed the database with sample data:

```bash
# From backend directory
npm run seed
```

## 🏃‍♂️ Running the Application

### Development Mode

You'll need **two terminal windows**:

#### Terminal 1 - Backend Server:
```bash
cd backend
npm run dev
```
The backend server will start on `http://localhost:3001`

#### Terminal 2 - Frontend Development Server:
```bash
cd frontend
npm run dev
```
The frontend will start on `http://localhost:5173`

### Production Mode

#### Build Frontend:
```bash
cd frontend
npm run build
```

#### Start Production Server:
```bash
cd backend
npm start
```

## 🔗 Application URLs

- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:3001
- **Health Check**: http://localhost:3001/api/health

## 📋 Usage Workflow

### Creating a Case

1. **Access Dashboard**: Navigate to http://localhost:5173
2. **Create New Case**: Click "Create Case" button
3. **Fill Case Details**:
   - Case title (e.g., "Software Contract Dispute")
   - Description
   - Case type (Civil, Criminal, Corporate, etc.)
   - Jurisdiction/Country
   - Plaintiff (Side A) description
   - Defendant (Side B) description

### Document Upload Process

1. **Navigate to Case**: Click on a case from the dashboard
2. **Upload Documents**: 
   - Drag and drop files or click to browse
   - Supported formats: PDF, DOC, DOCX, TXT
   - Maximum file size: 10MB per file
   - Add optional descriptions for document context
3. **Automatic Processing**: Documents are processed and text is extracted
4. **Status Updates**: Case status automatically changes when both sides have evidence

### AI Judgment Process

1. **Ready for Judgment**: When both sides have uploaded documents
2. **Request Verdict**: Click "Analyze Case & Render Verdict"
3. **AI Analysis**: System sends case data to Gemini AI for analysis
4. **Verdict Display**: Receive comprehensive verdict with:
   - Legal decision
   - Detailed reasoning
   - Key factual findings
   - Applicable legal principles
   - Confidence score (0-100%)

### Follow-up Arguments

1. **Submit Arguments**: Either side can present additional arguments
2. **AI Response**: Judge analyzes new arguments and may:
   - Maintain original verdict
   - Make minor modifications
   - Significantly change verdict
   - Completely reverse decision
3. **Real-time Updates**: All changes appear immediately via WebSocket

## 🔧 API Endpoints

### Case Management
- `POST /api/case/create` - Create new case
- `GET /api/case/:id` - Get specific case details
- `POST /api/case/:id/judge` - Request AI verdict
- `POST /api/case/:id/argue` - Submit legal argument

### Cases & Statistics
- `GET /api/cases` - List all cases
- `GET /api/cases/search` - Search cases with criteria
- `GET /api/cases/stats` - Get system statistics

### Document Upload
- `POST /api/upload/side-a` - Upload documents for plaintiff
- `POST /api/upload/side-b` - Upload documents for defendant

### System
- `GET /api/health` - Health check endpoint
- `GET /api/stats` - System statistics

## 🛠️ Development

### Code Organization

**Backend Services**:
- `geminiService.js`: AI integration and prompt engineering
- `caseService.js`: Database operations and case management
- `documentParser.js`: File processing and text extraction

**Frontend Components**:
- `Dashboard.jsx`: Main analytics and case overview
- `CaseView.jsx`: Individual case management, document upload, and verdict interaction
- `CreateCase.jsx`: Case creation form with validation
- `GooeyNav.jsx`: Animated navigation component

**State Management**:
- Zustand store for global state
- Real-time WebSocket updates
- Optimistic UI updates

### Available Scripts

#### Backend:
```bash
npm start          # Start production server
npm run dev        # Start development server with nodemon
npm run seed       # Seed database with sample data
npm run migrate:cloud  # Migrate files to cloud storage
```

#### Frontend:
```bash
npm run dev        # Start Vite development server
npm run build      # Build for production
npm run preview    # Preview production build
npm run lint       # Run ESLint
```




### Environment Setup
```bash
NODE_ENV=production
GEMINI_API_KEY=your_production_key
MONGO_URI=your_production_mongodb_uri
SUPABASE_URL=your_production_supabase_url
SUPABASE_SERVICE_ROLE_KEY=your_production_key
PORT=3001
```

### Build Process
```bash
# Build frontend
cd frontend
npm run build

# Start production server
cd backend
npm start
```
