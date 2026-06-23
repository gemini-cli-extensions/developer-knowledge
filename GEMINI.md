# DeveloperKnowledge MCP Server

This server provides access to documentation about Google developer products. It
can search for relevant documents based on a query and retrieve the full content
of those documents.

## Tools

### search_documents

This is the primary tool to search for documentation. It returns snippets of
relevant documents, along with their names and URLs. If snippets are
insufficient, use `get_documents` to retrieve full content.

**When to use:**

*   Use this tool as the first step when a user asks a question about one of the
    covered Google developer products and you need to find relevant
    documentation.

**When not to use:**

*   Do not use this tool if the user's question is not related to one of the
    covered Google developer products.
*   Do not use this tool if you already have a document name and need its
    content; use `get_documents` instead.

**Example:** If a user asks "How do I create a Cloud Storage bucket?", you
should call: `print(developer_knowledge.search_documents(query="How to create a
Cloud Storage bucket?"))`

### answer_query

Use this tool to let another model search for content and synthesize an answer.
This can save tokens in your own context window. This can be helpful for
summarizing complex results. `answer_query` returns citations for its response.
If needed, you can fetch the full content of the citations using
`get_documents`, just like you can with `search_documents`.

**When to use:**

*   Use this to synthesize complex information without using as many tokens as
    `search_documents`.

**When not to use:**

*   Do not use this tool if the user's question is not related to one of the
    covered Google developer products.
*   Do not use this tool if you already have a document name and need its
    content; use `get_documents` instead.

### get_documents

This tool retrieves the full content of multiple documents (up to 20) in a
single call, based on their names.

**When to use:**

*   After calling `search_documents`, if multiple results seem relevant but
    their snippets are insufficient to answer the user's question, use this tool
    to retrieve the full document content of up to 20 results in a single call,
    using the `parent` returned by `search_documents`.

**When not to use:**

*   Do not use this tool without first calling `search_documents` to obtain
    document names.

**Example:** If `search_documents` returns multiple results, and you need the
full content for two of them with `parent`
`documents/docs.cloud.google.com/storage/docs/creating-buckets` and
`documents/docs.cloud.google.com/storage/docs/introduction`, you should call:
`print(developer_knowledge.get_documents(names=["documents/docs.cloud.google.com/storage/docs/creating-buckets","documents/docs.cloud.google.com/storage/docs/introduction"]))`
