%-------------------------------------------------------------------------------
% LaTeX Template for Final Project Report: Databases for Developers
%-------------------------------------------------------------------------------

\documentclass[12pt, a4paper]{report}

%-------------------------------------------------------------------------------
% Packages
%-------------------------------------------------------------------------------
\usepackage[utf8]{inputenc}          % UTF-8 encoding
\usepackage[T1]{fontenc}             % Output encoding
\usepackage{lmodern}                 % Latin Modern fonts
\usepackage{geometry}                % Page layout
\usepackage{graphicx}                % Include images
\usepackage{hyperref}                % Hyperlinks
\usepackage{cleveref}                % Smart cross-referencing
\usepackage{listings}                % Code listings
\usepackage{xcolor}                  % Color definitions
\usepackage{fancyhdr}                % Fancy headers and footers
\usepackage{tocbibind}               % Include TOC in the TOC
\usepackage{appendix}                % Appendices
\usepackage{caption}                 % Customize captions
\usepackage{subcaption}              % Subfigures
\usepackage{amsmath, amssymb}        % Mathematical symbols
\usepackage{enumitem}                % Customize lists
\usepackage{booktabs}                % Professional tables
\usepackage{titlesec}                % Customize section titles
\usepackage{longtable}               % Tables that span multiple pages
\usepackage{pdfpages}                % Include external PDF pages
\usepackage{tikz}                    % For diagrams
\usetikzlibrary{positioning, arrows, shapes.geometric}

%-------------------------------------------------------------------------------
% Page Layout
%-------------------------------------------------------------------------------
\geometry{
    left=1in,
    right=1in,
    top=1in,
    bottom=1in,
    headheight=15pt,
}

%-------------------------------------------------------------------------------
% Headers and Footers
%-------------------------------------------------------------------------------
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{Final Project Report}
\fancyhead[R]{\thepage}
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\footrulewidth}{0pt}

%-------------------------------------------------------------------------------
% Hyperref Setup
%-------------------------------------------------------------------------------
\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    filecolor=magenta,      
    urlcolor=blue,
    pdftitle={Final Project Report},
    pdfpagemode=FullScreen,
}

%-------------------------------------------------------------------------------
% Listings Setup for Code
%-------------------------------------------------------------------------------
\lstdefinestyle{mystyle}{
    backgroundcolor=\color{white},   
    commentstyle=\color{green!50!black},
    keywordstyle=\color{blue},
    numberstyle=\tiny\color{gray},
    stringstyle=\color{orange},
    basicstyle=\ttfamily\footnotesize,
    breakatwhitespace=false,         
    breaklines=true,                 
    captionpos=b,                    
    keepspaces=true,                 
    numbers=left,                    
    numbersep=5pt,                   
    showspaces=false,                
    showstringspaces=false,
    showtabs=false,                  
    tabsize=2
}

\lstset{style=mystyle}

%-------------------------------------------------------------------------------
% Title Formatting
%-------------------------------------------------------------------------------
\titleformat{\chapter}[hang]
  {\normalfont\huge\bfseries}{\thechapter.}{2pc}{}

\titleformat{\section}
  {\normalfont\Large\bfseries}{\thesection}{1pc}{}

\titleformat{\subsection}
  {\normalfont\large\bfseries}{\thesubsection}{1pc}{}

%-------------------------------------------------------------------------------
% Document Information
%-------------------------------------------------------------------------------
\title{%
    \vspace{2in}
    \textbf{Databases for Developers: Final Project Report} \\
    \vspace{0.5in}
    \LARGE Backend Development and Deployment for Cyber Threat Intelligence Using MySQL, MongoDB, Neo4j, and Spring Boot
}
\author{
    \textbf{Simon Dieckmann Ørskov Beckmann} \\
    Group Number: \#10 \\
    Date of Delivery: \today
}
\date{}

%-------------------------------------------------------------------------------
% Begin Document
%-------------------------------------------------------------------------------
\begin{document}

%-------------------------------------------------------------------------------
% Cover Page
%-------------------------------------------------------------------------------
\maketitle
\thispagestyle{empty} % Remove page number from cover

\newpage

%-------------------------------------------------------------------------------
% List of Figures
%-------------------------------------------------------------------------------
\cleardoublepage
\phantomsection
\addcontentsline{toc}{chapter}{List of Figures}
\listoffigures
\thispagestyle{plain}

%-------------------------------------------------------------------------------
% List of Appendices
%-------------------------------------------------------------------------------
\cleardoublepage
\phantomsection
\addcontentsline{toc}{chapter}{List of Appendices}
\listofappendices
\thispagestyle{plain}

%-------------------------------------------------------------------------------
% Table of Contents
%-------------------------------------------------------------------------------
\cleardoublepage
\phantomsection
\tableofcontents
\thispagestyle{plain}

%-------------------------------------------------------------------------------
% Chapter 1: Introduction
%-------------------------------------------------------------------------------
\cleardoublepage
\chapter{Introduction}

\section{Problem Description}
In the ever-evolving landscape of cybersecurity, organizations face increasing threats from sophisticated cyber adversaries. Effective cyber threat intelligence (CTI) systems are crucial for collecting, analyzing, and responding to cyber threats. This project aims to develop the backend of a CTI web application, focusing on three key database technologies: relational (MySQL), document (MongoDB), and graph (Neo4j) databases. The backend will be developed using Spring Boot, with RESTful APIs facilitating CRUD operations for each database. Additionally, data migration services will be implemented using Apache Camel to transfer data from MySQL to MongoDB and Neo4j.

