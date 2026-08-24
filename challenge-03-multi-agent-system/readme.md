Challenge 3 – Multi-Agent Travel Assistant

This challenge extends the previous weather agent into a multi-agent system using Google ADK. A root LlmAgent coordinates between a weather specialist and a Google Search specialist. The weather agent is configured as a normal sub-agent and uses Google Maps Geocoding plus the National Weather Service API, while the search agent uses the ADK built-in Google Search tool and is exposed to the root through AgentTool.

Demonstrates both sub-agent handoff and agent-as-tool patterns.
Uses one persistent session to preserve context across multiple user requests.
Shows event authors to demonstrate agent routing and delegation.
Retains Challenge 2 prompt logging, response logging, U.S.-location validation, and unsafe-input validation.
Includes multi-turn tests covering weather, destination research, and contextual follow-up questions.
