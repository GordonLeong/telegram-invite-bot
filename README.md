# Personal Project - DOCS Invite Bot

## Overview
The following document serves as a record of the discussion between Gordon and Ducati Official Club Singapore (“DOCS”) represented by its Treasurer/Executive Committee Member, Nicholas Tan. DOCS is a non-profit society based in Singapore. The society uses, among other things, a private Telegram group as a communication channel between its Executive Committee (“the Committee”) and its members for disbursement of information to its members.

The agreement was for Gordon to develop a Telegram bot (“the Bot”) for DOCS on a pro bono basis, that aims to grant the Committee an automated way to control entrants to its group, while minimizing both unauthorized entrants and the need for manual intervention by administrators.

## Problem Statement
DOCS currently receives around 10 new Telegram group join requests per month. With only a few active administrators and their limited availability on weekday nights/weekends, this volume is difficult to handle manually.

The open invite links used today allow anyone access if shared widely, posing privacy and spam risks for the 400+ existing members. Unauthorized members also utilize member services and clutter valuable conversation channels.

Scalability is also an issue - manual vetting of all entries does not allow DOCS to grow membership easily, restricting the growth of the enthusiast community. Misuse issues may also increase with more members added via open invites versus careful screening.

## Solution

I have designed a Telegram bot that connects to a Firebase database for automated whitelist checking before allowing new group member requests.

Administrators manage member entries in the Firebase database via CSV upload or add/remove operations through the bot interface.

New member applicants engage the bot to get one-time invite links if they provide a phone number that matches the whitelist. The links are good for one-time use only and never expire.

A key benefit is round the clock self-service access. Applicants receive automated screening results in seconds rather than waiting for administrator availability. This drastically reduces administrative workload.

I chose Telegram because DOCS' existing member Telegram group is the target access point for applicants. Tight integration was needed with the platform holding the current community.

Firebase, owned by Google Cloud, provides a secure and reliable serverless backend to focus efforts on the bot delivery versus infrastructure maintenance at this stage.

Planned future functionality includes timed link expiration, usage analytics, whitelist version histories, and more to incrementally expand on the core automation capabilities.

## Business Requirements Document

### Gathering Business Requirements
I conducted a comprehensive business requirements interview with Nicholas Tan, the key stakeholder and committee member of the motorcycle club, to understand their needs and constraints.

The main goals we identified were:
- Automate entry approval process to reduce manual checks by administrators
- Restrict one-time invite links to only whitelisted members to improve security
- Easy to manage whitelist additions/removals for administrators
- Cost-effective solution given non-profit status

The final set of business requirements are summarised as follows:


## Feature: Invite Link Generator

### User Persona: New Members of DOCS
**User Story**: As a new member, I need a way to easily join the Official Telegram group.

- **Business Requirement**:
  - Cost-effective solution to generate one-time use invite links round the clock.
  - Automated authorization of entry.

### User Persona: Executive Committee
**User Story**: As an Executive Committee member, I want to restrict unauthorized entries to the group.

- **Business Requirement**:
  - Bot checks input phone number against whitelist database before sending invite link, to restrict unauthorized entries.

### User Persona: Whitelist Manager / Group Administrator
**User Story**: As an Admin of the Telegram group, I want to easily review and manage group membership by managing the whitelist.

- **Business Requirement**:
  - Upload/export whitelist via CSV file.
  - Add/remove numbers from the whitelist.
  - Check if numbers are on the whitelist.
  - Only allow admins to access management functions.





