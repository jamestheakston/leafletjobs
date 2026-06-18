# Leaflet Jobs

An Indeed-style job board application built with Clerk authentication and Supabase backend.

## Features

- **User Authentication**: Sign up and sign in using Clerk
- **Job Search**: Search jobs by keyword, location, job type, experience level, and salary range
- **Job Listings**: Browse job listings with Indeed-style cards
- **Post Jobs**: Authenticated users can post new job listings
- **Modern UI**: Clean, responsive design with Tailwind CSS
- **Real-time Updates**: Jobs are fetched from Supabase in real-time

## Setup Instructions

### 1. Clerk Setup

1. Go to [Clerk Dashboard](https://dashboard.clerk.com/)
2. Create a new application or select an existing one
3. Navigate to **API Keys** page
4. Copy your **Publishable Key** and **Frontend API URL**
5. In `index.html`, replace:
   - `YOUR_PUBLISHABLE_KEY` with your Clerk Publishable Key
   - `YOUR_FRONTEND_API_URL` with your Clerk Frontend API URL (both occurrences)

### 2. Supabase Setup

1. Go to [Supabase Dashboard](https://supabase.com/dashboard)
2. Create a new project
3. Navigate to **Project Settings > API**
4. Copy your **Project URL** and **anon/public key**
5. In `index.html`, replace:
   - `YOUR_SUPABASE_URL` with your Supabase Project URL
   - `YOUR_SUPABASE_ANON_KEY` with your Supabase anon key

### 3. Database Schema

1. In Supabase Dashboard, navigate to **SQL Editor**
2. Open the `supabase-schema.sql` file in this repository
3. Copy and paste the SQL code into the SQL Editor
4. Click **Run** to execute the schema

This will create the following tables:
- `users` - User profiles synced with Clerk
- `jobs` - Job listings
- `job_applications` - Job applications
- `saved_jobs` - Saved jobs for users

### 4. Configure Clerk with Supabase (Optional)

To integrate Clerk with Supabase authentication:

1. In Clerk Dashboard, go to **Configure > SSO Connections**
2. Add a new SSO connection using **OIDC**
3. Use your Supabase project's OAuth configuration
4. Follow the [Clerk + Supabase integration guide](https://supabase.com/docs/guides/auth/third-party/clerk) for detailed steps

### 5. Run the Application

1. Open `index.html` in a web browser
2. Or serve it using a local server:
   ```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js (if you have http-server installed)
   npx http-server
   ```
3. Navigate to `http://localhost:8000`

## Usage

### For Job Seekers

1. **Browse Jobs**: View all available job listings on the homepage
2. **Search**: Use the search bar to find jobs by keyword or location
3. **Filter**: Apply filters for job type, experience level, and salary range
4. **Apply**: Click "Apply Now" on any job card (requires sign in)
5. **Save Jobs**: Click "Save" to bookmark jobs for later (requires sign in)

### For Employers

1. **Sign In**: Create an account or sign in
2. **Post Job**: Click the "Post Job" button in the navigation
3. **Fill Details**: Complete the job posting form with:
   - Job title
   - Company name
   - Location
   - Job type (Full-time, Part-time, Contract, Internship)
   - Experience level
   - Salary range
   - Job description
   - Requirements
4. **Submit**: Click "Post Job" to publish the listing

## Database Schema

### Users Table
- `id` (UUID) - Primary key, synced with Clerk user ID
- `email` (TEXT) - User email
- `first_name` (TEXT) - First name
- `last_name` (TEXT) - Last name
- `created_at` (TIMESTAMP) - Account creation date
- `updated_at` (TIMESTAMP) - Last update date

### Jobs Table
- `id` (UUID) - Primary key
- `title` (TEXT) - Job title
- `company` (TEXT) - Company name
- `location` (TEXT) - Job location
- `job_type` (TEXT) - Full-time, Part-time, Contract, Internship
- `experience_level` (TEXT) - Entry, Mid, Senior, Executive
- `salary_min` (INTEGER) - Minimum salary
- `salary_max` (INTEGER) - Maximum salary
- `description` (TEXT) - Job description
- `requirements` (TEXT) - Job requirements
- `posted_by` (UUID) - User ID who posted the job
- `created_at` (TIMESTAMP) - Posting date
- `updated_at` (TIMESTAMP) - Last update date

### Job Applications Table
- `id` (UUID) - Primary key
- `job_id` (UUID) - Reference to jobs table
- `user_id` (UUID) - Reference to users table
- `status` (TEXT) - Application status (pending, reviewed, accepted, rejected)
- `cover_letter` (TEXT) - Cover letter text
- `resume_url` (TEXT) - Resume file URL
- `created_at` (TIMESTAMP) - Application date

### Saved Jobs Table
- `id` (UUID) - Primary key
- `job_id` (UUID) - Reference to jobs table
- `user_id` (UUID) - Reference to users table
- `created_at` (TIMESTAMP) - Save date

## Security

The application uses Row Level Security (RLS) on Supabase to ensure:
- Users can only view and edit their own data
- Jobs are publicly readable but only editable by their creators
- Applications are only visible to the applicant and job poster

## Technologies Used

- **Clerk** - Authentication and user management
- **Supabase** - Database and backend
- **Tailwind CSS** - Styling
- **Font Awesome** - Icons
- **Google Fonts (Inter)** - Typography

## Demo Mode

If you open the application without configuring Clerk and Supabase credentials, it will display sample job listings for demonstration purposes. To use the full functionality with authentication and database operations, complete the setup steps above.

## Future Enhancements

- Job application form with file upload
- User profile pages
- Company profiles
- Email notifications for applications
- Advanced search with filters
- Job recommendations
- Analytics dashboard for employers

## License

This project is open source and available for personal and commercial use.