\begin{figure}[htbp]
    \centering
    \includegraphics[width=\textwidth]{phys.png} % Replace with actual path
    \caption{Physical Model of the Cyber Threat Intelligence System}
    \label{fig:cti_system_schema}
\end{figure}

\section{Explanation of Choices}
\subsection{Databases}
\begin{itemize}
    \item \textbf{MySQL (Relational Database)}: Chosen for its robustness in handling structured data, support for ACID transactions, and widespread use in enterprise applications.
    \item \textbf{MongoDB (Document Database)}: Selected for its flexibility in storing unstructured or semi-structured data, such as threat reports and indicators, allowing for rapid development and schema evolution.
    \item \textbf{Neo4j (Graph Database)}: Ideal for modeling and querying complex relationships between entities like threat actors, campaigns, and attack vectors, providing efficient traversal and insights into interconnected data.
\end{itemize}

\subsection{Programming Languages and Tools}
\begin{itemize}
    \item \textbf{Spring Boot (Java)}: Provides a comprehensive framework for building microservices with embedded servers, auto-configuration, and production-ready features.
    \item \textbf{Apache Camel}: Utilized for its powerful integration capabilities, enabling seamless data migration between different databases.
    \item \textbf{Hibernate ORM}: Used for mapping Java objects to relational database tables in MySQL, simplifying database interactions.
    \item \textbf{Spring Data MongoDB and Neo4j}: Facilitates interaction with MongoDB and Neo4j databases through repositories and simplifies CRUD operations.
    \item \textbf{Postman/Swagger UI}: Used to simulate web client interactions and document the RESTful APIs, given that frontend development is out of scope.
\end{itemize}

%-------------------------------------------------------------------------------
% Chapter 2: Relational Database
%-------------------------------------------------------------------------------
\chapter{Relational Database}

\section{Introduction to Relational Databases}
Relational databases store data in tables composed of rows and columns, where each table represents an entity, and relationships are established via foreign keys. They use Structured Query Language (SQL) for defining and manipulating data. MySQL is a widely-used open-source relational database management system known for its reliability, performance, and ease of use.

\section{Database Design}
\subsection{Entity/Relationship Model}
The relational database is designed to manage structured cyber threat intelligence data, including entities such as \texttt{ThreatActors}, \texttt{Vulnerabilities}, \texttt{Incidents}, \texttt{AttackVectors}, and \texttt{Industries}.

\subsubsection{Conceptual Model}
The conceptual model identifies the main entities and relationships in the cyber threat intelligence system.

