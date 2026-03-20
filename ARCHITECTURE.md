# Architecture: cakephp-codesniffer

## Purpose

A PHP_CodeSniffer standard for CakePHP projects. It defines custom sniff rules enforcing CakePHP's coding conventions (naming, whitespace, commenting, control structures) and is used in CI pipelines via `phpcs --standard=CakePHP`.

## Directory Structure

```
CakePHP/
  ruleset.xml                        — The CodeSniffer standard definition (lists sniffs and references)
  Sniffs/
    Classes/
      ReturnTypeHintSniff.php        — Enforces return type hint declarations
    Commenting/
      DocBlockAlignmentSniff.php     — Checks @param/@return alignment in docblocks
      FunctionCommentSniff.php       — Validates function docblock presence and content
      InheritDocSniff.php            — Enforces correct use of {@inheritDoc}
      TypeHintSniff.php              — Validates type hint usage in docblocks
    ControlStructures/
      ControlStructuresSniff.php     — Checks brace placement for if/else/foreach/while
      ElseIfDeclarationSniff.php     — Prefers `elseif` over `else if`
      WhileStructuresSniff.php       — Validates while loop formatting
    Formatting/
      BlankLineBeforeReturnSniff.php — Requires a blank line before return statements
    NamingConventions/
      ValidFunctionNameSniff.php     — Enforces camelCase function names per CakePHP conventions
      ValidTraitNameSniff.php        — Enforces StudlyCaps trait names
    PHP/
      DisallowShortOpenTagSniff.php  — Bans `<?` short open tags
      SingleQuoteSniff.php           — Prefers single quotes for simple strings
    WhiteSpace/
      EmptyLinesSniff.php / TabAndSpaceSniff.php / Function*Sniff.php — Various spacing rules
  Tests/                             — Unit tests for each sniff (using CodeSniffer's test framework)

docs/
  generate.php                       — Script to auto-generate per-sniff documentation
```

## Key Design Decisions

- **CodeSniffer standard** — follows PHP_CodeSniffer's sniff API: each sniff implements `register()` (token list) and `process()` (violation reporting).
- **Extends PSR-2** — `ruleset.xml` references PSR-2 rules and extends/overrides them with CakePHP-specific preferences.
- **Each sniff is independently testable** — test fixtures in `Tests/` provide PHP files that should pass or fail each rule.

## Extension Points

- Add new sniffs by creating a class in `CakePHP/Sniffs/` following CodeSniffer's `AbstractSniff` contract.
- Reference additional rules from other standards (PSR-12, Squiz, etc.) in `ruleset.xml`.
