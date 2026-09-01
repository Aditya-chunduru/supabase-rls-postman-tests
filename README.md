# Supabase RLS & Auth Automation Collection

A Postman collection designed to test Row-Level Security (RLS) policies, automatically manage JWT token lifecycles, and execute automated validation pipelines via GitHub Actions for Supabase projects.

## Features
* **Auto-Authentication:** Automatically posts to Supabase's auth endpoint (/auth/v1/token) to generate and cache a fresh JWT using your credentials.
* **Global & Variable Flexibility:** Dynamically maps configuration via Postman variables or GitHub Actions workflow secrets.
* **RLS Validation:** Pre-configured test scripts to verify PostgREST behavior (handling 200, 404, and 401 responses) across protected endpoints.
* **CI/CD Integration:** Fully automated execution pipeline utilizing the Postman CLI and GitHub Actions.

## Quickstart Setup

1. **Import the Collection:** Clone this repository, then import the JSON file directly into Postman or use it directly within your local workspace directory.
  
2. **Configure Variables:** Set up the following variables either in your Postman Globals, Environment, or as GitHub Secrets (SUPABASE_ANON_KEY, USERS_EMAILS, USER_PASSWORDS):

* `supabase_url`: Your Supabase project URL (https://<project-ref>.supabase.co).
* `supabase_project_ref`: Your Supabase project reference ID.
* `supabase_anon_key`: Your Supabase public anonymous API key.
* `users_emails`: The email address of a test user in your Supabase Auth dashboard.
* `user_passwords`: The password for that test user.

 ### Managed Variables (Handled Automatically):    
   * `user_jwt` *(Auto-generated)*: Cached authentication token handled by the pre-request script.
   * `token_expiry` *(Auto-generated)*: Timestamp tracking token expiration for automatic background refreshes.
3. **Database Prerequisite:** Ensure you have a target table created in your Supabase database matching your RLS configuration.
4. **Run Collection:** Execute via Postman or trigger your GitHub Actions pipeline. The collection sequentially requests a token first, caches the JWT, and successfully validates your RLS-protected endpoints.



### Troubleshooting: 401 Unauthorized Errors: 
If your pipeline or local run returns a 401 Unauthorized status code during the authentication phase, verify the following common causes:

* **Email Confirmation Status:** Ensure the test user account in your Supabase dashboard (Authentication > Users) is marked as confirmed. Supabase blocks unconfirmed email logins by default.

* **Secret Mismatch:** Confirm that your GitHub repository secrets (SUPABASE_ANON_KEY, USERS_EMAILS, and USER_PASSWORDS) match the exact variable names expected by your workflow and contain no trailing whitespace or quotes.

* **Key Type:** Verify that SUPABASE_ANON_KEY is your project's public anonymous client key rather than the restricted service_role key.


### Manual Execution Tip:

If you are running the collection directly inside the Postman Desktop app and need to re-authenticate or debug manually, ensure the Get Auth Token request is explicitly set to the POST method hitting {{supabase_url}}/auth/v1/token?grant_type=password with your raw JSON payload containing "email" and "password", rather than executing it as a GET request against your database tables.
