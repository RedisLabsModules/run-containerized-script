[![GitHub release](https://img.shields.io/github/release/RedisLabsModules/run-containerized-script.svg?style=flat-square)](https://github.com/RedisLabsModules/run-containerized-script/releases/latest)

## About

A reusable GitHub Action that executes a bash script inside a container with the current working directory (CWD) mounted. This action simplifies workflows by enabling script execution in an isolated containerized environment while maintaining access to the local project files

This allows running [`actions/checkout`](https://github.com/actions/checkout), [`actions/download-artifact`](https://github.com/actions/download-artifact), [`actions/upload-artifact`](https://github.com/actions/upload-artifact), and other actions outside of the container's context.

___

* [Usage](#usage)
* [inputs](#inputs)

## Usage

```yaml
    steps:
      - name: Checkout Foo repository
        uses: actions/checkout@v4
      - name: Build inside of container
        uses: RedisLabsModules/run-containerized-script@v1
        with:
          image: docker.io/foo/foo-container:x.y.z
          args: |
            echo "::group::Building Foo"
            cd foo-folder
            make
            echo "::endgroup::"
            tar -czf foo-artifacts.tar.gz
      - name: Upload Foo artifact
        uses: actions/upload-artifact@v4
        with:
          name: foo-artifacts
          path: |
            foo-folder/foo-artifacts.tar.gz
```

## inputs

The following inputs can be used as `step.with` keys:

| Name               | Type        | Description                                                                                                                                                                       |
|--------------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `image`            | String      | The container image to use.                                                                                                                                                       |
| `args`             | String      | The script to invoke inside of the container.                                                                                                                                     |
