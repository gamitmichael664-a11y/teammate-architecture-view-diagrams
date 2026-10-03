# Agap Buhay Management System

Web-based system for managing beneficiary and assistance records.

## C4 System Context Diagram

```mermaid
C4Context
    title C4 System Context Diagram - Agap Buhay Management System

    Person(member, "Member", "Register member, view updates, send messages")
    Person(secretary, "Secretary", "Registers, searches, views, updates beneficiaries and manages assistance records")

    System(abms, "Agap Buhay Management System", "Web-based system for managing beneficiary and assistance records")
    System_Ext(db, "Database Server", "Stores beneficiary, assistance, user, and report records")

    Rel(member, abms, "Provides and submits beneficiary information", "HTTPS")
    Rel(secretary, abms, "Manages beneficiary and assistance records", "HTTPS")
    Rel(abms, db, "Stores and retrieves records", "MySQL")

    UpdateLayoutConfig($c4ShapeInRow="2", $c4BoundaryInRow="1")
```

## C4 Container Diagram

```mermaid
C4Container
    title C4 Container Diagram - Agap Buhay Management System

    Person(member, "Member", "Register member, view update, and send messages")
    Person(secretary, "Secretary", "Manages beneficiary and assistance records")

    System_Boundary(abms, "Agap Buhay Management System") {
        Container(web, "Web Application", "HTML5, CSS3, JavaScript, Bootstrap", "Provides the user interface for members and staff")
        Container(app, "Application Server", "PHP / Laravel", "Processes authentication, beneficiary, assistance, search, update, and report requests")
        ContainerDb(db, "Database", "MySQL", "Stores users, beneficiaries, assistance records, and reports")
    }

    Rel(member, web, "Accesses system", "HTTPS")
    Rel(secretary, web, "Uses management functions", "HTTPS")
    Rel(web, app, "Sends requests", "HTTPS")
    Rel(app, db, "Reads and writes records", "MySQL")

    UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```

## Deployment Diagram

```mermaid
flowchart TB
    provisional["Provisional"]

    subgraph staffDevice["Staff Device"]
        staffBrowser["Web Browser<br/>Chrome / Edge"]
    end

    subgraph memberDevice["Member Device"]
        memberBrowser["Web Browser<br/>Chrome / Edge"]
    end

    subgraph appServer["Web/Application Server"]
        apache["Apache HTTP Server"]
        laravel["Laravel Application<br/>PHP"]
    end

    subgraph dbServer["Database Server"]
        mysql["MySQL Database"]
    end

    webApp["Agap Buhay Web Application"]
    dbArtifact["Agap buhay Database"]

    staffBrowser -->|HTTPS| apache
    memberBrowser -->|HTTPS| apache
    apache -->|HTTP| laravel
    laravel -->|MySQL Protocol| mysql

    laravel -. Runs .-> webApp
    mysql -. stores .-> dbArtifact

    classDef node fill:#d5e8d4,stroke:#82b366,color:#333
    classDef artifact fill:#ececff,stroke:#9370db,color:#333
    class staffDevice,memberDevice,appServer,dbServer node
    class provisional,webApp,dbArtifact,staffBrowser,memberBrowser,apache,laravel,mysql artifact
```

<!-- Optional: for the exact draw.io look (3D boxes), add Deployment_Diagram.svg to docs/ and use:
![Deployment Diagram](docs/Deployment_Diagram.svg)
-->
