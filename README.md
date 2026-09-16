## Close Job — Product Backlog Exercise

A product requirements and backlog breakdown exercise for the Close Job feature within a Job Applications Management system.

This exercise demonstrates how a business requirement can be translated into a structured PRD → Epic → User Stories → Tasks delivery plan.

## Business Problem

Recruiters sometimes need to stop accepting applications for a job when the position is filled or the hiring process is closed, but existing applications still need to be preserved and processed.

## Feature

**Close Job**

## Actor

**Recruiter**

## Business Rules

- Recruiter can only close their own jobs.
- Closing is allowed only while the job status is **Open**.
- Once closed, the job no longer accepts new applications.
- Existing applications are **not deleted or cancelled**.
- Existing applications keep their current status and can still be reviewed.
- A closed job cannot be closed again.

## Data Model Changes

- **Job:** Status → add **“Closed”**
- **Job:** `ClosedAt` → nullable timestamp

## API Endpoint

**PATCH**

`/api/jobs/{id}/close`

## Acceptance Criteria

- Job is **Open**, owned by requester → status becomes **Closed**, `ClosedAt` is recorded.
- Job is already **Closed** → API rejects the request.
- Job doesn't belong to the requester → **403 Forbidden**.
- New application for a **Closed** job → API rejects the application.
- Existing applications remain unchanged and accessible to the recruiter.

---

# Task 2 — Epic → Stories → Task Breakdown

## Epic

**Job Applications Management**

## User Stories

| Story | Acceptance Criteria | Priority | Points |
|---|---|---|---:|
| **Recruiter closes their own job**<br><br>As a Recruiter, I want to close my own open job, so that it stops receiving new applications. | Valid close while job is Open → status becomes Closed and `ClosedAt` is recorded | **High** | **2** |
| **Prevent closing an already closed job**<br><br>As a Recruiter, I want the system to stop me closing a job that is already closed, so that the job status remains consistent. | Close attempt on Closed job is rejected | **Medium** | **1** |
| **Preserve existing applications**<br><br>As a Recruiter, I want existing applications to remain available after closing a job, so that I can continue processing candidates who already applied. | Existing applications remain unchanged and accessible after the job is closed | **High** | **2** |

## Task Breakdown — Story 1: Recruiter Closes Their Own Job

- Add `Closed` status + `ClosedAt` field to Job (migration).
- Implement `PATCH /api/jobs/{id}/close` endpoint.
- Add validation — job status must be `Open`.
- Add validation — requester must own the job.
- Update job status to `Closed` and record `ClosedAt`.

---

## Jira Board

<img width="1843" height="877" alt="image" src="https://github.com/user-attachments/assets/3ca12b4f-5228-4c6c-b116-db79534e7585" />

---

**Exercise:** Close Job  
**Domain:** Job Applications Management  
**Artifact:** PRD & Agile Backlog Breakdown
