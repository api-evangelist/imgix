# Imgix GraphQL Schema

## Overview

This conceptual GraphQL schema models the Imgix real-time image processing and CDN API. Imgix provides powerful on-the-fly image transformation and optimization through URL parameters, a management API for sources and assets, and analytics for usage tracking.

Reference: https://docs.imgix.com/apis

## Schema Design

The schema covers the following capability areas:

### Source Management
Imgix sources define where master images are stored. Supported origins include Amazon S3, Google Cloud Storage, Azure Blob Storage, Web Proxy (fetch from any URL), and S3-compatible stores.

Types: `Source`, `SourceDetails`, `SourceType`, `SourceURL`, `SourceURLConfig`, `SourceS3`, `SourceGCS`, `SourceAzure`, `SourceWebProxy`, `SourceGCSEnabled`

### Image Rendering and Transforms
The core Imgix capability — URL-driven image transformation. Parameters map directly to imgix Rendering API parameters.

Types: `Image`, `ImageDetails`, `ImageURL`, `ImageTransform`, `Resize`, `ResizeMode`, `Width`, `Height`, `Crop`, `CropMode`, `CropFocus`, `Fit`, `FitMode`, `DPR`, `Quality`, `Format`, `FormatDetails`, `Compression`, `Progressive`

### Auto Optimization
Imgix automatic optimization modes that choose the best format, compression, and enhancement for each viewer.

Types: `AutoOptimize`, `AutoCompress`, `AutoFormat`, `AutoEnhance`

### Adjustments
Per-image color and tone adjustments.

Types: `Saturation`, `Contrast`, `Brightness`, `Hue`, `Vibrance`, `Highlight`, `Shadow`, `Sharpness`, `Unsharp`, `Blur`, `Gaussian`

### Visual Effects
Overlay effects including gradients, padding, and borders.

Types: `RadialGradient`, `LinearGradient`, `Padding`, `Border`

### Watermarks and Marks
Overlay images or text watermarks on source images.

Types: `Mark`, `Watermark`

### Palette and Color Extraction
Extract dominant colors and palette information from images.

Types: `Palette`, `Colors`

### Face Detection
Locate and crop to detected faces within images.

Types: `FaceIndex`, `FaceRect`

### Security
Signed URL tokens and API key management.

Types: `SecurityKey`, `Token`, `APIKey`

### Rendering and Caching
Rendering mode selection and HTTP cache header control.

Types: `RenderingMode`, `Cache`, `CacheHeaders`

### Analytics and Stats
Usage statistics at the source and asset levels.

Types: `Stats`, `SourceStats`, `AssetStats`

### Webhooks
Event-driven notifications for source and asset lifecycle events.

Type: `Webhook`

## Queries

- `source(id: ID!)` — Fetch a single source by ID
- `sources` — List all sources for the account
- `image(url: String!)` — Inspect a rendered image URL and its metadata
- `palette(url: String!)` — Extract palette/colors from an image
- `faceDetection(url: String!)` — Detect faces in an image
- `stats(sourceId: ID!, range: String)` — Retrieve usage stats for a source
- `assetStats(sourceId: ID!, path: String!)` — Per-asset stats
- `webhooks` — List registered webhooks
- `apiKeys` — List API keys for the account

## Mutations

- `createSource(input: CreateSourceInput!)` — Create a new image source
- `updateSource(id: ID!, input: UpdateSourceInput!)` — Update source configuration
- `deleteSource(id: ID!)` — Remove a source
- `purgeAsset(sourceId: ID!, path: String!)` — Purge a cached asset
- `createWebhook(input: CreateWebhookInput!)` — Register a new webhook
- `deleteWebhook(id: ID!)` — Remove a webhook
- `rotateAPIKey(id: ID!)` — Rotate an API key

## File

- Schema: [imgix-schema.graphql](imgix-schema.graphql)
