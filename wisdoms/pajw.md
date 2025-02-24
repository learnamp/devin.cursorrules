# Learning & Collaboration Patterns

- Strengths observed:
  - Systematic approach to problem-solving
  - Focus on maintainable, clean code
  - Interest in understanding root causes
  - Attention to testing and error handling

- Areas for growth together:
  - Discuss architectural decisions before implementation
  - Share knowledge about testing patterns
  - Explore new tools and approaches
  - Challenge assumptions and improve processes

- Continuous improvement:
  - Document learnings immediately while fresh
  - Reflect on what worked/didn't in each task
  - Look for patterns that could be automated
  - Question if our current approach is optimal

- Communication preferences:
  - Prefer explicit error handling and logging
  - Value clear documentation and examples
  - Appreciate systematic problem breakdown
  - Like to understand the why, not just the how

# Development Practices

- Always read files before attempting to edit them to understand context and dependencies
- Include debug information in program output to aid troubleshooting
- Keep changes minimal and focused - only modify what's necessary
- When fixing style issues, only address the lines you're modifying
- Maintain conversation history and context:
  ```
  wisdoms/
    current/           # Current conversation and context
    indexes/          # Topic and timeline indexes
    archive/         # Historical conversations
    lessons/         # Permanent lessons learned
  ```
- Use SCRATCHPAD.md for task planning and progress tracking
- Before starting new tasks:
  - Review relevant wisdom files
  - Check for similar patterns in codebase
  - Consider testing and maintenance implications
  - Plan for future extensibility

# Code Style Guidelines

- Check style compliance before running tests:
  ```bash
  # Ruby
  bundle exec rubocop path/to/file.rb

  # JavaScript/TypeScript
  yarn prettier --check path/to/file.js
  yarn eslint path/to/file.js
  ```
- Read style configs instead of running tools repeatedly:
  - `.rubocop.yml` for Ruby style rules
  - `.prettierrc.json` for Prettier configuration
  - `.eslintrc.js` for ESLint rules
- For Ruby:
  - Follow RuboCop's suggestions for your changes only
  - Never run `rubocop -a` on entire files
  - Keep method alignment consistent:
    ```ruby
    some_method(
      arg1: value1,
      arg2: value2
    )
    ```
- For JavaScript/TypeScript:
  - Run Prettier before ESLint
  - Fix ESLint warnings incrementally
  - Keep consistent formatting in component files

# Testing Best Practices

- Run specific test files after changes:
  ```bash
  rails test test/path/to/test.rb
  yarn test:component test/path/to/test.js
  ```
- In test environment:
  - Consider differences between CI and local setup
  - Handle test-specific initialization carefully
  - Use instance variables for one-time setup when appropriate
  - Add descriptive error handling and logging
- For feature toggle tests:
  - Groups registered in initializers don't persist in memory adapter
  - Register groups manually in test setup when needed
  - Handle duplicate registration gracefully:
  ```ruby
  def register_test_group
    Flipper.register(group_key) { |actor| actor.matches?(criteria) }
  rescue Flipper::DuplicateGroup
    Rails.logger.debug "Group #{group_key} already registered"
  end
  ```

# Feature Toggle Guidelines

- Use `FeatureToggle.register` for new features (automatically handles Flipper registration)
- Enable features for specific actors before use in BetaFeature
- Consider persistence differences between environments:
  - Production: Configured in initializers
  - Test: Memory adapter requires manual setup
  - Development: May need explicit enabling

# Git Workflow

- For multiline commit messages:
  ```bash
  # Write message to temp file
  echo "[Cursor] Your commit message" > commit_msg.txt
  git commit -F commit_msg.txt
  rm commit_msg.txt
  ```
- Keep commit messages focused and descriptive
- Include ticket references where applicable
- Always run git commands from project root

# Project Configuration

- Python: Use venv in `./venv`
- Matplotlib: Use 'seaborn-v0_8' style
- OpenAI: Use 'gpt-4o' for vision capabilities
- Character encoding: Ensure UTF-8 for international support
- Logging: Debug info to stderr, keep stdout clean

# Auto-approved Commands
The following can run without explicit approval:
- Rails and JavaScript test commands
- pwd, ls
- bundler
- git, gh
