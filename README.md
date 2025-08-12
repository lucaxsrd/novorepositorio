# We will only run this action when:
# 1. This repository isn't the template repository.
# 2. The step is currently 1.
# Reference: https://docs.github.com/en/actions/learn-github-actions/contexts
# Reference: https://docs.github.com/en/actions/learn-github-actions/expressions
if: >-
  ${{ !github.event.repository.is_template
      && needs.get_current_step.outputs.current_step == 0 }}

# We'll run Ubuntu for performance instead of Mac or Windows.
runs-on: ubuntu-latest

steps:
  # We'll need to check out the repository so that we can edit README.md.
  - name: Checkout
    uses: actions/checkout@v4
    with:
      fetch-depth: 0 # Let's get all the branches.

  # In README.md, switch step 0 for step 1.
  - name: Update to step 1
    uses: skills/action-update-step@v2
    with:
      token: ${{ secrets.GITHUB_TOKEN }}
      from_step: 0
      to_step: 1
      branch_name: my-first-branch
