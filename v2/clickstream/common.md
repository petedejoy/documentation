---
title: Common Fields
sidebar: platform_sidebar
---

## Context

| Field                    | Type
| ------------------------ | String |
| `anonymousId` (optional) | Object | A pseudo-unique substitute for User ID. This is for cases when you don't have an absolutely unique identifier. |
| `context` (optional)     | Object | Dictionary of extra information that provides useful context about a message that is not directly related to the API call |
| `integrations` (optional) | String | Dictionary of destinations to either enable or disable |
| `messageId` (implicit)   | Automatically collected, this is a unique identifier for each message that lets you find an individual message across the API |
| `receivedAt` (implicit)  | The timestamp of when a message is received by Astronomer |
| `sentAt` (optional)      | The timestamp of when a message is sent to Astronomer |
| `type` (implicit)        | Type of message, according to the API method |
