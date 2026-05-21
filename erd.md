erDiagram
    User {
        int id PK
        string name
        string email
        string password_hash
        string phone
        string role
        string avatar_url
    }

    Library {
        int id PK
        string phone
        string address
        string schedule
    }

    Book {
        int id PK
        int library_id FK
        string isbn
        string title
        string author
        string annotation
        int year_published
        string format
        int amount
        string license
    }

    Review {
        int id PK
        int user_id FK
        int library_id FK
        int rating
        string comment
    }

    Hold {
        int id PK
        int user_id FK
        int book_id FK
        int library_id FK
        date date_created
    }

    Loan {
        int id PK
        int book_id FK
        int library_id FK
        int user_id FK
        date date_start
        date date_end
    }

    Notification {
        int id PK
        int user_id FK
        string type
        string message
        boolean is_read
        datetime sent_at
    }

    Library_cards {
        int id PK
        string code
        int library_id FK
    }

    Library ||--o{ Book : contains
    User ||--o{ Review : writes
    Library ||--o{ Review : receives

    User ||--o{ Hold : places
    Book ||--o{ Hold : reserved
    Library ||--o{ Hold : manages

    User ||--o{ Loan : borrows
    Book ||--o{ Loan : loaned
    Library ||--o{ Loan : issues

    User ||--o{ Notification : receives

    Library ||--o{ Library_cards : issues
