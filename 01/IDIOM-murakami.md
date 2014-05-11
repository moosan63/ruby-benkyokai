# アジェンダ

1. 高機能REPL `pry`の紹介
1. Rubyでよく使われるイディオムたち

# 高機能REPL `pry`の紹介

まずイディオムの前に軽く便利なgemを紹介します。

## pryとは

gemで提供されるirbに代わるRubyの高機能REPL
Ruby開発者のMatzもpry使おうとおすすめしてます。

github: https://github.com/pry/pry

## install

```bash
gem install pry pry-doc
```

おわり

## irbとの違い、便利な機能

* 式が見やすくなる

式が色付けされたりインデントされて見やすくなります。
irbでやるにはgemが必要だったりします。

* shellが使える

pry上でshellを使うことができます。

```bash
[1] pry(main)> .ls
Applications   Desktop  
```

* 強力なデバッグ機能

ここからがpryの本領

`show-method`でメソッドの実装が見られる

```bash
[1] pry(main)> show-method Array#sample

From: array.c (C Method):
Owner: Array
Visibility: public
Number of lines: 103

static VALUE
rb_ary_sample(int argc, VALUE *argv, VALUE ary)
{
    VALUE nv, result;
    VALUE opts, randgen = rb_cRandom;
    long n, len, i, j, k, idx[10];
    long rnds[numberof(idx)];

    if (OPTHASH_GIVEN_P(opts)) {
        VALUE rnd;
        ID keyword_ids[1];

        keyword_ids[0] = id_random;
        rb_get_kwargs(opts, keyword_ids, 0, 1, &rnd);
        if (rnd != Qundef) {
            randgen = rnd;
        }
    }
... 略
```

`binding.pry`でブレークポイントを設定出来る

```ruby
require 'pry'
puts "hoge"
binding.pry
puts "fuga"
```

```bash
% ruby test.rb
hoge

From: /Users/moosan63/Works/others/test.rb @ line 3 :

    1: require 'pry'
    2: puts "hoge"
 => 3: binding.pry
    4: puts "fuga"

[1] pry(main)> exit
fuga
```


* その他様々な機能
riをpry上で参照できたり、pry上のlsで現在のフレーム上で有効なオブジェクトを表示できたりとかいろいろ便利な機能がありますが、今日はpryの発表ではないのであとは

http://morizyun.github.io/blog/pry-command-rails-ruby/

この辺を参照してください。





