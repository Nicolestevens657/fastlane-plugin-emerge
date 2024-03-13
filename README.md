# Emerge `fastlane` plugin

[![fastlane Plugin Badge](https://rawcdn.githack.com/fastlane/fastlane/master/fastlane/assets/plugin-badge.svg)](https://rubygems.org/gems/fastlane-plugin-emerge)

## Getting Started

This project is a [_fastlane_](https://github.com/fastlane/fastlane) plugin. To get started with `fastlane-plugin-emerge`, add it to your project by running:

```bash
fastlane add_plugin emerge
```

## About Emerge

[Emerge](https://emergetools.com) offers a suite of products to help optimize app size, performance and quality. This plugin provides a set of actions to interact with the Emerge API.

## Usage

To get started, first obtain an [API token](https://docs.emergetools.com/docs/uploading-basics#obtain-an-api-key) for your organization. The API Token is used to authenticate with the Emerge API in each call.

```ruby
# Your EMERGE_API_TOKEN is available on your Emerge profile page: https://www.emergetools.com/profile
ENV['EMERGE_API_TOKEN'] = 'COPIED_FROM_EMERGETOOLS_PROFILE'

platform {:ios} do
  lane :app_size do
    emerge()
  end
end
```

For a full list of available parameters run `fastlane action emerge`.

## Git Configuration

For build comparisons to work, Emerge needs the appropriate Git `sha` and `base_sha` values set on each build. Emerge will automatically compare a build at `sha` against the build we find matching the `base_sha` for a given application id.

For example:

- `sha`: `pr-branch-commit-1`
- `base_sha`: `main-branch-commit-1`

Will compare the size difference of your pull request changes.

This plugin will automatically configure Git values for you assuming certain Github workflow triggers:

```yaml
on:
  # Produce base builds with a 'sha' when commits are pushed to the main branch
  push:
    branches: [main]

  # Produce branch comparison builds with `sha` and `base_sha` when commits are pushed
  # to open pull requests
  pull_request:
    branches: [main]

  ...
```

If this doesn't cover your use-case, manually set the `sha` and `base_sha` values when calling the Emerge plugin.

## Issues and Feedback

For any other issues and feedback about this plugin, please open a [GitHub issue](https://github.com/EmergeTools/fastlane-plugin-emerge/issues).

## Troubleshooting

If you have trouble using plugins, check out the [Plugins Troubleshooting](https://docs.fastlane.tools/plugins/plugins-troubleshooting/) guide.

## Using _fastlane_ Plugins

For more information about how the `fastlane` plugin system works, check out the [Plugins documentation](https://docs.fastlane.tools/plugins/create-plugin/).

## About _fastlane_

_fastlane_ is the easiest way to automate beta deployments and releases for your iOS and Android apps. To learn more, check out [fastlane.tools](https://fastlane.tools).
