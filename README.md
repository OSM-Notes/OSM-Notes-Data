# OSM-Notes-Data

JSON data files for OSM Notes Viewer and AI-assisted note resolution.

This repository contains pre-calculated analytics data exported from the OSM Notes Analytics data warehouse, optimized for consumption by web viewers and AI systems.

## 📁 Repository Structure

### Data Files

#### User Data (`data/users/`)

Individual JSON files for each OpenStreetMap user, organized in a hexadecimal subdirectory structure for optimal filesystem performance:

- **Structure**: `data/users/{hex1}/{hex2}/{hex3}/{user_id}.json`
- **Example**: `data/users/0/3/2/421938.json`
- **Format**: Hexadecimal hash-based 3-level directory structure (modulo 4096)
- **Purpose**: Provides detailed statistics per user including:
  - Notes created, resolved, and commented
  - Application usage (mobile vs desktop)
  - Resolution metrics and response times
  - Historical data by year/month
  - Contributor type information

**Why subdirectories?** With hundreds of thousands of user files, organizing them in subdirectories improves:
- Filesystem performance (faster directory listings)
- GitHub UI navigation (no truncation)
- Scalability for future growth (millions of users)

#### Country Data (`data/countries/`)

Individual JSON files for each country:

- **Structure**: `data/countries/{country_id}.json`
- **Purpose**: Country-level statistics including:
  - Notes by country
  - Resolution rates and metrics
  - Application usage patterns
  - Temporal resolution data

#### Index Files (`data/indexes/`)

Quick lookup files for efficient data discovery:

- **`users.json`**: Array of all users with basic statistics (sorted by activity)
- **`countries.json`**: Array of all countries with basic statistics
- **Purpose**: Enables fast user/country discovery without loading individual files

#### Metadata (`data/metadata.json`)

Export metadata including:
- Export timestamp
- Total counts (users, countries, notes)
- Data version information

#### GeoJSON Files

- **`countries.geojson.gz`**: Compressed GeoJSON with country boundaries
- **`maritimes.geojson.gz`**: Compressed GeoJSON with maritime boundaries
- **Purpose**: Geographic data for map visualization

#### CSV Files (`csv/notes-by-country/`)

**Purpose**: Provide context to AI systems for note resolution assistance.

These CSV files contain notes organized by country, formatted to help AI models understand:
- Note content and context
- Geographic distribution
- Resolution patterns
- Historical data for training/context

**Use Case**: When an AI system needs to assist in resolving OpenStreetMap notes, these files provide the necessary context about:
- What types of notes exist in each country
- Common resolution patterns
- Geographic and cultural context
- Historical resolution data

Files are named by country ID: `{country_id}_{country_name}.csv`

#### Other Files

- **`noteLocation.csv.zip`**: Compressed CSV with note locations (lat/lon coordinates)
- **`schemas/`**: JSON Schema files for data validation (synced from OSM-Notes-Common)
  - Available via GitHub Pages at: `https://osm-notes.github.io/OSM-Notes-Data/schemas/`

## 🌐 Access via GitHub Pages

This repository is configured for GitHub Pages. Data files and schemas are accessible via:

**Data files:**
```
https://osm-notes.github.io/OSM-Notes-Data/data/{path}
```

**JSON Schemas:**
```
https://osm-notes.github.io/OSM-Notes-Data/schemas/{schema-name}.schema.json
```

See `index.html` for a complete list of available endpoints.

## 📊 Data Source

All data is exported from the OSM Notes Analytics data warehouse (`notes_dwh` database) using automated ETL processes. The export scripts are located in the [OSM-Notes-Analytics](https://github.com/OSM-Notes/OSM-Notes-Analytics) repository.

## 🔄 Update Process

Data is automatically updated via scheduled exports that:
1. Extract modified data from the data warehouse
2. Export to JSON files
3. Validate against JSON schemas
4. Commit and push to this repository
5. Deploy via GitHub Pages

## 📝 File Formats

- **JSON**: All user, country, and index data
- **GeoJSON**: Geographic boundaries (compressed with gzip)
- **CSV**: Note data for AI context (organized by country)
- **Schemas**: JSON Schema for validation

## 🔗 Related Projects

- **[OSM-Notes-Analytics](https://github.com/OSM-Notes/OSM-Notes-Analytics)**: Data warehouse and ETL processes
- **[OSM-Notes-Viewer](https://github.com/OSM-Notes/OSM-Notes-Viewer)**: Web viewer that consumes this data
- **[OSM-Notes-Common](https://github.com/OSM-Notes/OSM-Notes-Common)**: Shared schemas and common utilities

## 📄 License

See [LICENSE](LICENSE) file for details.
