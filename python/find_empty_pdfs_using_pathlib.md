# Find Empty PDFs Using Pathlib

_Today I Learned added on 2025-11-20, learned on 2025-11-19._

In generating routine forecast visualizations yesterday, I received an error thrown by `pypdf` that the a PDF I was processing was empty (the forecast visualizations are aggregated into PDFs). After checking the usual (internal R package was installed and I was logged-in and authentized by Azure), I determined that it was time to actually find the empty PDF.

As I was working in Python, I expected there to be some one-line solutions. The solution I came up with may not be the best in terms of line-length or speed, but it worked OK for my use case:

```python
import pathlib


pdf_files = [f for f in pathlib.Path(".").rglob("*.pdf") if f.stat().st_size == 0]
```

This line recursively gets all PDF files in the current (`"."`) directory and all its sub-directories and adds them to the list if the size of the file is 0 (`if f.stat().st_size == 0`).
