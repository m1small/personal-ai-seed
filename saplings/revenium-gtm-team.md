# Revenium GTM Team Sapling

## Purpose

A Personal AI sapling for GTM (Go-to-Market) team members who need relationship management, sales development, and executive assistant capabilities. Pre-builds the infrastructure for CRM operations, contact management, identity resolution, and multi-channel outreach — so team members start with working structure instead of building from scratch.

## Source

`https://github.com/m1small/revenium-gtm-team-sapling`

## Audience

Revenium GTM team members — account executives, sales development reps, and customer-facing roles who need an AI system that manages relationships, tracks contacts, and supports outreach workflows.

## Pre-grown Branches

- **Relationship Management infrastructure** — Schema defining Canonical Identities, Communities, and Relationship Provenance. Processes for Identity Resolution, Network Proximity scoring, LinkedIn Data Maintenance, and Cross-Channel Enrichment. Layered data architecture (Identity → CRM → Personal RM → Community RM).
- **CRM data stores** — Pre-structured CSV stores for Active Contacts, Active Companies, Communication Log, Meeting Target Queue, Community Registry, Community Contacts, and LinkedIn connection stores. Empty headers, ready for data.
- **Sales Development agent template** — Research, enrichment, qualification, outreach drafting, CRM administration. Decision rules for Communication Boundary, Identity Resolution, and Dimension/Campaign production.
- **Executive Assistant agent template** — Situational briefings, priority surfacing, contact classification, routing. Decision rules for briefing format, response aging, and pre-meeting context.
- **Tool contract templates** — Setup guidance for Slack, Notion, Gmail, Google Calendar, Google Drive, Claude in Chrome, GitHub, Bitwarden, and Google Workspace API. Revenium workspace connection patterns.

## Customization Points

- **Persona** — Capture your communication style and professional voice. Template provided.
- **Product certification** — Add your product knowledge. Template provided.
- **Tool credentials** — Connect your accounts following the tool contract setup guidance.
- **Agent names** — Rename the Sales Development and Executive Assistant agents to match your vocabulary.
- **Domain knowledge** — Build certifications as you work. The system improves through use.
- **Personal RM** — The Personal RM layer is empty and private. Build it if you want non-professional relationship tracking.

## Tool Requirements

- Slack
- Notion
- Gmail
- Google Calendar
- Google Drive
- Claude in Chrome
- GitHub
- Bitwarden
- Google Workspace API

## Origin Tree

ms-os — Matt Small's Personal AI system, the first tree grown from the Personal AI seed.

## Notes

- This sapling intentionally excludes competitive intelligence, product positioning, and go-to-market certifications. Those contain proprietary knowledge and should be built by each team member through real work.
- The data store structure follows a Pyramid Layer architecture proven in the origin tree. Layer 1 (Canonical Identities) is Private. Layer 2 stores inherit their sharing classification: CRM is Shared, Personal RM is Private, Community RM is Selective.
- Agents start at Untrusted trust level regardless of the origin tree's trust levels. Trust is earned per individual, not inherited.
