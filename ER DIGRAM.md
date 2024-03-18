```mermaid
erDiagram
    USER {
        int userID PK
        string loginHash
        boolean isPal
    }

    VERIFICATION_TYPE {
        int vTypeID PK
        string vTypeName
    }

    USER_VERIFICATION  {
        int userID PK,FK
        int verifierID PK,FK
        int vTypeID PK,FK
        string gender "ID Verification, conditional field"
        string religion "ID Verification, conditional field"
        string language "ID Verification, conditional field"
        string nameHash "ID Verification, conditional field"
        string DOBHash "ID Verification, conditional field"
        string organizationLink "Partner Verification, conditional field"
    }

    REQUEST {
        int requestID PK
        int ownerID PK
        string nickName
        string content
        string imageURL "if any"
        int type "1: ads, 2: request"
        dateTime timeCreated
    }

    REQUEST_ACCESS {
        int requestID PK,FK
        int vTypeID PK,FK
        string gender "ID Verification, conditional field"
        string religion "ID Verification, conditional field"
        string language "ID Verification, conditional field"
        string nameHash "ID Verification, conditional field"
        string DOBHash "ID Verification, conditional field"
        string organizationLink "Partner Verification, conditional field"
    }

    RESPONSE {
        int userID PK,FK
        int requestID PK,FK
        string nickName
        string content
        string imageURL "if any"
        dateTime timeCreated
    }

    REVIEW {
        int userID PK,FK
        int reviewerID PK,FK
        int requestID PK,FK
        string nickname
        string notes
        string vote "yes, no"
        string editedVersion "if any"
        dateTime timeCreated
    }

    USER ||--o{ USER_VERIFICATION : "1"
    USER ||--o{ USER_VERIFICATION : "2"
    VERIFICATION_TYPE ||--|{ USER_VERIFICATION : ""
    USER ||--o{ REQUEST : "can create"
    USER ||--o{ RESPONSE : "can create"
    REQUEST ||--o{ RESPONSE : "may contain"
    REQUEST ||--o{ REQUEST_ACCESS : "may contain"
    VERIFICATION_TYPE ||--|{ REQUEST_ACCESS : ""
    USER ||--o{ REVIEW : ""
    RESPONSE ||--o{ REVIEW : ""
```

## **Notes:**

### **Verification Types**

1. **Partner Verification:**

   - Organization link

2. **Gaza Verification:**

3. **ID Verification:**

   - Gender
   - Religion
   - Language
   - Name (hashed)
   - DOB (hashed)

4. **Qualification Verification:**

### **Conditional Fields**

This is a relational database, so conditional fields are not best represented here. However, we are using this approach just to visualize the system.

### **Pending Responses**

Only when the response is from **non Gaza Verified** to **Gaza verified** that is currently in Gaza.
It is validated by around 10 ID verified users who can also edit the response.

### **Contributing**

As mentioned above, this is one way to visualize the system. So, please feel free to add to it or to fix any mistake.
