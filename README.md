# Supabase RLS & Auth Automation Collection

A Postman collection designed to test Row-Level Security (RLS) policies and automatically manage JWT token lifecycles for Supabase projects.

## Features
* **Auto-Authentication:** Automatically requests a fresh JWT from Supabase using your credentials when your token is missing or expires.
* **Environment & Global Flexibility:** Supports both Postman Environments and Global variables, allowing you to keep your workspace organized.
* **RLS Validation:** Pre-configured test scripts to verify PostgREST behavior (handling `200`, `404`, and `401` responses) when unauthorized or unauthenticated.

## Quickstart Setup

1. **Import the Collection:** Download or clone this repository, then import the JSON file directly into Postman.
2. **Configure Variables:** Set up the following variables either in your Postman Globals or inside a dedicated Postman Environment:
   * `supabase_project_ref`: Your Supabase project reference ID.
   * `supabase_anon_key`: Your Supabase public anonymous API key.
   * `user_email`: The email address of a test user in your Supabase Auth dashboard.
   * `user_password`: The password for that test user.
3. **Database Prerequisite:** Ensure you have a target table created in your Supabase database matching your RLS configuration.
4. **Run Requests:** Hit send on any request. The pre-request script will automatically authenticate in the background, cache your token, and execute your tests.
