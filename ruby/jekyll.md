github.io를 활용하여 알고리즘 블로그를 만들어보려고 했다. 만들 때 참고한 자료는 다음과 같다.

[DN_Developer]([Jekyll을 사용하여 GitHub 블로그 만들기 :: DN_Developer](https://dnight.tistory.com/entry/Jekyll을-사용하여-GitHub-블로그-만들기?category=1056191) 

[frhyme]([jekyll을 설치하고 로컬에 블로그를 뛰우려고 합니다. : frhyme.code](https://frhyme.github.io/blog/install_jekyll_again/))



`rbenv install -l`을 입력하면 ruby의 최신 버전을 확인할 수 있있다.

```shell
$ rbenv install -l
2.6.10
2.7.6
3.0.4
3.1.2
jruby-9.3.6.0
mruby-3.1.0
picoruby-3.0.0
rbx-5.0
truffleruby-22.1.0
truffleruby+graalvm-22.1.0

Only latest stable releases for each Ruby implementation are shown.
Use 'rbenv install --list-all / -L' to show all local versions.

```

여기서 `rbenv install 3.1.2`를 입력하니 다음과 같은 오류가 나왔다.

```shell
/Library/Ruby/Gems/2.6.0/gems/ffi-1.15.5/lib/ffi/library.rb:275: [BUG] Bus Error at 0x00000001009b4000

ruby 2.6.8p205 (2021-07-07 revision 67951) [universal.arm64e-darwin21]
```

오류는 [Install 2.x, 3.x version of Ruby via rbenv on M1 Mac - DEV Community](https://dev.to/yasuhiron777/install-2x-3x-version-of-ruby-via-rbenv-on-m1-mac-3okn) 기사에서 소개하는 [Installation issues with Arm Mac (M1 Chip) · Discussion #1853 · rbenv/ruby-build · GitHub](https://github.com/rbenv/ruby-build/discussions/1853#discussioncomment-2146106) 를 통해 고칠 수 있었다.



과정은 다음과 같다.

1. `brew install openssl@1.1`을 입력한다.

2.  `vim ~/.zshrc`에서 다음을 설정한다. 참고로 설정하는 방법은 esc 버튼을 누르고 `i`를 입력하면 insert 모드로 바뀐다.
   
   ```shell
   # openssl
   export PATH="/opt/homebrew/opt/openssl@1.1/bin:$PATH"
   export LDFLAGS="-L/opt/homebrew/opt/openssl@1.1/lib"
   export CPPFLAGS="-I/opt/homebrew/opt/openssl@1.1/include"
   export PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@1.1/lib/pkgconfig"
   export RUBY_CONFIGURE_OPTS="--with-openssl-dir=/opt/homebrew/opt/openssl@1.1"
   ```
   
   다 적었다면 esc 버튼을 누른후 `:wq!`을 입력하여 빠져나온다.

3. `source ~/.zshrc`로 reload

4. 이후 다음을 입력하면 끝!
   
   ```shell
   CONFIGURE_OPTS=--with-openssl-dir=`brew --prefix openssl@1.1` CFLAGS="-Wno-error=implicit-function-declaration" rbenv install 3.1.0
   ```

그 이후에는 `rbenv versions` 를 확인해서 system으로 되어있는 걸 global로 바꿔주면 된다. 다음은 위에 언급한 블로그를 참고하여 설치를 완료하였다.

사실 맥을 이용하면 jekyll 설치는 별 오류없이 가볍게 끝날 줄 알았는데 m1 chip이라 오류가 날 줄 몰랐다 ^ㅡ^... 구글링을 통해서 겨우 해결했는데 혹시 나와 같은 오류가 나신다면 이 방법을 활용해 보시길!
