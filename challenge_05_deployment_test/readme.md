Challenge 5 – Deploying an ADK Agent to Agent Platform

Challenge 5 extends the multi-agent workflow developed in Challenge 4 by deploying it to Google Cloud Agent Platform using Vertex AI Agent Engine. The deployed solution demonstrates that an ADK workflow can be packaged, deployed, and invoked as a remotely hosted agent.

Recreated the Challenge 4 workflow in a clean deployment notebook.
Configured Vertex AI with a Cloud Storage staging bucket.
Wrapped the ADK SequentialAgent workflow in AdkApp.
Validated the complete workflow locally before deployment.
Deployed the application using agent_engines.create().
Tested the deployed Agent Engine using async_stream_query().
Verified remote execution of the complete workflow:
Greeter Agent – acknowledges and frames the request.
Search Agent – uses Google Search to research the request.
Critique Agent – evaluates the initial research response.
Refine Agent – produces the final improved response.
Confirmed Google Search grounding works from the remotely deployed Search Agent.
Used gemini-2.5-flash for all LLM agents.

The final remote test successfully returned four events, one from each agent in the workflow, demonstrating end-to-end execution of the deployed multi-agent application.
