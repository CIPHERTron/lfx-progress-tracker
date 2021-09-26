## Week 1 - (Sep 10 - Sep 17)

Tasks:
1. Use Kyverno as an end user to know how it works
2. Set-up local development environment for kyverno
3. Use kyverno cli and the `test` and `apply` commands
4. Explore the [kyverno/policies](https://kyverno/policies) repo and the sample policies

Challenges faced:
1. Error in the `Makefile` whose actual reason was my Go's local dev setup
  Now, my local workspace looks similar to this:
  ```
  $ echo $GOPATH
  /home/ciphertron/go
  ```
  
  ```sh
  bin/
    gocode-gomod                 # command executable
    gopkgs                       # command executable
    gopls                        # command executable
    gotests                      # command executable
  src/
    github.com/
              CIPHERTron/
                        kyverno  # github.com/CIPHERTron/kyverno repository
                        policies # github.com/CIPHERTron/policies repository
  ```

2. Resetting my Go workspce solved the above error and now, I was able to execute the `make` commands but I was still facing another error i.e:
  ```
  build command-line-arguments: cannot load embed: malformed module path "embed": missing dot in first path element
  make: *** [Makefile: docker-build-kyverno-local] Error 1
  ```
  
  This was happening because the `embed` feature was added in go version 1.16 and my go version was 1.13.4.
  Thus I had to update it from `go version 1.13.4` to `go version 1.17.1` and everything seems to work perfectly fine.

3. Since my local dev wasn't setup, I installed kyverno cli using the latest release from [here](https://github.com/kyverno/kyverno/releases) and started playing around it.
