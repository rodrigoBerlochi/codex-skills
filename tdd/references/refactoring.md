# Refactor Candidates

After a green test run, look for:

- Duplication that should be extracted
- Long methods that should be split behind the same public interface
- Shallow modules that should be combined or deepened
- Feature envy, where logic belongs closer to the data it uses
- Primitive obsession that wants a value object
- Existing design problems exposed by the new slice
