---
title: Mermaid Beispiele und AI Prompts
description: description
authors: niclasedge
images:
- default.png
tags:
- azure
- networking
toc_max_heading_level: 5
created: 27.06.2024
---





## Mermaid Examples
```mermaid
graph LR
    subgraph one
    A[Hard edge] -->|Link text| B[Round edge]
    end
    
    subgraph two
    C{Decision}
    end
    
    subgraph tree
    D[Result one]
    E[Result two]
    end
    
    B --> C
    C -->|One| D
    C -->|Two| E
```

### Group Services together
```mermaid
flowchart LR
subgraph "One"
  a("`The **cat**
  in the hat`") -- "edge label" --> b{{"`The **dog** in the hog`"}}
end

subgraph "Two"
  c("`The **cat**
  in the hat`") -- "`Bold **edge label**`" --> d("The dog in the hog")
end
```

# icons 
```mermaid
flowchart TD
B["fa:fa-twitter for peace"]
B-->C[fa:fa-ban forbidden]
B-->D(fa:fa-spinner)
B-->E(A fa:fa-camera-retro perhaps?)
```

```powershell
Write-Host "test"
```

```mermaid
 gantt
	title Implementierung von Exchange Online
	dateFormat  YYYY-MM-DD
	section Planung
	Bedarfsanalyse           :a1, 2024-07-12, 30d
	Lizenzauswahl            :a2, after a1, 15d
	section Einrichtung
	Konfiguration            :b1, after a2, 45d
	Datenmigration           :b2, after b1, 60d
	section Schulung
	Administratorenschulung  :c1, after b1, 30d
	Benutzerschulung         :c2, after b2, 30d
	section Abschluss
	Go-Live                  :milestone, after c2, 0d
```
### Mermaid Example with all concepts
```mermaid
flowchart TB
    subgraph Diagram_Elements
        direction LR
        Node1[Regular Node]
        Node2(Rounded Node)
        Node3([Stadium Node])
        Node4[[Subroutine]]
        Node5[(Database)]
        Node6>Asymmetric]
        Node7{Decision}
        Node8{{Hexagon}}
    end

    subgraph Connections
        direction LR
        C1---C2
        C3-->C4
        C5===C6
        C7-.-C8
        C9-.->C10
        C11===>C12
    end

    subgraph Subgraphs
        direction TB
        subgraph SG1
            direction LR
            S1-->S2
        end
        subgraph SG2
            direction BT
            S3-->S4
        end
    end

    Icons[fa:fa-cogs Icons]

    Diagram_Elements --> Connections
    Connections --> Subgraphs
    Subgraphs --> Icons

    class Diagram_Elements,Connections,Subgraphs,Icons highlight
```

#### State Diagram
- Gute geeignet für technische Zeichnungen
```mermaid
stateDiagram
    [*] --> InInventory: In Inventory
    InInventory --> InUse: Issued to User
    InInventory --> InMaintenance: Maintenance Required
    InMaintenance --> InInventory: Maintenance Completed
    InInventory --> Retired: End of Life
    InUse --> InMaintenance: Malfunction
    InUse --> InInventory: Returned

    state InInventory {
        [*] --> Available: Available
        Available --> Issued: Issued
        Issued --> Available: Returned
    }

    state InUse {
        [*] --> Operational: Operational
        Operational --> Malfunction: Malfunction
    }

```

### Promtpt for technical drawings:
- Empfehlung Claude AI
- geht auch mit gpt-4o

Schritt 1: 
Fasse diesen Artikel in Strichpunkten zusammen

Schritt 2: Generieren Sie strukturierte JSON-Daten für ein interaktives Diagramm basierend auf meiner Dokumentation. Erfassen Sie folgende Elemente:

