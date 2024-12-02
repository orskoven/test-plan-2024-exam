```mermaid
erDiagram
    Users {
        INT user_id PK "Primary Key"
        VARCHAR username "Unique"
        VARCHAR email "Unique"
        VARCHAR password_hash
        DATETIME created_at
        DATETIME updated_at
        TINYINT is_enabled
        TINYINT is_account_non_locked
    }
    
    AuditLogs {
        INT log_id PK
        INT user_id FK "References Users(user_id)"
        VARCHAR action
        DATETIME performed_at
    }
    
    AuthTokens {
        INT token_id PK
        INT user_id FK "References Users(user_id)"
        VARCHAR token "Unique"
        DATETIME created_at
        DATETIME expires_at
    }
    
    Threat_Categories {
        INT category_id PK
        VARCHAR category_name
        INT parent_category_id FK "Self-referencing"
        VARCHAR taxonomy_path
        TEXT description
        TINYINT is_prioritized
    }
    
    Threat_Events {
        INT event_id PK
        INT source_id
        INT category_id FK "References Threat_Categories(category_id)"
        TEXT description
        DECIMAL confidence_score
        DECIMAL impact_score
        INT embedding_vector_id
        JSON related_events
        ENUM status
        DATETIME reported_at
        DATETIME created_at
    }
    
    Geo_Locations {
        INT geo_id PK
        GEOMETRY location
        CHAR country_code
        VARCHAR region
        VARCHAR city
        INT threat_density
    }
    
    Event_Locations {
        INT event_id FK "References Threat_Events(event_id)"
        INT geo_id FK "References Geo_Locations(geo_id)"
    }
    
    Event_Timeline {
        INT timeline_id PK
        INT event_id FK "References Threat_Events(event_id)"
        ENUM status
        TEXT state_change_reason
        DATETIME timestamp
    }
    
    IoCs {
        INT ioc_id PK
        INT event_id FK "References Threat_Events(event_id)"
        ENUM ioc_type
        VARCHAR ioc_value
        INT linked_ioc_id FK "Self-referencing"
        VARCHAR source
        DATETIME detected_at
    }
    
    NLP_Embeddings {
        INT embedding_id PK
        INT event_id FK "References Threat_Events(event_id)"
        VARBINARY embedding_vector
        DATETIME created_at
        JSON embedding_metadata
    }
    
    Permissions {
        INT permission_id PK
        VARCHAR permission_name "Unique"
    }
    
    Related_Events {
        INT event_id FK "References Threat_Events(event_id)"
        INT related_event_id FK "References Threat_Events(event_id)"
    }
    
    Roles {
        INT role_id PK
        VARCHAR role_name "Unique"
    }
    
    RolePermissions {
        INT role_permission_id PK
        INT role_id FK "References Roles(role_id)"
        INT permission_id FK "References Permissions(permission_id)"
    }
    
    Temporal_Data {
        INT temporal_id PK
        INT event_id FK "References Threat_Events(event_id)"
        DATETIME event_start_time
        DATETIME event_end_time
        ENUM time_bucket
    }
    
    Trusted_Sources {
        INT source_id PK
        VARCHAR name
        TEXT url
        CHAR country_code
        ENUM organization_type
        ENUM status
        FLOAT average_latency
        JSON scraped_metadata
        DATETIME created_at
        DATETIME last_updated_at
        VARCHAR region
    }
    
    UserRoles {
        INT user_role_id PK
        INT user_id FK "References Users(user_id)"
        INT role_id FK "References Roles(role_id)"
    }

    %% Relationships
    Users ||--o{ AuditLogs : has
    Users ||--o{ AuthTokens : has
    Users ||--o{ UserRoles : has
    Roles ||--o{ RolePermissions : has
    Permissions ||--o{ RolePermissions : has
    Threat_Categories ||--o{ Threat_Categories : "Parent Category"
    Threat_Categories ||--o{ Threat_Events : categorizes
    Threat_Events ||--o{ Event_Locations : includes
    Geo_Locations ||--o{ Event_Locations : locates
    Threat_Events ||--o{ IoCs : contains
    Threat_Events ||--o{ NLP_Embeddings : has
    Threat_Events ||--o{ Event_Timeline : tracks
    Threat_Events ||--o{ Related_Events : relates
