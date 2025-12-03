# Bone Age Prediction System Architecture

```mermaid
graph TD
    subgraph Input
        A[Hand Radiograph Image] --> B{Preprocessing}
    end

    subgraph "Path A: Classical Machine Learning"
        B -->|Resize & Grayscale| C[Feature Extraction]
        C --> D[HOG Features]
        C --> E[LBP Features]
        D --> F[Feature Concatenation]
        E --> F
        F --> G[PCA Dimensionality Reduction]
        G --> H{Regression Models}
        H --> I[Random Forest]
        H --> J[SVR]
        H --> K[Linear Regression]
        I --> L[Ensemble Prediction]
        J --> L
        K --> L
    end

    subgraph "Path B: Deep Learning (CNN)"
        B -->|Resize & Normalize| M[ResNet50 Backbone]
        M -->|Feature Maps| N[Global Average Pooling]
        N --> O[Dense Layer (256, ReLU)]
        O --> P[Dropout (0.5)]
        P --> Q[Output Layer (Linear)]
    end

    subgraph Output
        L --> R((Predicted Bone Age))
        Q --> R
    end

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style R fill:#9f9,stroke:#333,stroke-width:2px
    style M fill:#bbf,stroke:#333,stroke-width:1px
    style H fill:#bfb,stroke:#333,stroke-width:1px
```
