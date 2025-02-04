Documentation

Private Serverless Models on GPUs

Setting Secrets

### Setting secrets[](#setting-secrets)

For setting sensitive information (such as API keys or database credentials) to be accessed within your fal functions you can use the `fal secrets` CLI interface.

    $ fal secrets set MY_API_TOKEN=token MY_IDENTITY_KEY=identity

Any secret that is set will be exposed to all functions running from your user, and can be accessible as if they are regular environment variables.

    import os
    import fal

    @fal.function()
    def print_secrets():
        print(os.getenv("MY_API_TOKEN"))
        print(os.getenv("MY_IDENTITY_KEY"))

    if __name__ == "__main__":
        print_secrets()

You can also list the secrets you have through the CLI, but the values will be hidden for security reasons.

    $ fal secrets list
    ┏━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
    ┃ Secret Name             ┃ Created At                 ┃
    ┡━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
    │ MY_API_TOKEN            │ 2023-09-05 15:17:39.279347 │
    │ MY_IDENTITY_KEY         │ 2023-09-05 15:17:41.444478 │
    └─────────────────────────┴────────────────────────────┘

To omit a secret from being present in new runs, you can simply delete it through the CLI:

    $ fal secrets unset MY_API_TOKEN

Last updated on October 4, 2024

[Return Files and Images from Functions](/docs/private-serverless-models/return-files-and-images "Return Files and Images from Functions")[Data Validation with Pydantic](/docs/private-serverless-models/pydantic "Data Validation with Pydantic")
