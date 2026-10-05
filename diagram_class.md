# Diagramme de classes — Exercice 4

```mermaid
classDiagram

    class ConversationMemorable {
        +int id
        +String titre
        +String contenu
        +String pourquoiMarquante
        +int note
        +String evaluationPerformance
        +String explicationPerformance
    }

    class Participant {
        +int id
        +String nom
    }

    class LLM {
        +int id
        +String nom
        +String version
    }

    class Emotion {
        +int id
        +String nom
    }

    class TypeImpact {
        +int id
        +String nom
    }

    class CategorieTache {
        +int id
        +String nom
    }

    Participant "1" --> "0..*" ConversationMemorable : crée
    LLM "1" --> "0..*" ConversationMemorable : utilisé dans
    Emotion "1" --> "0..*" ConversationMemorable : caractérise
    TypeImpact "1" --> "0..*" ConversationMemorable : caractérise
    CategorieTache "1" --> "0..*" ConversationMemorable : catégorise
    TypeImpact "1" --> "0..*" ConversationMemorable : caractérise
    CategorieTache "1" --> "0..*" ConversationMemorable : catégorise
