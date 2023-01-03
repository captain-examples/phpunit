# Getting Captain working with PHPUnit

Starting from a [simple workflow that runs PHPUnit][workflow-before-captain], we want to

1. 🧪 Ensure PHPUnit produces JUnit output

`phpunit --log-junit tmp/phpunit.xml` will produce Captain-compatible XML output in `tmp/phpunit.xml`.

```sh
vendor/bin/phpunit --log-junit tmp/phpunit.xml tests/
```

2. 🔐 Create an Access Token

Create an Access Token for your organization within [Captain][captain] ([more documentation here][create-access-token]).

Add the new token as an action secret to your repository. Conventionally, we call this secret `RWX_ACCESS_TOKEN`.

3. 💌 Install the Captain CLI, and then call it when running tests

See the [full documentation on test suite integration][test-suite-integration].

```yaml
- uses: rwx-research/setup-captain@v1
- run: |
    captain run \
      --suite-id captain-examples-phpunit \
      --test-results tmp/phpunit.xml \
      --language PHP \
      --framework PHPUnit \
      -- \
      vendor/bin/phpunit --log-junit tmp/phpunit.xml tests/
  env:
    RWX_ACCESS_TOKEN: ${{ secrets.RWX_ACCESS_TOKEN }}
```

4. 🎉 See your test results in Captain!

Take a look at the [final workflow!][workflow-with-captain]

[workflow-before-captain]: https://github.com/captain-examples/phpunit/blob/basic-workflow/.github/workflows/ci.yml
[captain]: https://account.rwx.com/deep_link/manage/access_tokens
[create-access-token]: https://www.rwx.com/docs/access-tokens
[workflow-with-captain]: https://github.com/captain-examples/phpunit/blob/main/.github/workflows/ci.yml
[test-suite-integration]: https://www.rwx.com/captain/docs/test-suite-integration
