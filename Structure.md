Drift2PR/
├── cmd/
│   └── drift2hcl/        # Cobra CLI entrypoint
├── internal/
│   ├── ingest/           # Parses Terraform plan JSON & cloud activity diffs
│   ├── mapper/           # Maps cloud resource IDs to Terraform addresses
│   ├── astpatch/         # AST manipulation using HashiCorp hclwrite & go-cty
│   ├── ai/               # Bounded fallback agent for complex dynamic blocks
│   └── verify/           # Local sandbox validation and Git PR dispatch
├── go.mod
└── README.md
