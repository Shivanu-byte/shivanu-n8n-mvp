# README

## Features (Current MVP)

### Intelligent Request Routing

-   Detects whether a user message contains:
    -   a product URL
    -   a product-related question
    -   or both
-   Routes the request through the appropriate workflow without
    requiring explicit user instructions.

------------------------------------------------------------------------

### Multimodal Product Information Extraction

The product knowledge base is built by combining information from
multiple sources instead of relying solely on webpage text.

#### Text Extraction

-   Extracts structured information from the product page content.
-   Parses product descriptions, benefits, ingredients, dosage, FAQs,
    and other textual information.

#### Image Extraction

-   Identifies product-related Shopify CDN (`cdn.shopify.com`) images
    from the webpage.
-   Uses a multimodal LLM to extract information from:
    -   Supplement/Nutrition Facts panels
    -   Ingredient labels
    -   Usage instructions
    -   Certifications
    -   Packaging information
    -   Product imagery

#### Knowledge Fusion

The outputs from both extraction pipelines are merged into a unified
product context before being stored or used for question answering.

This significantly improves completeness compared to text-only
extraction since important nutritional and regulatory information is
often present only on the product packaging.

------------------------------------------------------------------------

### Deterministic Multi-LLM Pipeline

Instead of delegating the workflow to a single AI Agent, the application
uses multiple specialised LLM calls, each responsible for a well-defined
task.

Examples include:

-   Product text extraction
-   Product image understanding
-   Product knowledge consolidation
-   User question answering
-   Conversation summarisation

#### Why this approach instead of AI Agents?

-   Deterministic execution
-   Higher reliability
-   Lower latency
-   Lower cost
-   Easier debugging
-   Independent optimisation
-   Better observability
-   Production-friendly architecture

------------------------------------------------------------------------

### Session-aware Context Management

Stores:

-   Product information
-   Conversation summary
-   User's previous message
-   Assistant's previous response

Current MVP behaviour:

-   Replaces stored context whenever a new product URL is shared.
-   Long-term memory is intentionally out of scope.

------------------------------------------------------------------------

### Session Identification

Uses a Session ID to determine whether the conversation relates to the
same product or a newly supplied product.

------------------------------------------------------------------------

### Guard-railed Product Assistant

-   Answers only product-related questions.
-   Refuses unrelated requests.
-   Avoids unsupported medical claims.
-   Grounds every response in extracted product data.

## Future Enhancements

### Direct Shopify Integration

-   Faster retrieval
-   Structured product data
-   Product lookup via Name, SKU, Product ID, Barcode or Image

### Product Recommendation & Comparison Engine

-   Compare nutritional profiles
-   Compare ingredients
-   Compare certifications
-   Compare allergens
-   Recommend alternatives
-   Suggest complementary products

### Persistent User Memory

-   Vector database
-   User-specific memory
-   Behaviour analytics
-   Personalised recommendations

### Agent-based Task Orchestration

Introduce specialised agents for: - Product Retrieval - Product
Comparison - Recommendations - Customer Support - Order & Inventory

## Additional Future Enhancements

### Retrieval-Augmented Generation (RAG)

Semantic search across the complete product catalogue.

### Automatic Product Refresh

Automatically re-index products when ingredients, nutrition, pricing,
availability or certifications change.

### Multi-product Context

Support conversations involving multiple products.

### Explainable Recommendations

Explain recommendations using measurable product attributes.

### Personalised Health Profiles

Support dietary preferences, allergies, fitness goals and supplement
preferences.

### Analytics Dashboard

Capture anonymised usage trends and product insights.

### Automated Error Monitoring & Stakeholder Notifications

-   Detect failures across the workflow.
-   Capture workflow, node, session and error details.
-   Automatically notify stakeholders via email.
-   Maintain execution logs.
-   Support retries and future integrations with Teams/Slack.
