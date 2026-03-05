```mermaid
graph TD
    %% Definicja stylów (wizualne odróżnienie elementów PROV)
    classDef entity fill:#FFFACD,stroke:#333,stroke-width:2px;
    classDef activity fill:#ADD8E6,stroke:#333,stroke-width:2px;
    classDef agent fill:#FFB6C1,stroke:#333,stroke-width:2px;

    %% 1. Agenci (Agents)
    Laura{{Laura}}:::agent
    Jack{{Jack}}:::agent
    Jill{{Jill}}:::agent
    Peter{{Peter}}:::agent
    Paula{{Paula}}:::agent
    Zack{{Zack}}:::agent
    CoAuthors{{Other co-authors}}:::agent

    %% 2. Byty i Plany (Entities & Plans)
    Survey1([Survey v1]):::entity
    Survey2([Survey v2]):::entity
    Data1([Data 1]):::entity
    Data2([Data 2]):::entity
    CompiledData([Compiled results]):::entity
    StatPackage([Statistics package]):::entity
    AnalysisResults([Analysis results]):::entity
    Paper([Published paper]):::entity

    %% 3. Aktywności (Activities)
    Design1[Designing survey v1]:::activity
    Conduct1[Conducting survey 1]:::activity
    Revise[Revising survey]:::activity
    Conduct2[Conducting survey 2]:::activity
    Compile[Compiling data]:::activity
    Analyze[Analyzing data]:::activity
    Publish[Publishing paper]:::activity

    %% 4. Relacje: wasAssociatedWith (Aktywność -> Agent)
    Design1 -->|wasAssociatedWith| Laura
    Conduct1 -->|wasAssociatedWith| Jack
    Conduct1 -->|wasAssociatedWith| Jill
    Revise -->|wasAssociatedWith| Laura
    Conduct2 -->|wasAssociatedWith| Peter
    Conduct2 -->|wasAssociatedWith| Paula
    Compile -->|wasAssociatedWith| Zack
    Analyze -->|wasAssociatedWith| Zack
    Publish -->|wasAssociatedWith| Zack
    Publish -->|wasAssociatedWith| Laura
    Publish -->|wasAssociatedWith| CoAuthors

    %% 5. Relacje: used (Aktywność -> Byt)
    Conduct1 -->|used| Survey1
    Revise -->|used| Survey1
    Conduct2 -->|used| Survey2
    Compile -->|used| Data1
    Compile -->|used| Data2
    Analyze -->|used| CompiledData
    Analyze -->|used| StatPackage
    Publish -->|used| AnalysisResults

    %% 6. Relacje: wasGeneratedBy (Byt -> Aktywność)
    Survey1 -->|wasGeneratedBy| Design1
    Data1 -->|wasGeneratedBy| Conduct1
    Survey2 -->|wasGeneratedBy| Revise
    Data2 -->|wasGeneratedBy| Conduct2
    CompiledData -->|wasGeneratedBy| Compile
    AnalysisResults -->|wasGeneratedBy| Analyze
    Paper -->|wasGeneratedBy| Publish

    %% 7. Relacje: wasRevisionOf & wasDerivedFrom (Byt -> Byt)
    Survey2 -.->|wasRevisionOf| Survey1
    CompiledData -.->|wasDerivedFrom| Data1
    CompiledData -.->|wasDerivedFrom| Data2
