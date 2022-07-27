  [map]: #map
  [campaign]: #campaign
  [content]: #content

Broker

:   The broker is basically...

Worker

:   The Worker is basically...

Punnet

:   The Punnet is basically...


## Fast2 objects

### Folder

``` 
ㄴ folder
	ㄴ name
	ㄴ path
	ㄴ parent folder
		ㄴ name
		ㄴ path
		ㄴ parent folder
			ㄴ ...
```

### Dataset

### Content <small>(aka 'ContentContainer')</small> { #content data-toc-label="Content" }

### Annotations

### Document

### Workflow

### Punnet

#### Lifecycle

<!-- https://mermaid-js.github.io/mermaid/#/flowchart -->

``` mermaid
graph TD
  A(Created) --> B(Queued);
  B --> C(Processing);
  C --> D{ };
  D -->|Success| F(Processed OK);
  D -->|Failure| E(Processed KO);
  F -. Next task ? .-> B;
  E -.-> |Retry| H( );
  F -.-> |Retry| H;
  H -.-> I( );
  I -.->|Previous try| J{ };
  I -.-> B;
  J -.->|KO| L[SupersededException];
  J -.->|OK| K[SupersededOK];
```

## Task

## Map <small>-- workflow</small> { #map data-toc-label="Map" }

## Campaign <small>-- workflow instance</small> { #campaign data-toc-label="Campaign" }

### Lifecycle

``` mermaid
graph LR
  A(Undefined) --> B(Starting);
  B --> C(Started);
  C --> D(Running);
  D -.->|Stops source iterator| F(Stopping);
  D --> E(Finished);
  F -.->|Restart source iterator| B;
```

### Operating