# Bits and Bytes

# Bit
- plaats een 

![bit](images/bit.gif)

```mermaid
classDiagram
    class Persoon {
        +string naam
        +int leeftijd
        +void eet()
        +void slaapt()
    }

    class Student {
        +string school
        +void studeert()
    }

    class Leraar {
        +string vak
        +void geeftLes()
    }

    Persoon <|-- Student
    Persoon <|-- Leraar
