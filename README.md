# Project - DOCS Invite Bot

## Overview
The following document serves as a record of the discussion between Gordon and Ducati Official Club Singapore (“DOCS”) represented by its Treasurer/Executive Committee Member, Nicholas Tan. DOCS is a non-profit society based in Singapore. The society uses, among other things, a private Telegram group as a communication channel between its Executive Committee (“the Committee”) and its members for disbursement of information to its members.

The agreement was for Gordon to develop a Telegram bot (“the Bot”) for DOCS on a pro bono basis, that aims to grant the Committee an automated way to control entrants to its group, while minimizing both unauthorized entrants and the need for manual intervention by administrators.

## Problem Statement
DOCS currently receives around 10 new Telegram group join requests per month. With only a few active administrators and their limited availability on weekday nights/weekends, this volume is difficult to handle manually.

The open invite links used today allow anyone access if shared widely, posing privacy and spam risks for the 400+ existing members. Unauthorized members also utilize member services and clutter valuable conversation channels.

Scalability is also an issue - manual vetting of all entries does not allow DOCS to grow membership easily, restricting the growth of the enthusiast community. Misuse issues may also increase with more members added via open invites versus careful screening.

## Solution 

The project involves the development of a Telegram bot integrated with a Firebase database, aimed at optimizing the process of adding new members to the DOCS Telegram group. 
Key components of this solution include:
- **Automated Whitelist Verification**: The bot checks each new member request against a whitelist stored in Firebase.
- **Admin Interface for Whitelist Management**: Administrators can manage the whitelist through the bot, with functionalities like CSV uploads and add/remove commands.
- **One-time Invite Links**: Verified applicants receive a one-time use invite link for group access.

Firebase is utilized for its serverless infrastructure, supporting backend processes and enabling a focus on functionality and user experience.

## Key Benefits
The solution provides several critical benefits, enhancing both the efficiency and security of the DOCS Telegram group management:
- **Operational Efficiency**: Automates the member verification process, significantly reducing manual administrative tasks.
- **Enhanced Security**: One-time use invite links ensure controlled and exclusive access to the Telegram group.
- **Round-the-Clock Accessibility**: The bot operates continuously, offering immediate response to membership requests and reducing dependency on administrator availability.
- **Seamless Integration**: The use of Telegram for the bot aligns with the existing communication platform used by DOCS, ensuring a cohesive experience for both administrators and members.

## Project Scope
The scope of this project is focused on delivering an efficient, secure, and user-friendly tool for managing the DOCS Telegram group membership. It addresses the specific needs identified by the community, providing immediate improvements in operational efficiency and group security. The current implementation effectively meets these needs, with the potential for future enhancements if required.

## Business Requirements 

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
**User Story**: As a new member, I am seeking a hassle-free way to join the official Telegram group.

- **Business Requirement**:
  - Cost-effective solution to generate one-time use invite links round the clock.
  - Automated authorization of entry.

### User Persona: Executive Committee
**User Story**: As an Executive Committee member, I want to ensure secure and controlled access to the group.

- **Business Requirement**:
  - Bot checks input phone number against whitelist database before sending invite link, to restrict unauthorized entries.

### User Persona: Whitelist Manager / Group Administrator
**User Story**: As an Admin of the Telegram group, I want an easy way to manage group membership and ensure group privacy.

- **Business Requirement**:
  - Upload/export whitelist via CSV file.
  - Add/remove numbers from the whitelist.
  - Check if numbers are on the whitelist.
  - Only allow admins to access management functions.


## Technical Requirements and Considerations

### Choice of Firebase
- **Integration with Google Cloud Platform**: Firebase, as a part of the Google Cloud ecosystem, offers seamless integration, making it an ideal choice for backend services.
- **Serverless Architecture**: Firebase's serverless infrastructure aligns well with the need for a scalable, maintenance-free backend.
- **Cost-Effectiveness**: Leveraging Firebase and Google Cloud’s generous free tier keeps the infrastructure costs minimal, an important consideration for a pro bono project.

### Learning and Implementing Cloud Functions
- **Serverless Instances**: The project provided an opportunity to explore Google Cloud Functions, a serverless computing solution. This approach eliminated the need for a continuously running server, reducing operational complexity and cost.
- **Challenges of Serverless Architecture**: Adapting to the stateless nature of serverless functions meant rethinking data persistence strategies. Unlike traditional server-based applications, serverless instances do not maintain in-memory variables across calls.

### Infrastructure and Bot Interaction
- **Webhook Configuration**: Setting up a webhook with Telegram enabled efficient bot-server communication, crucial for real-time responsiveness.
- **Robust and Scalable**: The chosen architecture ensures that the bot remains reliable and scalable, capable of handling varying loads without additional configuration.

### Administrator Whitelist Management
- **Enhanced User Experience**: To limit direct interaction with the Firestore database by administrators, bot-based management functions were developed.
- **Intuitive Backend Interaction**: The bot provides a user-friendly interface for on-the-fly whitelist management, reducing reliance on manual methods like Excel.
- **Flexibility in Management**: This approach allows administrators to dynamically manage member access, aligning with the needs of a growing and active community.

The technical architecture of this project not only addresses the immediate functional requirements but also provides a foundation that is scalable, cost-effective, and adaptable for potential future enhancements.

## Security and Admin Privileges

### Persistent Admin Access via Database
- **Manual Granting of Admin Rights**: Admin privileges are controlled directly through the Firestore database. This ensures a secure and controlled process for granting access.
- **Revocation of Access**: Admin rights can be manually revoked by signing into the Firebase console, providing a straightforward method for managing admin access.

### Two-Layer Security for Admin Authentication
- **Database-Level Control**: Admin access is initially granted by setting the `is_admin` flag in Firestore. This level of control is safeguarded by Google's secure login system, requiring direct access to the Firebase account.
- **Password Authentication**: Once a user has admin rights in the database, they must authenticate their privileges within the Telegram bot using a password. This adds an additional layer of verification.

### Enhanced Security for Personal Identifiable Information (PII)
- **Handling Sensitive Data**: As the bot handles phone numbers, a form of PII, robust security measures are crucial.
- **Separation of Privileges**: The necessity for both database-level access and a password within the bot to gain admin privileges significantly reduces the risk of unauthorized access.
- **Bypassing UI Limitations for Passwords**: Due to the inability of Telegram's chat UI to hide passwords, the two-step process involving Firebase and the bot itself offers a secure workaround.

### Rationale
- **Secured Admin Onboarding**: The process to enable new admin rights is secure, as it requires access to the Firebase account, which is protected by Google's authentication mechanisms.
- **Operational Security**: This layered approach to security ensures that even if the Telegram bot interface is compromised, administrative control over the bot and its data remains protected.

The security design for admin privileges in this project is built to safeguard against unauthorized access, particularly important due to the handling of personal identifiable information. It represents a balance between operational functionality and stringent security measures.