1. Dienste: Identifizieren Sie alle Dienste/Komponenten mit eindeutigen IDs.
2. Verbindungen: Erfassen Sie Abhängigkeiten zwischen Diensten.
3. Funktionen: Listen Sie Hauptfunktionen jedes Dienstes auf.
4. Warnungen: Notieren Sie fehlende Funktionen oder Einschränkungen.
5. Metadaten: Fügen Sie relevante Zusatzinformationen hinzu (Version, Datum, Verantwortliche).
Verwenden Sie dieses JSON-Format:
```json
{
  "services": [
    {
      "id": "service_id",
      "name": "Service Name",
      "description": "Kurzbeschreibung",
      "functions": [{"category": "Kategorie", "description": "Funktionsbeschreibung"}],
      "warnings": ["Warnung zu Einschränkungen"],
     "Team A"}
    }
  ],
  "connections": [
    {
      "source": "quell_service_id",
      "target": "ziel_service_id",
      "description": "Verbindungsbeschreibung"
    }
  ]
}
```
Schritt 3: Erstelle ein diagram:
When creating technical diagrams for documentation, follow these guidelines:
1. Use Mermaid syntax for all diagrams.
2. Start with a top-level flowchart:
TB
3. Group related elements using subgraphs:
end
4. Use appropriate node shapes:
Rectangle [] for general concepts
Rounded rectangle () for processes
Circle (()) for start/end points
Diamond {} for decisions
Cylinder [()] for databases
5. Connect nodes with appropriate arrows:
--> for normal flow
==> for emphasized flow
-.->for optional or background flow
6. Add labels to connections when necessary:
B
7. Use icons to enhance readability:
]
For complex diagrams, use nested subgraphs:
end
9. Use consistent color coding:
important
10. Add a title and brief description above the diagram.
Adjust the layout (TB, LR, RL, BT) as needed for best readability. Always prioritize clarity and simplicity in your diagrams.

Seien Sie konsistent in der Benennung und prägnant in den Beschreibungen. Markieren Sie fehlende Informationen mit "Keine Information verfügbar".

hier die doku aus der am ende ein technisches diagram entstehen soll:


## Übersicht über die Mermaid Diagramm Typen
```mermaid
stateDiagram-v2
    [*] --> MermaidDiagrams
    MermaidDiagrams --> typFlowchart
    MermaidDiagrams --> typSequenceDiagram
    MermaidDiagrams --> typClassDiagram
    MermaidDiagrams --> typStateDiagram
    MermaidDiagrams --> typEntityRelationshipDiagram
    MermaidDiagrams --> typGantt
    MermaidDiagrams --> typPieChart

    typFlowchart : Flowchart Diagram
    typSequenceDiagram : Sequence Diagram
    typClassDiagram : Class Diagram
    typStateDiagram : State Diagram
    typEntityRelationshipDiagram : Entity Relationship Diagram
    typGantt : Gantt Chart
    typPieChart : Pie Chart
```

### Flowchart Example
```mermaid
%% Flowchart Example
graph TD
    A[Start] --> B{Decision}
    B -->|Yes| C[Action 1]
    B -->|No| D[Action 2]
    C --> E[End]
    D --> E
```

### Sequence Diagram Example
```mermaid
%% Sequence Diagram Example
sequenceDiagram
    participant A as Alice
    participant B as Bob
    A->>B: Hello Bob, how are you?
    B-->>A: I'm good, thanks!
    A-)B: Great to hear!
    Note right of B: Bob thinks
    B->>A: How about you?
```

### Class Diagram Example
```mermaid
%% Class Diagram Example
classDiagram
    Animal <|-- Duck
    Animal <|-- Fish
    Animal : +int age
    Animal : +String gender
    Animal: +isMammal()
    Animal: +mate()
    class Duck{
        +String beakColor
        +swim()
        +quack()
    }
```

### State Diagram Example
```mermaid
%% State Diagram Example
stateDiagram-v2
    [*] --> Still
    Still --> [*]
    Still --> Moving
    Moving --> Still
    Moving --> Crash
    Crash --> [*]
```

### Entity Relationship Diagram Example
```mermaid
%% Entity Relationship Diagram Example
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```

### Gantt Chart Example
```mermaid
%% Gantt Chart Example
gantt
    title A Gantt Diagram
    dateFormat  YYYY-MM-DD
    section Section
    A task           :a1, 2014-01-01, 30d
    Another task     :after a1, 20d
    section Another
    Task in sec      :2014-01-12, 12d
    another task     :24d
```

### Pie Chart Example
```mermaid
%% Pie Chart Example
pie
    title Key elements in Product X
    "Calcium" : 42.96
    "Potassium" : 50.05
    "Magnesium" : 10.01
    "Iron" :  5
```

