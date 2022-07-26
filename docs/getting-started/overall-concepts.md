  [map]: #map
  [campaign]: #campaign
  [content]: #content

Broker

:   The broker is basically...

Worker

:   The Worker is basically...

Punnet

:   The Punnet is basically...



``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```


## Fast2 objects

### Folder

### Dataset

### Content <small>(aka 'ContentContainer')</small> { #content data-toc-label="Content" }

### Annotations

### Document

### Workflow

### Punnet

## Task

## Map <small>-- workflow</small> { #map data-toc-label="Map" }

## Campaign <small>-- workflow instance</small> { #campaign data-toc-label="Campaign" }