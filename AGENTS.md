# Development Guide for Agents

## Build/Test Commands
- `make test` - Run all unit tests with race detection
- `make test-cover` - Run tests with coverage statistics  
- `make lint` - Run golangci-lint with project configuration
- `make vet` - Run go vet static analysis
- `make format` - Format code with gofmt
- `go test ./path/to/package` - Run tests for a specific package
- `go test -run TestName ./path/to/package` - Run a single specific test

## Code Style Guidelines
- Use `gofmt` for formatting (spaces, not tabs)
- Import order: standard library, third-party, local packages (prefix: github.com/gosom/google-maps-scraper)
- Use descriptive variable names (e.g., `entry`, `cfg`, `ctx`)
- Error handling: return errors, use `fmt.Errorf` with wrapping (`%w`)
- Use struct tags for JSON marshaling: `json:"field_name"`
- Constants use CamelCase (e.g., `RunModeFile`)
- Interface names end with -er suffix (e.g., `Runner`, `S3Uploader`)
- Use context.Context as first parameter in functions
- Prefer early returns to reduce nesting
- Use meaningful package names that reflect their purpose
- Add godoc comments for exported types and functions
- Use `nolint` comments sparingly with explanations
- Avoid magic numbers, use named constants or comment them

## Personal Notes
- When experimenting with scraper depth/concurrency settings, start low (1-2 workers) to avoid rate limiting
- The `--depth` flag significantly affects runtime; default of 1 is usually sufficient for most use cases
- Prefer running with `--lang en` when testing to keep output consistent and easier to parse
- For local CSV output, pipe results through `sort -u` to deduplicate if running the same query multiple times
- Use `--zoom 15` for city-level searches; zoom 12-13 works better for broader regional queries
- When scraping large result sets, add a short sleep between runs (`sleep 30`) to reduce the chance of soft bans
