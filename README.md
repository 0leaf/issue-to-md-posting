# issue-to-md-posting
This action to help you manage static page blog posts like jekyll as github issues.


## Input arguments

In order to pass the input parameters to the issue-to-md-posting action, you have to use the with argument in a step that uses the action,
If you do not need to change the default values of all parameters, you do not need to pass any values.
e.g.

```yaml

jobs:
  posting-release:
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Release post
        uses: 0leaf/issue-to-md-posting@v0.1.1
        with:
          post_base_path: '_posts'
       #   author: 'author'
       #   author_email:  'author@noreply.com'
```

Here are all the parameters you can change via the inputs available

|           Input            |                          Description                           |               Default             |
| -------------------------- | -------------------------------------------------------------- | --------------------------------- |
| `post_base_path`           | Path to the directory for post                                 | `_posts`                          |
| `author`                   | Author name                                                    | `${{ github.actor }}`             |
| `author_email`             | Author email address                                           | `${{ github.actor }}@noreply.com` |


## Example Usage
When configured as in the following example, the time of posting release can be configured as the time when the "release" tag attached.

```yaml
name: posting-by-issue

on:
  issues:
    types:
      - labeled

jobs:
  posting-release:
    if: github.event.label.name == 'release'
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Release post
        uses: 0leaf/issue-to-md-posting@v0.1.1
        with:
          post_base_path: '_posts'
```

## With jekyll
Using this actions with the following steps will make blog posts easier.
- Build a github.io static page blog with Jekyll.
- Configure workflow using this actions. (0leaf/issue-to-md-posting)
- Configure issue template for posting metadata.

## Cautions
- The title of the issue should follow the format like `2022-08-27-article title`
- When posting is completed, a completion message will be attached to the issue, and the tag will be deleted.
