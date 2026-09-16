## Close Job — Product Backlog Exercise

A product requirements and backlog breakdown exercise for the Close Job feature within a Job Applications Management system.

This exercise demonstrates how a business requirement can be translated into a structured PRD → Epic → User Stories → Tasks delivery plan.

**Business Problem:**

Recruiters sometimes need to stop accepting applications for a job when the position is filled or the hiring process is closed, but existing applications still need to be preserved and processed.

**Feature:** Close Job

**Actor:** Recruiter

### Business Rules

-  Recruiter can only close their own jobs. 
-  Closing is allowed only while the job status is **Open**. 
-  Once closed, the job no longer accepts new applications. 
-  Existing applications are **not deleted or cancelled**. 
-  Existing applications keep their current status and can still be reviewed. 
-  A closed job cannot be closed again. 

### Data Model (delta)

- **Job:** Status → add **“Closed”** 
- **Job:** `ClosedAt` → nullable timestamp 

### API Endpoints

**PATCH**

`/api/jobs/{id}/close`

### Acceptance Criteria

-  Job is **Open**, owned by requester → status becomes **Closed**, `ClosedAt` is recorded. 
-  Job is already **Closed** → API rejects the request. 
-  Job doesn't belong to the requester → **403 Forbidden**. 
-  New application for a **Closed** job → API rejects the application. 
-  Existing applications remain unchanged and accessible to the recruiter. 
