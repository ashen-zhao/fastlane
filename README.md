fastlane documentation
================
# Installation

Make sure you have the latest version of the Xcode command line tools installed:

```
xcode-select --install
```

## Choose your installation method:

<table width="100%" >
<tr>
<th width="33%"><a href="http://brew.sh">Homebrew</a></th>
<th width="33%">Installer Script</th>
<th width="33%">RubyGems</th>
</tr>
<tr>
<td width="33%" align="center">macOS</td>
<td width="33%" align="center">macOS</td>
<td width="33%" align="center">macOS or Linux with Ruby 2.0.0 or above</td>
</tr>
<tr>
<td width="33%"><code>brew cask install fastlane</code></td>
<td width="33%"><a href="https://download.fastlane.tools">Download the zip file</a>. Then double click on the <code>install</code> script (or run it in a terminal window).</td>
<td width="33%"><code>sudo gem install fastlane -NV</code></td>
</tr>
</table>

# Available Actions
## iOS
### ios test
```
fastlane ios test
```
Runs all the tests
### ios sethost
```
fastlane ios sethost
```

### ios testhost
```
fastlane ios testhost
```

### ios devhost
```
fastlane ios devhost
```

### ios releasehost
```
fastlane ios releasehost
```

### ios build
```
fastlane ios build
```

### ios to_pgyer
```
fastlane ios to_pgyer
```
上传到蒲公英
### ios to_pgyer_dev
```
fastlane ios to_pgyer_dev
```
开发环境上传到蒲公英
### ios to_pgyer_test
```
fastlane ios to_pgyer_test
```
测试环境上传到蒲公英
### ios to_pgyer_release
```
fastlane ios to_pgyer_release
```
线上环境上传到蒲公英
### ios to_appstore
```
fastlane ios to_appstore
```
上传到iTC

----

This README.md is auto-generated and will be re-generated every time [fastlane](https://fastlane.tools) is run.
More information about fastlane can be found on [fastlane.tools](https://fastlane.tools).
The documentation of fastlane can be found on [docs.fastlane.tools](https://docs.fastlane.tools).
