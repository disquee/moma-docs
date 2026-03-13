# Artworks Metadata Dictionary
**Version:** 1.0.0  
**Status:** Published  
**Owner:** Content Strategy & Engineering

This dictionary defines the standard metadata schema for the MoMA collection dataset. Adherence to these standards ensures data interoperability across the museum’s digital ecosystem, from the public API to internal curatorial tools.

---

## 1. Core Identification Fields
These fields are required for every object ingested into the collection database.

| Field Name | Data Type | Requirement | Description | Example |
| :--- | :--- | :--- | :--- | :--- |
| `Title` | String | **Required** | The official title of the artwork. Use *Untitled* if no name is provided. | *The Starry Night* |
| `Artist` | String (Link) | **Required** | The primary creator. Must match an entry in the `Artists` dictionary. | Vincent van Gogh |
| `ObjectID` | Integer | **Required** | A unique, non-changing identifier assigned at ingestion. | `4362` |
| `AccessionNo` | String | **Required** | The legal identifier assigned when the work is acquired. | `472.1941` |

---

## 2. Classification & Categorization
Fields used for filtering, faceted search, and information architecture.

### **Department (`Department`)**
* **Definition:** The curatorial department responsible for the work.
* **Allowed Values (Controlled Vocabulary):** * `Architecture & Design`
    * `Drawings & Prints`
    * `Film`
    * `Media and Performance`
    * `Painting & Sculpture`
    * `Photography`
* **Usage Rule:** Only one department may be assigned per artwork.

---

## 3. Physical Attributes
Technical specifications for archival and display purposes.

| Field Name | Format | Logic |
| :--- | :--- | :--- |
| `Medium` | String | A concise description of materials used. (e.g., *Oil on canvas*) |
| `Dimensions` | String | Physical size. Format as: `Height x Width x Depth (Units)`. |
| `Date` | YYYY or Range | The year of completion. Use `c.` for circa or `-` for ranges (e.g., `1912-1914`). |

---

## 4. Content Governance & Style
To maintain a global content ecosystem, follow these formatting rules:

* **Artist Names:** Always use *First Name Last Name* format. Do not use all caps.
* **Dates:** If the exact date is unknown, use the decade (e.g., `1920s`) rather than "Unknown."
* **Credit Line:** Must include the source of funds or donor name as legally required by the acquisition contract.

> **Note for Developers:** > When querying this data via the MoMA API, ensure your headers include `Accept-Encoding: gzip` to handle the large payload sizes of the full collection export.