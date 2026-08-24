Challenge 4 – Agent Workflow

This challenge demonstrates a multi-agent workflow using Google ADK SequentialAgent. The workflow processes a travel-planning request through four specialized agents in sequence:

Greeter Agent – acknowledges and frames the user's request.
Search Agent – uses the ADK built-in Google Search tool to generate an initial researched answer.
Critique Agent – reviews the initial response and identifies specific opportunities for improvement.
Refine Agent – rewrites the response using the critique and produces the final polished answer.

Intermediate agent outputs are stored in session state using output_key, allowing later agents to consume results from earlier workflow stages. The notebook includes both an intermediate Search → Critique test and a complete Greeter → Search → Critique → Refine workflow test that prints agent events to demonstrate execution order.

You could also add one short technical note:

SequentialAgent currently produces a deprecation warning in ADK 2.4.0 in favor of the newer Workflow API. It is used here because the challenge specifically requires a Sequential or Loop agent and the implementation remains functional.
