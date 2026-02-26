---
title: google-integration
---
```mermaid
flowchart LR
    subgraph Client
        A[Browser]
        B[Mobile App]
    end

    subgraph Server
        C[API Server]
        D[Auth Service]
    end

    subgraph Data
        E[(PostgreSQL)]
        F[(Redis Cache)]
    end

    A --> C
    B --> C
    C --> D
    C --> E
    C --> F

    style C fill:#3b82f6,color:#fff
    style D fill:#8b5cf6,color:#fff
    style E fill:#10b981,color:#fff
    style F fill:#f97316,color:#fff
```

```typescript
type ApiResponse<T> = {
  data: T
  error?: string
}

export async function fetchJSON<T>(url: string): Promise<ApiResponse<T>> {
  try {
    const res = await fetch(url)

    if (!res.ok) {
      throw new Error(`HTTP ${res.status}`)
    }

    const data = await res.json()
    return { data }
  } catch (error) {
    return { data: null as T, error: (error as Error).message }
  }
}
```

​
