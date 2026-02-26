# @bitovi/n8n-nodes-semantic-text-splitter

This is an n8n community node. It lets you use semantic text splitting in your n8n workflows.

Semantic text splitting is an advanced text processing technique that splits text based on semantic similarity rather than simple character or token counts. This node implements the methodology described in [5 Levels Of Text Splitting](https://github.com/FullStackRetrieval-com/RetrievalTutorials/blob/main/tutorials/LevelsOfTextSplitting/5_Levels_Of_Text_Splitting.ipynb), which uses embedding models to identify natural breakpoints in text where meaning shifts significantly.

[n8n](https://n8n.io/) is a [fair-code licensed](https://docs.n8n.io/reference/license/) workflow automation platform.

[Installation](#installation)  
[Operations](#operations)  
[Compatibility](#compatibility)  
[Usage](#usage)  
[Resources](#resources)  
[Version history](#version-history)

## Installation

Follow the [installation guide](https://docs.n8n.io/integrations/community-nodes/installation/) in the n8n community nodes documentation.

**Quick Installation:**

- Make sure to allow community nodes with `N8N_COMMUNITY_PACKAGES_ENABLED=true`
- Once logged in to your N8N web UI, go to `/settings/community-nodes` and type `@bitovi/n8n-nodes-semantic-text-splitter`

## Operations

The Semantic Text Splitter node provides intelligent text splitting capabilities:

- **Semantic Text Splitting**: Splits text into semantically coherent chunks using embedding-based similarity analysis
- **Configurable Parameters**: Control splitting behavior with customizable thresholds and window sizes
- **Integration with Embedding Models**: Works with any n8n-compatible embedding model for similarity calculations

## Compatibility

- **Minimum n8n version**: Compatible with n8n v1.0+
- **Node.js version**: Requires Node.js 18.10 or higher
- **Dependencies**: Requires @langchain/core and @langchain/textsplitters

This node is tested with the latest stable version of n8n and should work with most n8n installations that support community nodes.

## Usage

### Node Configuration

The Semantic Text Splitter node requires an embedding model connection and supports the following parameters:

- **Percentile Threshold for Breakpoints** (default: 0.95): Controls how selective the algorithm is when identifying breakpoints. Higher values result in fewer, larger chunks.
- **Number of Sentences to Consider in Sliding Window** (default: 3): The size of the sliding window used for embedding comparison.
- **Minimum Chunk Size** (default: 100): Minimum character length for generated chunks.
- **Sentence Delimiters** (default: `.,!,?`): Comma-separated list of delimiters used to identify sentence boundaries (for example `.,!,?,\\n`).

### How It Works

1. **Sentence Splitting**: Text is first split into sentences using the configured delimiters
2. **Sliding Windows**: Creates overlapping windows of sentences based on the window size
3. **Embedding Generation**: Each window is converted to embeddings using the connected embedding model
4. **Distance Calculation**: Calculates cosine distances between sequential window embeddings
5. **Breakpoint Detection**: Identifies breakpoints where semantic distance exceeds the threshold
6. **Chunk Creation**: Creates final text chunks based on identified breakpoints

### Example Workflow

1. Connect a text input (e.g., from a document loader)
2. Connect an embedding model (e.g., OpenAI Embeddings)
3. Configure the splitting parameters based on your needs
4. Connect the output to downstream processing nodes (e.g., vector store, document processing)

This approach creates more coherent chunks compared to simple character or token-based splitting, making it ideal for RAG (Retrieval Augmented Generation) applications and document processing workflows.

## Resources

- [n8n community nodes documentation](https://docs.n8n.io/integrations/community-nodes/)
- [5 Levels Of Text Splitting Tutorial](https://github.com/FullStackRetrieval-com/RetrievalTutorials/blob/main/tutorials/LevelsOfTextSplitting/5_Levels_Of_Text_Splitting.ipynb)
- [LangChain Text Splitters Documentation](https://js.langchain.com/docs/modules/data_connection/document_transformers/)

## Version history

- **v0.1.2** (Current): Latest stable release with full semantic splitting functionality
- **v0.1.x**: Initial releases with core semantic text splitting features

## Need help or have questions?

Need guidance on leveraging AI agents or N8N for your business? Our [AI Agents workshop](https://hubs.ly/Q02X-9Qq0) will equip you with the knowledge and tools necessary to implement successful and valuable agentic workflows.

## License

[MIT](./LICENSE.md)
