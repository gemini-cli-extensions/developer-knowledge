# DeveloperKnowledge MCP Server

This server provides access to documentation about Google developer products. It
can search for relevant documents based on a query and retrieve the full content
of those documents.

## Tools

### search_documents

This is the primary tool to search for documentation. It returns snippets of
relevant documents, along with their names and URLs. If snippets are
insufficient, use `get_document` or `batch_get_documents` to retrieve full
content.

**When to use:**

*   Use this tool as the first step when a user asks a question about one of the
    covered Google developer products and you need to find relevant
    documentation.

**When not to use:**

*   Do not use this tool if the user's question is not related to one of the
    covered Google developer products.
*   Do not use this tool if you already have a document name and need its
    content; use `get_document` or `batch_get_documents` instead.

**Example:** If a user asks "How do I create a Cloud Storage bucket?", you
should call: `print(developer_knowledge.search_documents(query="How to create a
Cloud Storage bucket?"))`

### get_document

This tool retrieves the full content of a single document based on its name.

**When to use:**

*   After calling `search_documents`, if a result seems relevant but the snippet
    is insufficient to answer the user's question, use this tool to retrieve the
    full document content of that single result using the `parent` returned by
    `search_documents`.

**When not to use:**

*   Do not use this tool without first calling `search_documents` to obtain a
    document name.
*   Do not use this tool if you need to fetch more than one document; use
    `batch_get_documents` instead for efficiency.

**Example:** If `search_documents` returns a result with
`parent='documents/docs.cloud.google.com/storage/docs/creating-buckets'`, and you
need the full content, you should call:
`print(developer_knowledge.get_document(name="documents/docs.cloud.google.com/storage/docs/creating-buckets"))`

### batch_get_documents

This tool retrieves the full content of multiple documents (up to 20) in a
single call, based on their names.

**When to use:**

*   After calling `search_documents`, if multiple results seem relevant but
    their snippets are insufficient to answer the user's question, use this tool
    to retrieve the full document content of up to 20 results in a single call,
    using the `parent` returned by `search_documents`. This is more efficient
    than calling `get_document` multiple times.

**When not to use:**

*   Do not use this tool without first calling `search_documents` to obtain
    document names.
*   Do not use this tool if you only need to fetch a single document; use
    `get_document` instead.

**Example:** If `search_documents` returns multiple results, and you need the
full content for two of them with `parent`
`documents/docs.cloud.google.com/storage/docs/creating-buckets` and
`documents/docs.cloud.google.com/storage/docs/introduction`, you should call:
`print(developer_knowledge.batch_get_documents(names=["documents/docs.cloud.google.com/storage/docs/creating-buckets","documents/docs.cloud.google.com/storage/docs/introduction"]))`
