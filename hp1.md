# Handy Potato: 1 - Python Style Guidelines

## Abstract

Since we make free and open-source software (FOSS), we accept contributions from people across the world. Everyone has their way of writing code. But the code should be consistent.

## Specification

### Requirements

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as shown here.

The guidelines stated here should only be used if it is reasonable, and it isn't required/noted otherwise.

### The Guidelines

- The code MUST follow PEP 8. Some additional stuff to PEP 8:
  - If you cannot break a line, try to use a backslash (`\`)
  - Line breaks (as stated in PEP 8) should be BEFORE any operators
  - Code MUST (only) use UTF-8.
  - Names (variable, function, file, ...) SHOULD use snake_case; class names SHOULD use CapWords (CamelCase).
  - Except for one-line ones, docstring MUST have a new line after the opening, and before the closing([example](https://github.com/sco1/flake8-annotations/blob/7e44ba73866e92fcce8d1c9ca082ffaabec99d9c/flake8_annotations/checker.py#L53-L58)). (This is permitted by [PEP 257](https://archive.ph/kY0Hw#selection-615.313-615.399).)
  - As described in PEP 257, double-quotes MUST be used for docstrings.

- Double-quotes MUST be used. If double-quotes are already in the string (except docstrings and triple quote strings), single-quotes SHOULD be used; escaping (`\"`) MAY be used.

- Semi-colons (in code) MUST NOT be used (unless for timeit codes).

- The walrus operator (`:=`) SHOULD NOT be used, for compatibility reasons until June 2023. After that, it MAY be used.

- Logging SHOULD be done with [mylog](https://github.com/koviubi56/mylog).

- A star ("*", keyword only), and a slash ("/", positional only) MAY be used in arguments.

- Exception types MAY inherit from "Exception"; they SHOULD NOT inherit directly from "BaseException".

- There SHOULD be backwards and forward compatibility.

- Properties SHOULD NOT have setters. Try changing them to an instance variable, or make a "set_*" and a "get_*" method for it.

- Comprehensions and in-line statements MAY be used, but only if they are easy to read and understand.

- `is` and `is not` MUST be used for [real constants](https://docs.python.org/3/library/constants.html#built-in-constants), classes, and singletons, and they MUST NOT be used for literals (str, int, float, ...) except if it's something like `MISSING = object()`.

- "Just container" classes SHOULD use dataclasses([example](https://github.com/IBM/lmctl/blob/0d0efd979301f369f17f0cd95f7262710d8d62c9/tests/unit/utils/dcutils/test_dc_to_dict.py#L8-L12)).

- Properties MUST be kept short, they MUST NOT do expensive calculations.

- Threads SHOULD only be used sparingly, and/or only if the user knows about them. There MUST NOT be a lot of threads. Threads SHOULD be daemon.

- For files, directories, folders, paths, `pathlib.Path`, and its methods SHOULD be used.

- If possible always use binary reads and writes (this means pass binary instead of string to `json.load`, but feel free to use regular reads and writes when it is reasonable). If binary cannot be used, UTF-8 SHOULD be used. The encoding argument MUST be passed as a keyword argument, and it MUST be written as "utf-8" (all lowercase).

- f-strings SHOULD be used instead of "{}".format() and "" + x + "". In f-strings `{x!r}` (and others) MUST be used instead of `{repr(x)}`.

- Too broad `except`s SHOULD NOT be used, unless reasonable (because there are situations where you do need it).

#### Docstrings

- The [Google docstring style](https://www.sphinx-doc.org/en/master/usage/extensions/example_google.html) MUST be used, BUT:

  - There MUST be a new line after the opening.
  - Module/Package/Class level docstrings SHOULD NOT have a "Attributes" section
  - Docstrings MUST NOT have a "Todo(s)" nor "Note(s)" section.
  - reStructuredText or anything like that MUST NOT be used.
  - Attributes and variables SHOULD NOT have docstrings (with triple quotes). They MAY have simple/normal comments (#).
  - Examples (doctests) MUST be put after the main description, and before the arguments (but the use of docstrings is OPTIONAL).
  - Argument types in docstrings MUST reflect the type hints (so `:obj:int` and `list(str)` MUST NOT be used, `List[str]` MUST be used instead).
  - Argument types in docstrings MUST have `, optional` before the `)` if they are optional, and they MUST have `Defaults to x.` at the end.
  - Properties' and special/magic method's docstrings MUST be the same as if they were a function.
  - `self` MUST NOT be included in `Args`.
- Every function SHOULD have a docstring, and they MAY have a doctest. Any function that starts with an underscore (e.g. `_private`, `__really_private`, `__magic__`) MAY have a docstring.

#### Type hinting

- Type hints MUST be used for function arguments, function return values, and other places where possible and reasonable.
- Type hints MAY be used with local and/or private variables.
- The generics MUST be provided when using generic types (`list[str]`, `dict[str, int]`, ...).
- Until 2024 October `typing` generics MUST be used instead of built-in generics (`typing.List` before 2024 October; `list` after).
- The `if TYPE_CHECKING: import` style([example](https://github.com/pydantic/pydantic/blob/5dd9b4f5ca5715ed2bd65378201473b45c419c89/pydantic/main.py#L74-L91)) MUST NOT be used. Additionally only type hinting something when `TYPE_CHECKING` is True MUST NOT be used([example](https://github.com/pydantic/pydantic/blob/5dd9b4f5ca5715ed2bd65378201473b45c419c89/pydantic/main.py#L312-L327)).
- If possible, most of the type hinting stuff imported from `typing` SHOULD be moved to `typing_extensions` for forward compatibility.

## Copyright

This document has been placed in the public domain.
