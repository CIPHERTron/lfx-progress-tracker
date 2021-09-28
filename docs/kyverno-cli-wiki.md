## How to use Kyverno CLI in development mode?

"_The Kyverno Command Line Interface (CLI) is designed to validate and test policy behavior to resources prior to adding them to a cluster. The CLI can be used in CI/CD pipelines to assist with the resource authoring process to ensure they conform to standards prior to them being deployed._"

You can install and use the kyverno cli using [`krew`](https://kyverno.io/docs/kyverno-cli/#install-via-krew), [`yay`](https://kyverno.io/docs/kyverno-cli/#install-via-aur-archlinux) or by directly [building it from source](https://kyverno.io/docs/kyverno-cli/#building-the-cli-from-source). But here, we will see how to use kyverno CLI in development mode. Basically the usage remains the same except that here, you've to execute the Go package i.e. `cmd/cli/kubectl-kyverno/main.go` which essentially calls the kyverno CLI.

## Example
Let's say you've to run the `test` command to `validate` the [Disallow Latest Tag](https://kyverno.io/policies/best-practices/disallow_latest_tag/disallow_latest_tag/) policy.
To do this using the kyverno CLI, you run: <br>
```
kyverno test ../policies/best-practices/disallow_latest_tag
```
But to use the kyverno CLI in the development mode, follow these steps:
1. Make sure you've cloned the fork of [`kyverno/kyverno`](https://github.com/kyverno/kyverno) and [`kyverno/policies`](https://github.com/kyverno/policies) in the same directory. Your workspace should be looking something like this:

```
/kyverno
    api
    charts
    cmd
    definitions
    docs...

/policies
    best-practices
    cert-manager
    other
    pod-security...
```

2. `cd` into `kyverno` directory _(which is your local fork of [`kyverno/kyverno`](https://github.com/kyverno/kyverno))_
3. Run the below mentioned command:

```
go run ./cmd/cli/kubectl-kyverno/main.go test ../policies/best-practices/disallow_latest_tag
```
4. On executing the above command, you'll get an output as follows:
```
Executing disallow_latest_tag...
applying 1 policy to 1 resource... 
│───│─────────────────────│────────────────────│───────────│────────│
│ # │ POLICY              │ RULE               │ RESOURCE  │ RESULT │
│───│─────────────────────│────────────────────│───────────│────────│
│ 1 │ disallow-latest-tag │ require-image-tag  │ myapp-pod │ Pass   │
│ 2 │ disallow-latest-tag │ validate-image-tag │ myapp-pod │ Pass   │
│───│─────────────────────│────────────────────│───────────│────────│
```