\begin{figure}[htbp]
    \centering
    \begin{tikzpicture}[
        entity/.style={rectangle, draw=black, fill=blue!20, minimum width=3cm, minimum height=1cm},
        relationship/.style={diamond, draw=black, fill=green!20, aspect=2, minimum width=2cm, minimum height=1cm},
        line/.style={draw=black, -latex'},
        attribute/.style={ellipse, draw=black, fill=yellow!20, minimum width=2cm, minimum height=1cm},
        font=\small
        ]
        
        % Entities
        \node[entity] (ThreatActor) {ThreatActor};
        \node[entity] (AttackVector) [right=3cm of ThreatActor] {AttackVector};
        \node[entity] (IncidentLog) [below=2cm of ThreatActor] {IncidentLog};
        \node[entity] (Vulnerability) [below=2cm of AttackVector] {Vulnerability};
        \node[entity] (Geolocation) [below=2cm of IncidentLog] {Geolocation};
        \node[entity] (Industry) [left=3cm of IncidentLog] {Industry};
        \node[entity] (ThreatCategory) [above=2cm of ThreatActor] {ThreatCategory};
        \node[entity] (AttackVectorCategory) [above=2cm of AttackVector] {AttackVectorCategory};
        \node[entity] (Country) [left=3cm of ThreatActor] {Country};
        \node[entity] (AffectedProduct) [below=2cm of Vulnerability] {AffectedProduct};
        \node[entity] (GlobalThreat) [right=3cm of Vulnerability] {GlobalThreat};
        
        % Relationships
        \draw[line] (ThreatActor) -- node[above] {belongs to} (ThreatCategory);
        \draw[line] (ThreatActor) -- node[above] {from} (Country);
        \draw[line] (ThreatActor) -- node[above] {uses} (AttackVector);
        \draw[line] (AttackVector) -- node[above] {categorized as} (AttackVectorCategory);
        \draw[line] (IncidentLog) -- node[left] {involves} (ThreatActor);
        \draw[line] (IncidentLog) -- node[right] {uses} (AttackVector);
        \draw[line] (IncidentLog) -- node[left] {occurs in} (Geolocation);
        \draw[line] (IncidentLog) -- node[above] {targets} (Industry);
        \draw[line] (IncidentLog) -- node[right] {exploits} (Vulnerability);
        \draw[line] (Vulnerability) -- node[right] {affects} (AffectedProduct);
        \draw[line] (Vulnerability) -- node[above] {associated with} (GlobalThreat);
        
    \end{tikzpicture}
    \caption{Conceptual Entity-Relationship Diagram}
    \label{fig:conceptual_er}
\end{figure}

\subsubsection{Logical Model}
The logical model expands on the conceptual model by detailing the attributes, primary keys, foreign keys, and cardinalities of relationships.

\begin{figure}[htbp]
    \centering
    \begin{tikzpicture}[
        entity/.style={rectangle, draw=black, fill=blue!20, minimum width=4cm, minimum height=1cm},
        relationship/.style={diamond, draw=black, fill=green!20, aspect=2, minimum width=2cm, minimum height=1cm},
        line/.style={draw=black, -latex'},
        pk/.style={underline},
        font=\small,
        node distance=2cm
        ]
        
        % Entities with attributes
        % ThreatActor
        \node[entity] (ThreatActor) {
            \begin{tabular}{l}
            \textbf{ThreatActor} \\
            \underline{actor\_id} \\
            name \\
            type\_id \\
            description \\
            origin\_country \\
            first\_observed \\
            last\_activity \\
            category\_id \\
            \end{tabular}
        };
        
        % ThreatCategory
        \node[entity] (ThreatCategory) [above=of ThreatActor] {
            \begin{tabular}{l}
            \textbf{ThreatCategory} \\
            \underline{category\_id} \\
            category\_name \\
            description \\
            \end{tabular}
        };
        
        % ThreatActorType
        \node[entity] (ThreatActorType) [below=of ThreatActor] {
            \begin{tabular}{l}
            \textbf{ThreatActorType} \\
            \underline{type\_id} \\
            type\_name \\
            description \\
            \end{tabular}
        };
        
        % Country
        \node[entity] (Country) [left=of ThreatActor] {
            \begin{tabular}{l}
            \textbf{Country} \\
            \underline{country\_code} \\
            country\_name \\
            \end{tabular}
        };
        
        % AttackVector
        \node[entity] (AttackVector) [right=of ThreatActor] {
            \begin{tabular}{l}
            \textbf{AttackVector} \\
            \underline{vector\_id} \\
            name \\
            vector\_category\_id \\
            description \\
            severity\_level \\
            \end{tabular}
        };
        
        % AttackVectorCategory
        \node[entity] (AttackVectorCategory) [above=of AttackVector] {
            \begin{tabular}{l}
            \textbf{AttackVectorCategory} \\
            \underline{vector\_category\_id} \\
            category\_name \\
            description \\
            \end{tabular}
        };
        
        % IncidentLog
        \node[entity] (IncidentLog) [below=of AttackVector] {
            \begin{tabular}{l}
            \textbf{IncidentLog} \\
            \underline{incident\_id} \\
            actor\_id \\
            vector\_id \\
            vulnerability\_id \\
            geolocation\_id \\
            incident\_date \\
            target \\
            industry\_id \\
            impact \\
            response \\
            response\_date \\
            \end{tabular}
        };
        
        % Geolocation
        \node[entity] (Geolocation) [below=of IncidentLog] {
            \begin{tabular}{l}
            \textbf{Geolocation} \\
            \underline{geolocation\_id} \\
            ip\_address \\
            country \\
            region \\
            city \\
            latitude \\
            longitude \\
            \end{tabular}
        };
        
        % Vulnerability
        \node[entity] (Vulnerability) [right=of IncidentLog] {
            \begin{tabular}{l}
            \textbf{Vulnerability} \\
            \underline{vulnerability\_id} \\
            cve\_id \\
            description \\
            published\_date \\
            severity\_score \\
            \end{tabular}
        };
        
        % Industry
        \node[entity] (Industry) [left=of IncidentLog] {
            \begin{tabular}{l}
            \textbf{Industry} \\
            \underline{industry\_id} \\
            industry\_name \\
            description \\
            \end{tabular}
        };
        
        % Relationships with cardinalities
        % ThreatActor to ThreatCategory (Many to One)
        \draw[line] (ThreatActor) -- node[right] {belongs to} (ThreatCategory);
        % ThreatActor to Country (Many to One)
        \draw[line] (ThreatActor) -- node[above] {origin} (Country);
        % ThreatActor to ThreatActorType (Many to One)
        \draw[line] (ThreatActor) -- node[right] {has type} (ThreatActorType);
        % ThreatActor to AttackVector (Many to Many via ThreatActorAttackVector)
        \node[relationship] (Uses) [below right=1cm and 1cm of ThreatActor] {uses};
        \draw[line] (ThreatActor) -- (Uses);
        \draw[line] (Uses) -- (AttackVector);
        % AttackVector to AttackVectorCategory (Many to One)
        \draw[line] (AttackVector) -- node[right] {categorized as} (AttackVectorCategory);
        % IncidentLog to ThreatActor (Many to One)
        \draw[line] (IncidentLog) -- node[above] {involves} (ThreatActor);
        % IncidentLog to AttackVector (Many to One)
        \draw[line] (IncidentLog) -- node[above] {uses} (AttackVector);
        % IncidentLog to Geolocation (Many to One)
        \draw[line] (IncidentLog) -- node[right] {occurs at} (Geolocation);
        % IncidentLog to Vulnerability (Many to One)
        \draw[line] (IncidentLog) -- node[above] {exploits} (Vulnerability);
        % IncidentLog to Industry (Many to One)
        \draw[line] (IncidentLog) -- node[above] {targets} (Industry);
        
    \end{tikzpicture}
    \caption{Logical Entity-Relationship Diagram}
    \label{fig:logical_er}
\end{figure}

\subsection{Normalization Process}
Normalization was applied to minimize redundancy and dependency:

\begin{itemize}
    \item \textbf{First Normal Form (1NF)}: Ensured that each table cell contains only atomic values and each record is unique.
    \item \textbf{Second Normal Form (2NF)}: Removed partial dependencies; all non-key attributes are fully functionally dependent on the primary key.
    \item \textbf{Third Normal Form (3NF)}: Eliminated transitive dependencies; non-key attributes are not dependent on other non-key attributes.
\end{itemize}

\section{Physical Data Model}
\subsection{Data Types}
Appropriate data types were selected for optimal storage and performance:

\begin{itemize}
    \item \texttt{INT}, \texttt{BIGINT}: For identifiers and numerical values.
    \item \texttt{VARCHAR}, \texttt{TEXT}: For variable-length character data.
    \item \texttt{DATE}, \texttt{DATETIME}, \texttt{TIMESTAMP}: For date and time values.
    \item \texttt{DECIMAL}: For precise numerical values like severity scores.
\end{itemize}

\subsection{Primary and Foreign Keys}
\begin{itemize}
    \item \textbf{Primary Keys}: Unique identifiers for each table (e.g., \texttt{actor\_id}, \texttt{incident\_id}).
    \item \textbf{Foreign Keys}: Establish relationships between tables, enforcing referential integrity (e.g., \texttt{actor\_id} in \texttt{incident\_logs} referencing \texttt{threat\_actors}).
\end{itemize}

\subsection{Indexes}
Indexes were created to enhance query performance:

\begin{itemize}
    \item Indexes on frequently queried fields like \texttt{cve\_id}, \texttt{name}, and foreign key columns.
    \item Composite indexes for multi-column searches.
\end{itemize}

\subsection{Constraints and Referential Integrity}
Constraints ensure data validity and consistency:

\begin{itemize}
    \item \textbf{NOT NULL}: Critical fields must contain values.
    \item \textbf{UNIQUE}: Prevents duplicate entries (e.g., \texttt{cve\_id} in \texttt{vulnerabilities}).
    \item \textbf{CHECK}: Validates data based on specified conditions.
    \item \textbf{FOREIGN KEY}: Enforces referential integrity between related tables.
\end{itemize}

\section{Stored Objects}
\subsection{Stored Procedures and Functions}
Stored procedures and functions encapsulate reusable SQL code:

\begin{lstlisting}[language=SQL, caption=Procedure to Alert High Severity Threats]
CREATE PROCEDURE alert_high_severity_threats()
BEGIN
    SELECT name, severity_level FROM global_threats WHERE severity_level >= 8;
END;
\end{lstlisting}

\subsection{Views}
Views provide simplified data access and abstraction:

\begin{lstlisting}[language=SQL, caption=View for Most Exploited Vulnerabilities]
CREATE VIEW most_exploited_vulnerabilities AS
SELECT v.cve_id, v.description, COUNT(il.incident_id) AS exploitation_count
FROM incident_logs il
JOIN vulnerabilities v ON il.vulnerability_id = v.vulnerability_id
GROUP BY v.cve_id, v.description
ORDER BY exploitation_count DESC;
\end{lstlisting}

\subsection{Triggers and Events}
Triggers automate actions in response to database events:

\begin{lstlisting}[language=SQL, caption=Trigger for Auditing Vulnerability Changes]
CREATE TRIGGER vulnerabilities_after_update
AFTER UPDATE ON vulnerabilities
FOR EACH ROW
BEGIN
    INSERT INTO vulnerabilities_audit (
        action_type, vulnerability_id, cve_id, description, action_timestamp, performed_by
    ) VALUES (
        'UPDATE', OLD.vulnerability_id, OLD.cve_id, OLD.description, NOW(), 'system'
    );
END;
\end{lstlisting}

\section{Transactions}
Transactions ensure that database operations are executed reliably and maintain data integrity:

\begin{itemize}
    \item Used in critical operations like incident logging and threat updates.
    \item Managed using \texttt{START TRANSACTION}, \texttt{COMMIT}, and \texttt{ROLLBACK}.
    \item Ensures atomicity; either all operations succeed or none do.
\end{itemize}

\section{Auditing}
An auditing mechanism was implemented using triggers to track changes:

\begin{itemize}
    \item Audit tables store historical data with action types, timestamps, and user information.
    \item Triggers on \texttt{INSERT}, \texttt{UPDATE}, and \texttt{DELETE} operations log changes to critical tables like \texttt{threat\_actors} and \texttt{vulnerabilities}.
\end{itemize}

\section{Security}
\subsection{Users and Privileges}
Database security was enforced by creating users with specific privileges:

\begin{itemize}
    \item \textbf{Application User}: Limited privileges necessary for application functionality.
    \item \textbf{Admin User}: Full privileges for database management tasks.
    \item \textbf{Read-Only User}: Can perform \texttt{SELECT} operations on all tables.
    \item \textbf{Restricted User}: Has limited read access, unable to see sensitive data.
\end{itemize}

\subsection{SQL Injection Prevention}
Measures to prevent SQL injection attacks:

\begin{itemize}
    \item Use of prepared statements with parameterized queries in all database interactions.
    \item Input validation and sanitization at the application layer.
    \item Utilization of ORM tools like Hibernate to abstract SQL queries.
\end{itemize}

\section{Description of the CRUD Application for RDBMS}
\subsection{REST APIs}
RESTful APIs were developed to perform CRUD operations:

\begin{itemize}
    \item \texttt{GET /mysql/threat-actors}: Retrieve all threat actors.
    \item \texttt{POST /mysql/incidents}: Create a new incident log.
    \item \texttt{PUT /mysql/vulnerabilities/\{id\}}: Update vulnerability details.
    \item \texttt{DELETE /mysql/attack-vectors/\{id\}}: Delete an attack vector.
\end{itemize}

\subsection{Service Layer}
The service layer contains business logic and interacts with repositories:

\begin{itemize}
    \item Handles transactions and ensures data integrity.
    \item Implements validation and business rules.
\end{itemize}

\subsection{Security – Registration / Login}
Implemented using Spring Security with JWT:

\begin{itemize}
    \item \textbf{Authentication}: Users authenticate via JWT tokens upon successful login.
    \item \textbf{Authorization}: Access to APIs is controlled based on user roles and privileges.
\end{itemize}

\subsection{Transactions}
Managed using Spring's \texttt{@Transactional} annotation to ensure that operations are executed within a transactional context.

%-------------------------------------------------------------------------------
% Chapter 3: Document Database
%-------------------------------------------------------------------------------
\chapter{Document Database}

\section{Introduction to Document Databases}
Document databases store data as documents, typically using JSON-like formats. They allow for flexible schemas and can handle unstructured data effectively. MongoDB is a leading document database that provides high performance, scalability, and availability.

\section{Database Design}
\subsection{Database Design and Features}
The document database was designed to store CTI data that benefits from a flexible schema:

\begin{itemize}
    \item \textbf{Collections}: \texttt{threat\_actors}, \texttt{incidents}, \texttt{vulnerabilities}, \texttt{indicators}.
    \item \textbf{Embedded Documents}: Nested structures for related data (e.g., incidents containing embedded indicators).
    \item \textbf{Indexes}: Created on fields like \texttt{name}, \texttt{cveId}, and \texttt{incidentId} for efficient querying.
    \item \textbf{Constraints}: Implemented using schema validation to enforce data types and required fields.
\end{itemize}

\subsection{Sample Document Structure}
\begin{lstlisting}[language=json, caption=Sample Incident Document]
{
    "_id": ObjectId("..."),
    "incidentId": "INC-000123",
    "title": "Data Breach Incident",
    "description": "Unauthorized access detected...",
    "reportedAt": ISODate("2023-10-01T10:00:00Z"),
    "status": "Open",
    "threatActors": [
        {
            "name": "APT28",
            "originCountry": "RU",
            "firstObserved": ISODate("2012-01-15T00:00:00Z")
        }
    ],
    "indicators": [
        {
            "indicatorId": "IND-000456",
            "type": "IP Address",
            "value": "192.168.1.100"
        }
    ]
}
\end{lstlisting}

\section{Description of the CRUD Application for the Document Database}
\subsection{REST APIs}
Endpoints were established for CRUD operations:

\begin{itemize}
    \item \texttt{GET /mongodb/incidents}: Retrieve all incidents.
    \item \texttt{POST /mongodb/threat-actors}: Add a new threat actor.
    \item \texttt{PUT /mongodb/vulnerabilities/\{id\}}: Update a vulnerability.
    \item \texttt{DELETE /mongodb/indicators/\{id\}}: Delete an indicator.
\end{itemize}

\subsection{Service Layer}
Uses Spring Data MongoDB for database interactions:

\begin{itemize}
    \item Simplifies data access with repository interfaces.
    \item Handles conversion between domain objects and MongoDB documents.
\end{itemize}

\subsection{Security}
Implemented similar to the relational database application:

\begin{itemize}
    \item JWT-based authentication and authorization.
    \item Role-based access control enforced at the service layer.
\end{itemize}

\subsection{Transactions}
MongoDB supports multi-document transactions:

\begin{itemize}
    \item Transactions used when operations affect multiple documents or collections.
    \item Managed using Spring's transaction management and MongoDB sessions.
\end{itemize}

%-------------------------------------------------------------------------------
% Chapter 4: Graph Database
%-------------------------------------------------------------------------------
\chapter{Graph Database}

\section{Introduction to Graph Databases}
Graph databases use nodes and relationships to represent and store data, making them suitable for applications with complex and interconnected data. Neo4j is a prominent graph database that uses the Cypher query language, enabling efficient querying and traversal of graph structures.

\section{Database Design and Features}
\subsection{Database Design}
Entities are modeled as nodes, and relationships represent connections:

\begin{itemize}
    \item \textbf{Nodes}: \texttt{ThreatActor}, \texttt{Campaign}, \texttt{Vulnerability}, \texttt{Indicator}, \texttt{Incident}.
    \item \textbf{Relationships}:
    \begin{itemize}
        \item \texttt{PARTICIPATES\_IN}: Between \texttt{ThreatActor} and \texttt{Campaign}.
        \item \texttt{TARGETS}: Between \texttt{ThreatActor} and \texttt{Incident}.
        \item \texttt{INDICATES}: Between \texttt{Indicator} and \texttt{Incident}.
        \item \texttt{EXPLOITS}: Between \texttt{ThreatActor} and \texttt{Vulnerability}.
    \end{itemize}
\end{itemize}

\subsection{Features}
\begin{itemize}
    \item Efficient traversal and querying of complex relationships.
    \item Indexes on node properties like \texttt{name} and \texttt{incidentId} for faster searches.
    \item Constraints to ensure uniqueness and data integrity (e.g., unique constraint on \texttt{incidentId}).
\end{itemize}

\section{Description of the CRUD Application for the Graph Database}
\subsection{REST APIs}
Endpoints for interacting with the graph database:

\begin{itemize}
    \item \texttt{GET /neo4j/threat-actors}: Retrieve threat actor nodes.
    \item \texttt{POST /neo4j/relationships}: Create relationships between nodes.
    \item \texttt{PUT /neo4j/incidents/\{id\}}: Update an incident node.
    \item \texttt{DELETE /neo4j/campaigns/\{id\}}: Delete a campaign node.
\end{itemize}

\subsection{Service Layer}
Utilizes Spring Data Neo4j for database interactions:

\begin{itemize}
    \item Provides repositories for node and relationship entities.
    \item Manages session and transaction scopes.
\end{itemize}

\subsection{Security}
Consistent with other applications:

\begin{itemize}
    \item JWT-based authentication and authorization.
    \item Access control enforced at the service and repository layers.
\end{itemize}

\subsection{Transactions}
Transactions in Neo4j ensure data integrity:

\begin{itemize}
    \item Spring's transaction management integrates with Neo4j.
    \item Transactions wrap operations that modify the graph.
\end{itemize}

%-------------------------------------------------------------------------------
% Chapter 5: Data Migration with Apache Camel
%-------------------------------------------------------------------------------
\chapter{Data Migration with Apache Camel}

\section{Introduction to Apache Camel}
Apache Camel is an open-source integration framework that provides routing and mediation rules. It simplifies the integration of different systems by providing a standardized approach to data exchange.

\section{Migration Process}
\subsection{MySQL to MongoDB}
Migration involves extracting data from MySQL, transforming it into a suitable JSON format, and inserting it into MongoDB collections.

\subsection{MySQL to Neo4j}
Migration requires mapping relational data to graph structures:

\begin{itemize}
    \item Tables and records are mapped to nodes.
    \item Foreign keys and relationships are mapped to edges.
\end{itemize}

\section{Implementation with Apache Camel}
Data migration routes were defined using Camel DSL:

\begin{lstlisting}[language=Java, caption=Sample Camel Route]
from("jdbc:mysqlDataSource?useHeadersAsParameters=true")
    .routeId("MySQLToMongoRoute")
    .process(new MySQLToMongoProcessor())
    .to("mongodb:myMongoDb?database=cti&collection=threatActors&operation=insert");
\end{lstlisting}

\subsection{Best Practices}
\begin{itemize}
    \item Implemented error handling and retry mechanisms.
    \item Ensured data consistency during migration.
    \item Validated and transformed data appropriately.
\end{itemize}

%-------------------------------------------------------------------------------
% Chapter 6: Testing Strategy
%-------------------------------------------------------------------------------
\chapter{Testing Strategy}

\section{V-Model Overview}
The V-Model is a software development lifecycle model that emphasizes a corresponding testing phase for each development stage. It ensures that testing activities are planned and executed in parallel with development, promoting early detection of defects and alignment with requirements.

\begin{figure}[htbp]
    \centering
    \includegraphics[width=\textwidth]{v_model.png} % Replace with actual path
    \caption{V-Model of Software Development}
    \label{fig:v_model}
\end{figure}

\section{Testing Levels}
\subsection{Unit Testing}
Unit testing focuses on individual components or units of the application, ensuring that each part functions correctly in isolation.

\subsection{Integration Testing}
Integration testing verifies the interactions between different components or systems, such as microservices and databases, ensuring they work together seamlessly.

\subsection{System Testing}
System testing evaluates the complete and integrated application to verify that it meets the specified requirements.

\subsection{Acceptance Testing}
Acceptance testing ensures that the application meets the business requirements and is ready for deployment. It involves validating the system's functionality from an end-user perspective.

\section{Testing Types}
\subsection{Functional Testing}
Functional testing assesses the application's features and functionalities, ensuring they operate according to the requirements. This includes CRUD operations, authentication, and authorization mechanisms.

\subsection{Non-Functional Testing}
Non-functional testing evaluates aspects such as performance, security, and usability. This ensures the application not only functions correctly but also meets quality standards.

\subsubsection{Performance Testing}
Performance testing measures the application's responsiveness, stability, and scalability under varying workloads.

\subsubsection{Security Testing}
Security testing identifies vulnerabilities and ensures that the application protects data and resources from unauthorized access.

\subsubsection{Usability Testing}
Usability testing assesses the application's user interface and user experience, ensuring it is intuitive and user-friendly.

%-------------------------------------------------------------------------------
% Chapter 7: Test Plan
%-------------------------------------------------------------------------------
\chapter{Test Plan}

\section{Scope}
The scope of testing encompasses all backend functionalities, including CRUD operations for MySQL, MongoDB, and Neo4j databases, API endpoints, data migration processes, security mechanisms, and performance under load.

\section{Objectives}
\begin{itemize}
    \item Verify the correctness and reliability of CRUD operations across all database systems.
    \item Ensure seamless data migration between MySQL, MongoDB, and Neo4j.
    \item Validate the security measures against common threats like SQL injection.
    \item Assess the application's performance under normal and stress conditions.
    \item Confirm that the application meets all specified functional and non-functional requirements.
\end{itemize}

\section{Resources}
\begin{itemize}
    \item \textbf{Tools}: Postman, Swagger UI, JUnit, Mockito, Selenium WebDriver, Apache JMeter, Jenkins.
    \item \textbf{Personnel}: Testers, Developers, QA Engineers.
    \item \textbf{Environments}: Development, Testing, Staging, Production.
\end{itemize}

\section{Schedule}
\begin{longtable}{|p{4cm}|p{8cm}|}
    \hline
    \textbf{Phase} & \textbf{Timeline} \\
    \hline
    Test Planning & Weeks 1-2 \\
    \hline
    Test Design & Weeks 3-4 \\
    \hline
    Test Environment Setup & Weeks 3-4 \\
    \hline
    Test Execution & Weeks 5-8 \\
    \hline
    Defect Reporting & Weeks 5-8 \\
    \hline
    Test Closure & Week 9 \\
    \hline
\end{longtable}

\section{Deliverables}
\begin{itemize}
    \item Test Plan Document
    \item Test Cases and Test Scripts
    \item Test Execution Reports
    \item Defect Logs
    \item Test Summary Report
\end{itemize}

%-------------------------------------------------------------------------------
% Chapter 8: Test Design
%-------------------------------------------------------------------------------
\chapter{Test Design}

\section{Black-Box Test Design}
Black-box testing techniques focus on input and output without considering the internal structure. The following techniques were employed:

\subsection{Equivalence Partitioning}
Equivalence partitioning divides input data into valid and invalid partitions, reducing the number of test cases while maintaining coverage.

\begin{itemize}
    \item \textbf{Valid Partitions}: Valid threat actor names, valid incident IDs, proper JSON structures for MongoDB documents.
    \item \textbf{Invalid Partitions}: Missing required fields, invalid data types, excessively long strings.
\end{itemize}

\subsection{Boundary Value Analysis}
Boundary value analysis tests the boundaries between partitions, ensuring that edge cases are handled correctly.

\begin{itemize}
    \item Testing maximum and minimum lengths for \texttt{name} fields.
    \item Verifying date fields with boundary dates (e.g., leap years).
    \item Checking numerical fields like \texttt{severity\_score} at their limits (0.0 and 10.0).
\end{itemize}

\subsection{Decision Tables}
Decision tables were used to model complex business rules and ensure that all possible combinations of inputs are tested.

\begin{itemize}
    \item Example: Authorization rules based on user roles and API endpoints.
\end{itemize}

\subsection{State Transition Testing}
State transition diagrams represent the states of the application and the transitions caused by events.

\begin{itemize}
    \item Example: User authentication states (Logged Out, Logging In, Logged In, Logging Out).
\end{itemize}

\begin{figure}[htbp]
    \centering
    \begin{tikzpicture}[node distance=2cm, auto]
        \node[state] (S0) {Logged Out};
        \node[state] (S1) [right of=S0] {Logging In};
        \node[state] (S2) [right of=S1] {Logged In};
        \node[state] (S3) [below of=S1] {Logging Out};
        
        \path[->] 
            (S0) edge node {Start Login} (S1)
            (S1) edge node {Success} (S2)
            (S1) edge node {Failure} (S0)
            (S2) edge node {Start Logout} (S3)
            (S3) edge node {Logout Complete} (S0);
    \end{tikzpicture}
    \caption{State Transition Diagram for User Authentication}
    \label{fig:state_transition}
\end{figure}

\section{White-Box Test Design}
White-box testing examines the internal structures or workings of an application.

\subsection{Code Coverage Analysis}
Code coverage tools were utilized to measure the extent to which the application's source code is tested.

\begin{itemize}
    \item \textbf{Statement Coverage}: Ensured that every executable statement is executed at least once.
    \item \textbf{Branch Coverage}: Verified that every possible branch (e.g., if-else conditions) is tested.
\end{itemize}

\subsection{Path Testing}
Path testing identifies and tests all possible paths through the code to ensure that all logic is executed correctly.

\begin{itemize}
    \item Identifying critical paths in CRUD operations.
    \item Testing error handling and exception paths.
\end{itemize}

%-------------------------------------------------------------------------------
% Chapter 9: Test Execution
%-------------------------------------------------------------------------------
\chapter{Test Execution}

\section{Execution Plan}
The execution plan outlines how test cases will be run, managed, and tracked throughout the testing lifecycle.

\begin{enumerate}
    \item Execute unit tests for individual components.
    \item Perform integration tests to verify interactions between microservices and databases.
    \item Conduct system tests to validate the complete application against requirements.
    \item Carry out acceptance tests to ensure the system meets business needs.
    \item Perform non-functional tests, including performance and security assessments.
\end{enumerate}

\section{Test Results}
\subsection{Unit Test Results}
\begin{table}[htbp]
    \centering
    \caption{Unit Test Results}
    \begin{tabular}{lcc}
        \toprule
        \textbf{Test Case ID} & \textbf{Status} & \textbf{Comments} \\
        \midrule
        UT-001 & Passed & Validated ThreatActor creation \\
        UT-002 & Passed & Validated Vulnerability update \\
        UT-003 & Failed & NullPointerException on missing fields \\
        \bottomrule
    \end{tabular}
    \label{tab:unit_test_results}
\end{table}

\subsection{Integration Test Results}
\begin{table}[htbp]
    \centering
    \caption{Integration Test Results}
    \begin{tabular}{lcc}
        \toprule
        \textbf{Test Case ID} & \textbf{Status} & \textbf{Comments} \\
        \midrule
        IT-001 & Passed & MySQL to MongoDB data migration \\
        IT-002 & Passed & API endpoint authentication \\
        IT-003 & Passed & Neo4j relationship creation \\
        \bottomrule
    \end{tabular}
    \label{tab:integration_test_results}
\end{table}

\subsection{System Test Results}
\begin{table}[htbp]
    \centering
    \caption{System Test Results}
    \begin{tabular}{lcc}
        \toprule
        \textbf{Test Case ID} & \textbf{Status} & \textbf{Comments} \\
        \midrule
        ST-001 & Passed & Full CRUD operations functionality \\
        ST-002 & Passed & Data consistency across databases \\
        ST-003 & Passed & Security measures against SQL injection \\
        \bottomrule
    \end{tabular}
    \label{tab:system_test_results}
\end{table}

\subsection{Acceptance Test Results}
\begin{table}[htbp]
    \centering
    \caption{Acceptance Test Results}
    \begin{tabular}{lcc}
        \toprule
        \textbf{Test Case ID} & \textbf{Status} & \textbf{Comments} \\
        \midrule
        AT-001 & Passed & Meets business requirement for incident logging \\
        AT-002 & Passed & User authentication flows \\
        AT-003 & Passed & Data migration accuracy \\
        \bottomrule
    \end{tabular}
    \label{tab:acceptance_test_results}
\end{table}

\section{Defect Tracking}
Defects identified during testing are logged in a defect tracking system, categorized by severity and priority. Each defect includes detailed descriptions, steps to reproduce, screenshots, and status updates.

\begin{table}[htbp]
    \centering
    \caption{Defect Log}
    \begin{tabular}{lllp{6cm}}
        \toprule
        \textbf{Defect ID} & \textbf{Severity} & \textbf{Priority} & \textbf{Description} \\
        \midrule
        DEF-001 & High & P1 & NullPointerException when creating ThreatActor without required fields \\
        DEF-002 & Medium & P2 & Slow response time on \texttt{GET /mysql/threat-actors} endpoint \\
        DEF-003 & Low & P3 & UI misalignment in Swagger UI documentation \\
        \bottomrule
    \end{tabular}
    \label{tab:defect_log}
\end{table}

%-------------------------------------------------------------------------------
% Chapter 10: Test Automation
%-------------------------------------------------------------------------------
\chapter{Test Automation}

\section{Unit Tests}
Unit tests were implemented using JUnit and Mockito to validate individual components.

\begin{lstlisting}[language=Java, caption=Sample Unit Test for ThreatActorService]
@RunWith(MockitoJUnitRunner.class)
public class ThreatActorServiceTest {

    @Mock
    private ThreatActorRepository threatActorRepository;

    @InjectMocks
    private ThreatActorService threatActorService;

    @Test
    public void testCreateThreatActor_Success() {
        ThreatActor actor = new ThreatActor("APT28", "RU", "Russian group");
        Mockito.when(threatActorRepository.save(actor)).thenReturn(actor);

        ThreatActor created = threatActorService.createThreatActor(actor);

        assertNotNull(created);
        assertEquals("APT28", created.getName());
        Mockito.verify(threatActorRepository, Mockito.times(1)).save(actor);
    }

    @Test(expected = InvalidDataException.class)
    public void testCreateThreatActor_InvalidData() {
        ThreatActor actor = new ThreatActor("", "RU", "Russian group");
        threatActorService.createThreatActor(actor);
    }
}
\end{lstlisting}

\section{Integration Tests}
Integration tests validate the interactions between different components and databases.

\begin{lstlisting}[language=Java, caption=Sample Integration Test for MySQL to MongoDB Migration]
@RunWith(SpringRunner.class)
@SpringBootTest
public class DataMigrationIntegrationTest {

    @Autowired
    private DataMigrationService dataMigrationService;

    @Autowired
    private ThreatActorRepository threatActorRepository;

    @Autowired
    private ThreatActorMongoRepository threatActorMongoRepository;

    @Test
    public void testMySQLToMongoMigration() {
        List<ThreatActor> mysqlActors = threatActorRepository.findAll();
        dataMigrationService.migrateThreatActorsToMongo();

        List<ThreatActorMongo> mongoActors = threatActorMongoRepository.findAll();
        assertEquals(mysqlActors.size(), mongoActors.size());
    }
}
\end{lstlisting}

\section{Continuous Integration}
A Continuous Integration (CI) pipeline was set up using Jenkins to automate the building, testing, and deployment processes.

\subsection{CI Pipeline Overview}
\begin{enumerate}
    \item **Code Checkout**: Jenkins pulls the latest code from the GitHub repository.
    \item **Build**: Maven compiles the code and packages the application.
    \item **Unit Tests**: Executes unit tests and generates coverage reports.
    \item **Integration Tests**: Runs integration tests to verify component interactions.
    \item **API Testing**: Executes Postman collections to validate API endpoints.
    \item **Deployment**: Deploys the application to a staging environment.
    \item **Reporting**: Generates and archives test reports and coverage metrics.
\end{enumerate}

\subsection{CI Job Scripts}
Sample Jenkins pipeline script (Jenkinsfile):

\begin{lstlisting}[language=Groovy, caption=Sample Jenkins Pipeline Script]
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/cti-backend.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'mvn test'
                junit '**/target/surefire-reports/*.xml'
                cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
            }
        }
        stage('Integration Tests') {
            steps {
                sh 'mvn verify -DskipUnitTests=true'
                junit '**/target/failsafe-reports/*.xml'
            }
        }
        stage('API Testing') {
            steps {
                sh 'newman run tests/api_tests.postman_collection.json -e tests/api_tests.environment.json'
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn deploy'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            archiveArtifacts artifacts: 'reports/**', allowEmptyArchive: true
            publishCoverage adapters: [cobertura('target/site/cobertura/coverage.xml')]
        }
    }
}
\end{lstlisting}

\subsection{CI Pipeline Output}
The CI pipeline generates reports for unit tests, integration tests, and code coverage. These reports are accessible through the Jenkins dashboard, providing insights into test pass rates and coverage metrics.

%-------------------------------------------------------------------------------
% Chapter 11: API Testing
%-------------------------------------------------------------------------------
\chapter{API Testing}

\section{Testing Tools}
Postman and Swagger UI were used for designing and executing API tests.

\section{Test Scripts}
Postman collections were created to automate API testing, covering various endpoints and scenarios.

\subsection{Sample Postman Test Script}
\begin{lstlisting}[language=JSON, caption=Sample Postman Collection JSON]
{
    "info": {
        "name": "CTI API Tests",
        "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
    },
    "item": [
        {
            "name": "Get All Threat Actors",
            "request": {
                "method": "GET",
                "header": [],
                "url": {
                    "raw": "http://localhost:8080/mysql/threat-actors",
                    "protocol": "http",
                    "host": ["localhost"],
                    "port": "8080",
                    "path": ["mysql", "threat-actors"]
                }
            },
            "response": []
        },
        {
            "name": "Create New Incident",
            "request": {
                "method": "POST",
                "header": [
                    {
                        "key": "Content-Type",
                        "value": "application/json"
                    },
                    {
                        "key": "Authorization",
                        "value": "Bearer {{jwt_token}}"
                    }
                ],
                "body": {
                    "mode": "raw",
                    "raw": "{ \"incidentId\": \"INC-000124\", \"title\": \"Phishing Attack\", \"description\": \"Susp
