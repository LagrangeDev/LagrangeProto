# LagrangeProto

Protobuf files extracted from [Lagrange.Core](https://github.com/LagrangeDev/Lagrange.Core) and [LagrangeV2](https://github.com/LagrangeDev/LagrangeV2)

# Usage

## Use buf (recommend)

### install buf

#### macos and linux
```bash
brew install bufbuild/buf/buf
```

#### windows
```bash
scoop install buf
```

#### all
```bash
npm install @bufbuild/buf
```

### add buf.gen.yaml ([docs](https://buf.build/docs/configuration/v2/buf-gen-yaml/))
```yaml
# buf.gen.yaml
version: v2
clean: true
managed:
  # overwrite the fields defined in the proto file, such as go_package_prefix, to make the codegen more flexible
  enabled: true
  override:
    - file_option: go_package_prefix
      value: github.com/LagrangeDev/LagrangeGo/pb
plugins:
  # if use remote plugin, more plugin can found in https://buf.build/plugins
  - remote: buf.build/protocolbuffers/go
    out: gen
    opt: paths=source_relative
  # if use local plugin
  - local: protoc-gen-go
    out: gen
inputs:
  # if use git submodule
  - directory: proto
  # if use remote git repo
  - git_repo: https://github.com/LagrangeDev/LagrangeProto.git
    branch: master
    depth: 1
    subdir: proto
    paths:
      - common/v2
      - login/v2
      - message/v2
      - notify/v2
      - service/v2
      - service/highway/v2
      - system/v2
```

the most concise example
```yaml
# buf.gen.yaml
version: v2
clean: true
managed:
  enabled: true
  override:
    - file_option: go_package_prefix
      value: github.com/LagrangeDev/LagrangeGo/pb
plugins:
  - remote: buf.build/protocolbuffers/go
    out: gen
    opt: paths=source_relative
inputs:
  - git_repo: https://github.com/LagrangeDev/LagrangeProto.git
    branch: v2
    depth: 1
    subdir: proto
    paths:
      - common/v2
      - login/v2
      - message/v2
      - notify/v2
      - service/v2
      - service/highway/v2
      - system/v2
```

### Generate code

```bash
buf generate
```
