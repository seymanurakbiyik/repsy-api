# repsy-api
repsy-api
# Repsy Package Repository API

A minimalistic REST API to deploy and download `.rep` packages and associated `meta.json` files for the fictional Repsy programming language.

## 📦 Features
- Upload `.rep` and `meta.json` to REST endpoint
- Download uploaded packages
- Two storage strategies: file system and MinIO (object storage)
- Configurable via `application.properties` or environment variables
- Dockerized deployment

## 🔧 REST Endpoints

### Deploy a Package
```
POST /{packageName}/{version}
Content-Type: multipart/form-data
Body:
  - package.rep (zip file)
  - meta.json (JSON file with metadata)
```

### Download a File
```
GET /{packageName}/{version}/{fileName}
```

## ⚙️ Configuration
Add the following to `application.properties` or use environment variables:

```properties
# Choose strategy: file-system or object-storage
storage.strategy=file-system

# MinIO settings (used only if object-storage is selected)
minio.endpoint=http://localhost:9000
minio.accessKey=minioadmin
minio.secretKey=minioadmin
minio.bucket=repsy-packages
```

## 🐳 Docker
To build and run:
```bash
./mvnw clean package
docker build -t repsy-api .
docker run -p 8080:8080 repsy-api
```

## 📝 Notes
- `.rep` files are treated as generic `.zip` archives.
- There is no validation of dependency existence from `meta.json`.
- PostgreSQL database integration placeholder is ready for extension.

## 📬 Submit
Please push your code to a public GitHub repository and deploy the Docker container to a Repsy-accessible registry.

