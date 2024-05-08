# Backend Application

This is the main application file for the backend of our project.

## File Access Control

The application has a feature to control access to files based on the `AZURE_ENFORCE_ACCESS_CONTROL` environment variable.

- If `AZURE_ENFORCE_ACCESS_CONTROL` is not set or set to `false`, logged in users can access all files regardless of access control.
- If `AZURE_ENFORCE_ACCESS_CONTROL` is set to `true`, logged in users can only access files they have access to.

Please note that enabling access control can make the application slower and more memory-hungry.

## File Opening

The application opens a file by removing the page number from the path (if present) and then attempts to download the blob from the Azure Blob Storage.

If the blob is not found in the general Blob container, and user uploads are enabled, the application tries to download the file from the user's directory in the Azure Data Lake Storage.

If the blob or file is still not found, the application returns a 404 error.

## File Sending

Once the blob is successfully downloaded, the application reads it into a `BytesIO` object and sends it as a file response with the appropriate MIME type. If the MIME type of the blob is `application/octet-stream`, the application tries to guess the MIME type based on the file extension.

Please note that the application does not send the file as an attachment.

# Dependencies

The project has the following dependencies:

- `aiofiles==23.2.1`: Asynchronous file read/write support using asyncio, used by Quart.
- `aiohttp==3.9.3`: Asynchronous HTTP client/server framework for asyncio and Python, a direct requirement and used by Microsoft Kiota Authentication Azure.
- `aiosignal==1.3.1`: A helper for asyncio-friendly signalling, used by aiohttp.
- `annotated-types==0.6.0`: A library for annotated types, used by Pydantic.
- `anyio==4.3.0`: AnyIO is a compatibility layer for asynchronous networking and I/O in Python, used by HTTPX and OpenAI.
- `asgiref==3.7.2`: ASGI reference implementation, used by OpenTelemetry Instrumentation ASGI.
- `attrs==23.2.0`: Classes Without Boilerplate, used by aiohttp.
- `azure-ai-documentintelligence==1.0.0b2`: Client library for Azure AI Document Intelligence, a direct requirement.
- `azure-common==1.1.28`: Microsoft Azure common code, used by Azure Search Documents.
- `azure-core==1.30.1`: Microsoft Azure Core Library for Python, used by multiple Azure services including Azure AI Document Intelligence, Azure Core Tracing OpenTelemetry, Azure Identity, Azure KeyVault Secrets, Azure Monitor OpenTelemetry, Azure Monitor OpenTelemetry Exporter, Azure Search Documents, Azure Storage Blob, and Azure Storage File DataLake.

