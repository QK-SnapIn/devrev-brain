---
title: MS Fabric AirSync
devrev_id: ART-22480
parent_directory: AirSync
translation_group: GYJm4pCY
modified_date: "2026-02-12T04:50:03.764Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/GYJm4pCY"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# MS Fabric AirSync

# Microsoft Fabric

The Microsoft Fabric AirSync connector enables you to import structured table data from Microsoft Fabric Lakehouses into DevRev as custom objects. This integration allows you to leverage your Fabric data for agentic work, analytics, and insights within DevRev.

### Supported objects

The Microsoft Fabric connector imports structured table data from your lakehouse as custom objects in DevRev. All tables from the selected lakehouse are imported, with each table becoming a custom object type in DevRev.

### Importing from Microsoft Fabric

1. Log in to DevRev.
2. Navigate to **[Settings > Integrations > Snap-ins](https://app.devrev.ai/?setting=snap-ins)**, search for **Microsoft Fabric** under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)** in the left-navigation.
5. Click **Airsync** in the top right corner and select **Microsoft Fabric**.
6. Create a new connection to authenticate with your Microsoft Fabric workspace, or use an existing active connection if you already have one.
7. Once the connection is established, select the lakehouse you want to import and specify the DevRev part to be used for any imported work. This initiates a bulk import of the selected sync.
8. DevRev makes an effort to automatically map the structured table data from your lakehouse to custom objects in DevRev. However, you may be prompted to manually map certain fields if needed.

### Create Microsoft Fabric Connection

To create a Microsoft Fabric connection, you must first generate the required credentials from Azure and then use them while creating the connection in DevRev.

### Step 1: Create a Service Principal

1. Create a service principal in Azure Active Directory (Azure AD) for authentication.
2. Note down the following credentials:- **Client ID** (Application ID)
   - **Client Secret**
   - **Tenant ID**

> These will be required while creating the Microsoft Fabric connection in DevRev.

### Step 2: Grant Required Permissions

Grant the following permissions to your service principal:

1. **Workspace Read Access**: Provide read access to the Microsoft Fabric workspace containing the lakehouse you want to import.
2. **Lakehouse Access**: Share the specific lakehouse with the service principal and grant:- **Read access via SQL**
   - **Read access via Spark**

These permissions ensure the connector can access and read data from your Fabric lakehouse.

### Step 3: Create Microsoft Fabric Connection in DevRev

1. In **DevRev**, navigate to **Airsync**.
2. Select **Microsoft Fabric**.
3. Click **Add Connection**.
4. Enter the following details:- **Connection Name**
   - **Client ID**
   - **Client Secret**
   - **Tenant ID**
   - **Subdomain**: Enter `fabric` as the subdomain value
5. Click **Next**.
6. On the next screen, select the lakehouse you want to import data from.
7. Specify the DevRev part where the imported content should reside. Click **Start**.
8. This will trigger an import of the selected lakehouse.

> Import duration varies from minutes to hours based on data size.

## Data import limits

The connector enforces the following limits to ensure optimal performance and system stability:

- **30,000 rows per table**: Each table can import a maximum of 30,000 rows
- **20 tables maximum**: You can import up to 20 tables per lakehouse
- **50 MB parquet size limit**: Individual parquet files must not exceed 50 MB in size

If your data exceeds these limits, consider filtering or partitioning your data before import, or use the Workload Data Job approach to prepare a subset of your data for import.

## Best practices for data relationships

To ensure proper primary key and foreign key relationships in your imported data, we recommend maintaining a metadata table within your lakehouse. This metadata table allows the connector to understand relationships between your tables and generate proper reference fields in DevRev.

### Metadata table structure

Create a table named `devrev_pk_fk_metadata` in your lakehouse with the following structure:

**Table Name**: `devrev_pk_fk_metadata`

**Table Path**: The metadata table must be created at `Tables/dbo/devrev_pk_fk_metadata` in your lakehouse (e.g., `{lakehouseId}/Tables/dbo/devrev_pk_fk_metadata`).

**Required fields**:

- `table_name` (STRING, NOT NULL): Name of the table (e.g., "departments", "employees", "purchase_order_lines")
- `constraint_type` (STRING, NOT NULL): Must be "PRIMARY_KEY" or "FOREIGN_KEY"
- `field_names` (STRING, NOT NULL): Field names separated by commas- Single field: `"employee_id"`
  - Composite key: `"po_id,line_number,part_id"` (comma-separated, spaces optional)

**Optional fields** (required for FOREIGN_KEY only):

- `referenced_table` (STRING): Name of the referenced table (only for FOREIGN_KEY, NULL for PRIMARY_KEY)
- `referenced_fields` (STRING): Referenced field names separated by commas (only for FOREIGN_KEY, must match the order and count of field_names)

### Example Data

**Primary Keys**:

| table_name | constraint_type | field_names | referenced_table | referenced_fields |
| --- | --- | --- | --- | --- |
| departments | PRIMARY_KEY | department_id | NULL | NULL |
| employees | PRIMARY_KEY | employee_id | NULL | NULL |

**Foreign Keys**:

| table_name | constraint_type | field_names | referenced_table | referenced_fields |
| --- | --- | --- | --- | --- |
| employees | FOREIGN_KEY | department_id | departments | department_id |
| purchase_order_lines | FOREIGN_KEY | po_id | purchase_orders | po_id |
| purchase_order_lines | FOREIGN_KEY | part_id | parts | part_id |

### Important Rules

1. **Primary key fields**: Must be of type `int` or `text` in DevRev. If a field is not `int` or `text`, the primary key constraint will be ignored.
2. **Foreign key fields**: Must be of type `int` or `text` in DevRev. If a field is not `int` or `text`, the foreign key constraint will be ignored.
3. **Single-field primary keys**: A field that is the entire primary key (single-field PK) cannot also be a foreign key.
4. **Composite primary keys**: Fields that are part of a composite primary key CAN also be foreign keys.
5. **Field count match**: For foreign keys, `field_names` and `referenced_fields` must have the same number of fields (comma-separated).
6. **One row per constraint**: Each PRIMARY_KEY or FOREIGN_KEY relationship should be a separate row.

### Benefits of maintaining a metadata table

- **Enhanced data visualization**: Proper relationships enable better data visualization and understanding of connections between tables
- **Improved agent understanding**: DevRev's AI agents can better understand and navigate interconnected data when relationships are properly defined
- **Better insights**: Well-structured relationships lead to more accurate analytics and insights
- **Proper ID generation**: Primary keys are used for generating external IDs, ensuring data consistency
- **Reference field mapping**: Foreign keys create reference fields in DevRev, enabling proper data linking

 This metadata table is not imported to DevRev. It is only used internally by the connector during metadata extraction. If this table doesn't exist or is empty, the connector will use default configurations.

## Use case

After importing your Microsoft Fabric data into DevRev, you can:

- **Enable agentic work**: Use DevRev's AI agents to query, analyze, and work with your Fabric data directly within DevRev
- **Unified analytics**: Combine your Fabric business intelligence data with DevRev's customer and product data for comprehensive insights
- **Cross-platform workflows**: Leverage your Fabric data in DevRev's customer support, product development, and business workflows
- **Data-driven decisions**: Make informed decisions by having all your data accessible in one unified platform

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [MS Fabric AirSync](https://support.devrev.ai/en-US/devrev/article/GYJm4pCY) (ART-22480)
