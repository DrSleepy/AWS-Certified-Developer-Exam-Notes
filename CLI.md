# Command Line Interface (CLI)

## Pagination

- by default, AWS CLI uses a "page size" of 1,000
  - so to get all 2,500 items in a bucket the API will make 3 calls to S3
  - will still display all items at once

**Errors & Fixes:**

- Sometimes a page size of 1,000 may be too high, which can cause errors
- You are most likely to see "timed out" error
  - solved by using --page-size flag
