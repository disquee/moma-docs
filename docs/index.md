# Collection Data: Ecosystem & Governance

**Version 1.0.2** | **Status: Active**

---

## The Collection Dataset
The Museum of Modern Art (MoMA) maintains a living, open-source repository of its collection data. This dataset encompasses over 140,000 artworks and 15,000 artists, spanning curatorial departments from Photography and Architecture to Media & Performance. The raw data provides comprehensive, historical metadata including accession numbers, medium descriptions, dimensions, and precise curatorial classifications.

## Ecosystem Objectives
Transforming a continuously evolving historical archive into a functional digital product presents significant architectural challenges. This documentation portal serves as the single source of truth for engineering, curatorial, and content design teams, bridging the gap between raw data and end-user application. 

This governance framework is designed to accomplish three primary objectives:

1. **Data Standardization:** Establish strict structural rules for data architects and catalogers to ensure schema interoperability across all internal databases.
2. **Content Consistency:** Provide curators and UX writers with rigorous voice, tone, and accessibility guidelines to maintain an inclusive, global editorial standard.
3. **Programmatic Access:** Equip developers and external partners with the precise technical specifications required to seamlessly integrate the collection database into consumer applications and academic research models.

---

## Documentation Architecture

Navigate the ecosystem via the core pillars below.

### [Metadata Schema](schema/artworks.md)
**For Data Architects & Catalogers** The structural dictionary for artworks and artists, detailing exact data types, controlled vocabularies, and requirement levels.

### [Voice & Tone](strategy/style-guide.md)
**For Curators, UX Writers & Marketers** Overarching voice principles, contextual tone mapping, and rigorous accessibility standards (including alt-text requirements).

### API Reference
**For Developers & External Partners** The technical specifications for programmatically querying the collection database. 

* [API Overview](api/index.md): Dataset context and technical navigation.
* [Authentication & Limits](api/authentication.md): Public access rules and standard throttling.
* [Endpoints](api/endpoints.md): Available GET requests, parameters, and JSON payloads.
* [Error Handling](api/errors.md): Standardized HTTP status codes and resolutions.

---

## Concept Portfolio

*Note: This documentation portal is an independent concept project and is not affiliated with the Museum of Modern Art.*

Developed by **Eric Disque** to demonstrate how scalable, global content ecosystems are architected. Drawing on over 15 years of experience turning product ambiguity into clear, structured information, this project utilizes a modern Docs-as-Code workflow (Markdown, Git, Python, MkDocs) to bridge the gap between complex historical data and user-centric design.

**Author:** [Eric Disque](https://disquedoesit.com)  
**Source Data:** [Collection GitHub Repository](https://github.com/moma/collection)