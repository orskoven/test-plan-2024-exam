
### `cyber_threat_intel2` Schema ER Diagram

```markdown
```mermaid
erDiagram
    affected_products {
        INT product_id PK
        VARCHAR product_name "Unique"
        VARCHAR vendor
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    attack_vector_categories {
        INT vector_category_id PK
        VARCHAR category_name "Unique"
        TINYTEXT description
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    attack_vectors {
        INT vector_id PK
        VARCHAR name "Unique"
        VARCHAR description
        INT vector_category_id FK "References attack_vector_categories(vector_category_id)"
        INT severity_level
        TIMESTAMP created_at
        TIMESTAMP updated_at
        VARCHAR category
    }
    
    audit_log {
        BIGINT log_id PK
        DATETIME event_time
        VARCHAR user_host
        TEXT query_text
    }
    
    countries {
        CHAR country_code PK
        VARCHAR country_name "Unique"
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    geolocation_data {
        BIGINT geolocation_id PK
        VARCHAR city
        VARCHAR country
        VARCHAR ip_address
        DOUBLE latitude
        DOUBLE longitude
        VARCHAR region
    }
    
    geolocations {
        BIGINT geolocation_id PK
        VARCHAR ip_address "Unique"
        CHAR country
        VARCHAR region
        VARCHAR city
        DECIMAL latitude
        DECIMAL longitude
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    global_threats {
        INT threat_id PK
        VARCHAR name "Unique"
        VARCHAR description
        DATE first_detected
        DATE last_updated
        INT severity_level
        DATETIME data_retention_until
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    threat_categories {
        INT category_id PK
        VARCHAR category_name "Unique"
        VARCHAR description
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    threat_actor_types {
        INT type_id PK
        VARCHAR type_name "Unique"
        TINYTEXT description
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    threat_actors {
        INT actor_id PK
        VARCHAR name "Unique"
        INT type_id FK "References threat_actor_types(type_id)"
        VARCHAR description
        CHAR origin_country FK "References countries(country_code)"
        DATE first_observed
        DATE last_activity
        INT category_id FK "References threat_categories(category_id)"
        TIMESTAMP created_at
        TIMESTAMP updated_at
        VARCHAR type
    }
    
    industries {
        INT industry_id PK
        VARCHAR industry_name "Unique"
        TINYTEXT description
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    vulnerabilities {
        INT vulnerability_id PK
        VARCHAR cve_id "Unique"
        TINYTEXT description
        DATE published_date
        DECIMAL severity_score
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    incident_logs {
        BIGINT incident_id PK
        INT actor_id FK "References threat_actors(actor_id)"
        INT vector_id FK "References attack_vectors(vector_id)"
        INT vulnerability_id FK "References vulnerabilities(vulnerability_id)"
        BIGINT geolocation_id FK "References geolocations(geolocation_id)"
        DATETIME incident_date
        VARCHAR target
        INT industry_id FK "References industries(industry_id)"
        VARCHAR impact
        VARCHAR response
        DATETIME response_date
        DATETIME data_retention_until
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    incident_logs_audit {
        BIGINT audit_id PK
        ENUM action_type
        BIGINT incident_id
        INT actor_id
        INT vector_id
        INT vulnerability_id
        BIGINT geolocation_id
        DATETIME incident_date
        VARCHAR target
        INT industry_id
        VARCHAR impact
        VARCHAR response
        DATETIME response_date
        DATETIME data_retention_until
        TIMESTAMP action_timestamp
        VARCHAR performed_by
    }
    
    machine_learning_features {
        BIGINT feature_id PK
        BIGINT incident_id FK "References incident_logs(incident_id)"
        JSON feature_vector
        VARCHAR feature_name
        DOUBLE feature_value
        TIMESTAMP created_at
    }
    
    most_exploited_vulnerabilities_mat {
        VARCHAR cve_id PK
        TINYTEXT description
        BIGINT exploitation_count
    }
    
    password_reset_tokens {
        BIGINT id PK
        VARCHAR token "Unique"
        BIGINT user_id FK "References users(id)"
        DATETIME expiry_date
        TIMESTAMP created_at
    }
    
    privileges {
        BIGINT id PK
        VARCHAR name "Unique"
    }
    
    refresh_tokens {
        BIGINT id PK
        VARCHAR token "Unique"
        DATETIME expiry_date
        BIGINT user_id FK "References users(id)"
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }
    
    roles {
        BIGINT id PK
        VARCHAR name "Unique"
    }
    
    roles_privileges {
        BIGINT role_id FK "References roles(id)"
        BIGINT privilege_id FK "References privileges(id)"
    }
    
    statistical_reports {
        BIGINT report_id PK
        VARCHAR content
        DATE generated_date
        VARCHAR report_type
    }
    
    threat_actor_attack_vector {
        INT threat_actor_id FK "References threat_actors(actor_id)"
        INT attack_vector_id FK "References attack_vectors(vector_id)"
    }
    
    threat_actors_audit {
        BIGINT audit_id PK
        ENUM action_type
        INT actor_id
        VARCHAR name
        INT type_id
        VARCHAR description
        CHAR origin_country
        DATE first_observed
        DATE last_activity
        INT category_id
        TIMESTAMP action_timestamp
        VARCHAR performed_by
    }
    
    threat_predictions {
        BIGINT prediction_id PK
        DATE prediction_date
        INT threat_id FK "References global_threats(threat_id)"
        DOUBLE probability
        VARCHAR predicted_impact
        DATETIME data_retention_until
        TIMESTAMP created_at
    }
    
    time_series_analytics {
        BIGINT time_series_id PK
        DATE analysis_date
        VARCHAR metric
        DOUBLE value
        BIGINT incident_id FK "References incident_logs(incident_id)"
    }
    
    user_roles {
        BIGINT id PK
        BIGINT user_id FK "References users(id)"
        BIGINT role_id
    }
    
    verification_tokens {
        BIGINT id PK
        VARCHAR token "Unique"
        BIGINT user_id FK "References users(id)"
        DATETIME expiry_date
        TIMESTAMP created_at
    }
    
    vulnerability_product_association {
        INT vulnerability_id FK "References vulnerabilities(vulnerability_id)"
        INT product_id FK "References affected_products(product_id)"
    }

    %% Relationships
    attack_vector_categories ||--o{ attack_vectors : has
    attack_vectors ||--o{ threat_actor_attack_vector : uses
    threat_actors ||--o{ threat_actor_attack_vector : employs
    threat_actor_types ||--o{ threat_actors : defines
    countries ||--o{ threat_actors : originates
    threat_categories ||--o{ threat_actors : categorizes
    industries ||--o{ incident_logs : involves
    vulnerabilities ||--o{ incident_logs : exploited_in
    geolocations ||--o{ incident_logs : located_at
    attack_vectors ||--o{ incident_logs : vector
    threat_actors ||--o{ incident_logs : perpetrates
    vulnerabilities ||--o{ vulnerability_product_association : affects
    affected_products ||--o{ vulnerability_product_association : includes
    global_threats ||--o{ threat_predictions : predicts
    incident_logs ||--o{ machine_learning_features : analyzed_by
    users ||--o{ password_reset_tokens : requests
    users ||--o{ refresh_tokens : owns
    users ||--o{ user_roles : assigned_to
    roles ||--o{ roles_privileges : includes
    privileges ||--o{ roles_privileges : grants
    incident_logs ||--o{ incident_logs_audit : audited
    threat_actors ||--o{ threat_actors_audit : audited
    vulnerabilities ||--o{ vulnerabilities_audit : audited
    incident_logs ||--o{ incident_logs_audit : audited
