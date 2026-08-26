
Architecture Evolution
Note: This repository intentionally retains artifacts from both architectural approaches. The first implementation demonstrates the original direct multi-agent/sequential design and was validated locally. 
The second implementation represents the final AgentTool-based architecture used for successful deployment to Google Cloud Agent Platform. These files are retained to document the design evolution and lessons learned during implementation.

During development of the ReadyNow! agent, two architectural approaches were implemented and evaluated. Both approaches successfully demonstrated the required multi-agent and response-quality concepts; however, deployment constraints encountered with Google Cloud Agent Platform led to a change in the final architecture.

Approach 1 — Direct Multi-Agent / Sequential Workflow

The initial implementation used a more traditional ADK multi-agent structure. The ReadyNow! root agent coordinated specialist sub-agents for weather, search/news, routing, and emergency-preparedness guidance. A separate sequential response-quality workflow was used to validate and refine the response before it was returned to the user.

This architecture worked well during local notebook execution and testing. Specialist routing, tool execution, input validation, response validation/refinement, and interaction logging were all successfully demonstrated.

However, deployment to Vertex AI Agent Engine exposed limitations associated with the agent hierarchy and parent/child relationships. In particular, the existing root agent and its sub-agent relationships could not be cleanly incorporated into the SequentialAgent response workflow while preserving the architecture that worked locally.

Rather than substantially altering a working local implementation simply to accommodate deployment, a second architecture was developed.

Approach 2 — AgentTool-Based Architecture

The final implementation converts the specialist agents and response-quality workflow into tools available to the ReadyNow! root agent.

The root agent remains responsible for understanding the user's request and orchestrating the overall interaction. It can invoke one or more specialist AgentTools as required:

Weather Agent — current weather, forecasts, and weather alerts
Search / News Agent — current emergency information, news, and official notices
Routes Agent — routing, evacuation routes, and directions
Safety / Q&A Agent — emergency-preparedness and public-safety guidance
Response Quality Workflow — sequential validation and refinement of the candidate response

The root agent first invokes the appropriate specialist tool or combination of tools. It then synthesizes the specialist results into a candidate response and passes that response to the Response Quality Workflow.

The Response Quality Workflow remains a true ADK sequential workflow:

Response Validator Agent → Response Refiner Agent

The validated and refined result is then returned through the root agent to the user.

Why the Architecture Changed

The change was driven primarily by deployment compatibility rather than a failure of the original design.

Approach 1 demonstrated the desired behavior locally, but its agent-parent relationships made packaging the complete architecture for Agent Engine deployment problematic. Approach 2 preserved the same functional goals while creating a cleaner deployment boundary.

Using AgentTools allowed the root agent to orchestrate specialist agents and the sequential quality workflow without attempting to place the existing root-agent hierarchy inside another agent hierarchy.

This resulted in an architecture that could be successfully packaged, deployed, and exercised through Google Cloud Agent Platform.

Final Deployed Flow
User Request
     |
     v
Input Validation
     |
     +---- UNSAFE / OFF_MISSION ----> Block
     |
     v
ReadyNow! Root Agent
     |
     +---- Weather AgentTool
     +---- Search / News AgentTool
     +---- Routes AgentTool
     +---- Safety / Q&A AgentTool
     |
     v
Root Synthesizes Candidate Response
     |
     v
Response Quality Workflow AgentTool
     |
     v
Response Validator Agent
     |
     v
Response Refiner Agent
     |
     v
ReadyNow! Root Agent
     |
     v
Final Response
Deployment Validation

The final AgentTool-based architecture was successfully deployed to Google Cloud Agent Platform / Vertex AI Agent Engine and tested through the Agent Platform Playground.

Deployment testing confirmed specialist routing for weather, search/news, routes, and safety requests. Testing also demonstrated multi-specialist orchestration, execution of the sequential response-quality workflow, and blocking of requests classified by input validation as OFF_MISSION or UNSAFE.

The final implementation therefore retains the major capabilities demonstrated by the original local architecture while providing an architecture that is compatible with the deployed Agent Engine environment.

Logging Note

The development implementation also includes interaction logging used during local execution and testing. This provides timestamped records of agent interactions and assists with troubleshooting and validation.

Full application-level interaction logging was not made part of the final deployed architecture during the primary implementation. Extending the same logging capability into the deployed Agent Engine environment I considered a reach goal / future enhancement.
