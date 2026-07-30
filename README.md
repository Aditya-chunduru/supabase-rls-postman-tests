# Supabase RLS & Automated Postman Testing Suite

A lightweight API testing and back-end security verification suite designed to test Row-Level Security (RLS) policies and automate dynamic JWT authentication in Postman.

## Overview

Because Postman collection exports exclude runtime credentials for security reasons, this repository contains the raw request collection configured with pre-request scripts to automatically handle Supabase authentication and validate data isolation at the database layer.

## Setup & Usage Instructions

### 1. Import the Collection
1. Download the `supabase-rls-testing.postman_collection.json` file directly from this repository.
2. Open **Postman**.
3. Click **Import** in the top left and drag or select the downloaded JSON file into your workspace.

### 2. Configure Postman Globals
Before running any requests, you must configure the following **Global Variables** in your Postman workspace so the automated pre-request script can successfully fetch your auth token:

1. Click the gear/environment icon or go to **Globals** in your Postman workspace.
2. Add the following keys and populate them with your project details:

| Variable Key | Description | Example Value |

| `supabase_url` | Your project's Supabase API URL | `https://xyzcompany.supabase.co` |

| `supabase_anon_key` | Your public Supabase anonymous API key | `eyJhbGciOi...` |

| `user_email` | Test account email address | `user@example.com` |

| `user_password` | Test account password | `your_secure_password` |


### 3. Run the Requests
Once your global variables are set, send any request in the collection. The pre-request script will automatically authenticate against Supabase, inject the fresh JWT into your headers, and allow you to verify that your RLS policies correctly filter and isolate data.
