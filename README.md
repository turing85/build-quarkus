[![GitHub license file](https://img.shields.io/github/license/turing85/build-quarkus)](https://github.com/turing85/build-quarkus/blob/main/LICENSE)

# Github action build Quarkus applications

This action builds a Quarkus application with maven.

## Components
This action is a composite action, it uses the following actions:

<table>
  <tr>
    <th>Action</th>
  </tr>

  <tr>
  <td>

[`actions/checkout@v4`][checkout]

  </td>
  </tr>

  <tr>
  <td>

[`actions/upload-artifact@v4`][upload]

  </td>
  </tr>

  <tr>
  <td>

[`graalvm/setup-graalvm@v1`][graalvm]

  </td>
  </tr>

</table>


## Prerequisite

The project needs to have a [maven wrapper (`maven.apache.org`)](https://maven.apache.org/wrapper/) present.

## What it does

The current project is checked out, the specified version of GraalVM is setup (with a corresponding maven dependency cache), and `./mvnw` is executed.

The base command executed is:

```bash
./mvnw
  --batch \
  -- color always \
  ${{ inputs.additional-maven-opts }} \
  ${{ inputs.maven-targets }}
```

The default target executed is `verify`, and no additional arguments are passed to the maven command.
To customize this commands, see section [Inputs](#Inputs).

The following artifacts are created. 
Take special note When the artifacts are created.

<table>
  <tr>
  <th>name</th><th>content</th><th>retention</th>
  </tr>

  <tr>
  <th colspan="3" align="center">Always created</th>
  </tr>

  <tr>
  <td>

`${{ inputs.test-report-name }}`
  </td>
  <td>

`'**/target/**/TEST*.xml'`
  </td>

  <td>2 days</td>
  </tr>

  <tr>
  <th colspan="3" align="center">On non-native builds</th>
  </tr>

  <tr>
  <td>

`maven-state`
  </td>
  <td>

`'**/target/maven-*'`
  </td>

  <td>2 days</td>
  </tr>

  <tr>
  <td>

`compiled-classes`
  </td>
  <td>

`'**/target/*classes'`
  </td>

  <td>2 days</td>
  </tr>

  <tr>
  <td>

`jars`
  </td>
  <td>

`'**/target/*.jar'`
  </td>

  <td>2 days</td>
  </tr>

  <tr>
  <td>

`fast-jar`
  </td>
  <td>

`'target/quarkus-app'`
  </td>

  <td>2 days</td>
  </tr>

  <tr>
  <th colspan="3" align="center">On native builds</th>
  </tr>

  <tr>
  <td>

`executable`
  </td>
  <td>

`target/*-runner`<br>
`target/*.so`
  </td>

  <td>2 days</td>
  </tr>
</table>

The build will fail if any artifact that should be created, is empty.

## Inputs

<table>
  <tr>
  <th>Name</th><th>semantics</th><th>Required?</th><th>default</th>
  </tr>

  <tr>
  <th colspan="4" align="center">General Inputs</th>
  </tr> 

  <tr>
  <td>

`graalvm-distribution`
  </td>
  <td>The GraalVM Distribution to used.</td>
  <td>✅</td>
  <td>

`mandrel`
  </td>
  </tr>

  <tr>
  <td>

`graalvm-version`
  </td>
  <td>The version of the GraalVM Distribution to used.</td>
  <td>✅</td>
  <td>

`mandrel-23.1.2.0-Final`
  </td>
  </tr>

  <tr>
  <td>

`java-version`
  </td>
  <td>The Java version of the GraalVM Distribution.</td>
  <td>✅</td>
  <td>

`'21'`
  </td>
  </tr>

  <tr>
  <td>

`additional-maven-opts`
  </td>
  <td>Additional options passed to the maven command.</td>
  <td>❌</td>
  <td>

  </td>
  </tr>

  <tr>
  <td>

`maven-targets`
  </td>
  <td>The maven target(s) to execute.</td>
  <td>✅</td>
  <td>

`verify`
  </td>
  <tr>
  <td>

`is-native`
  </td>
  <td>
Whether this build is a native build.

This determines which artifacts are created by this build.
  </td>
  <td>✅</td>
  <td>

`'false'`
  </td>
  </tr>

  <tr>
  <td>

`test-report-name`
  </td>
  <td>The name for the test report artifact.</td>
  <td>✅</td>
  <td>

`test-report-jvm`
  </td>
  </tr>

</table>

## Outputs
None.

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/turing85"><img src="https://avatars.githubusercontent.com/u/32584495?v=4?s=100" width="100px;" alt="Marco Bungart"/><br /><sub><b>Marco Bungart</b></sub></a><br /><a href="https://github.com/turing85/build-quarkus/commits?author=turing85" title="Code">💻</a> <a href="#maintenance-turing85" title="Maintenance">🚧</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors][all-contributors] specification. Contributions of any kind welcome!

## License

This project is licensed under the [Apache License 2.0][apacheLicense]. The license file can be found [here][license].

[checkout]: https://github.com/actions/checkout

[graalvm]: https://github.com/graalvm/setup-graalvm

[download]: https://github.com/actions/download-artifact

[upload]: https://github.com/actions/upload-artifact

[all-contributors]: https://github.com/all-contributors/all-contributors

[apacheLicense]: http://www.apache.org/licenses/LICENSE-2.0

[license]: https://github.com/turing85/build-quarkus/blob/main/LICENSE