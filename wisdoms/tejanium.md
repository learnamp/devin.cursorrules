# User Specified Lessons

- When making changes to a test file, run the individual test file (e.g. `rails test test/models/bulk_item_import_test.rb`) after each change to verify the changes work.
- In tests, avoid using `index.zero?` with array indexing. Instead use explicit methods like `find_by(attribute: value)` to make tests more readable and maintainable.
- When creating PRs with `gh pr`, always choose `learnamp/learnamp`, NEVER create a fork.
- PR titles should start with the JIRA ticket number in the format `[LA-XXXXX]`, not `[Cursor]`.
- Never run `rubocop -a` on the whole file, fix RuboCop warnings manually to maintain control over changes.
- Only fix RuboCop issues in lines that you have modified - do not fix style issues in untouched code.
- Never refactor code unless explicitly requested to do so.
- Keep changes minimal and focused - only modify relevant lines and never touch unrelated files or code.
- In tests, keep blank lines between logical groups of assertions but remove unnecessary blank lines between related assertions within the same group.
- Always execute git commands inside the project directory to ensure proper context and hooks are applied.
- Always use `SCRATCHPAD.md` for task planning and progress tracking, never put scratchpad content in `.cursorrules`.
- Always run RuboCop before running tests to catch style issues early and maintain consistent code quality. Example:
  ```bash
  bundle exec rubocop path/to/test/file.rb
  ```
- Instead of running RuboCop repeatedly, read the `.rubocop.yml` file and use that as a style guide.
- For string concatenation with backslash, indent the continuation line one level from the start of the string:
  ```ruby
  message = 'first line ' \
             'second line'
  ```
- When starting a new task with a JIRA ticket:
  1. Create a new branch from latest trunk:
     ```bash
     git checkout trunk
     git pull
     ```
  2. Create branch with format `LA-XXXXX/description-of-task`
  3. Never push directly to trunk

# Ruby Specific Lessons

- For test assertions with complex data structures, use multi-line format with parentheses for better readability:
  ```ruby
  assert_equal(
    actual,
    {
      key: {
        nested_key: value
      }
    }
  )
  ```
- When working on a specific test, run it by line number (e.g. `rails test test/path/to/test.rb:123`) instead of running the entire test file for faster feedback
- Use Mocha instead of Minitest::Mock for stubbing and mocking in tests - it's more reliable and provides better error messages
- Always run RuboCop after making changes to verify code style compliance
- Use `assert_called` instead of Minitest::Mock for verifying method calls - it's more concise and provides better error messages. Example:
  ```ruby
  assert_called(MyClass, :my_method, returns: value) do |mock|
    # do something that should call my_method
    assert_equal expected_args, mock.calls.first.args
  end
  ```
- For verifying method calls in tests, prefer Mocha's `expects` over `assert_called` when you know the exact arguments - it's more explicit and verifies at call time. Example:
  ```ruby
  MyClass.expects(:my_method)
         .with(expected_args)
         .returns(value)
  ```
- For multi-line method calls, put the opening parenthesis on the first line and align parameters under it:
  ```ruby
  # Good
  some_method(
    foo: 'bar',
    baz: 'qux'
  )

  # Bad
  some_method(foo: 'bar',
              baz: 'qux')
  ```
