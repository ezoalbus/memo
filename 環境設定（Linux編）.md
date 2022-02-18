## タイピングをストレスフリーかつ高速に

以下，Linux(ArchLinux)を前提とする。

**大原則: 矢印キーとマウスは極力使わない**

  **→ Vimmerになろう**

### Vimをより快適に
1. ノーマルモードと挿入モードの切り替え
    - [候補] keymapの変更
        - CapsLockとEscを交換する
            - `cp /etc/X11/xinit/xinitrc ~/.xinitrc`
                - `~/.xinitrc` と `~/.xprofile`に以下を追記
                - `setxkbmap -option caps:escape`
            - [うまくいかなかった方法] Xの設定ファイル(`/etc/X11/xorg.conf.d/00-keyboard.conf`)を編集
                - 追記: `Option "XkbOptions" "caps:swapescape"`
    - [候補] Escキーではなく，Ctrl + C でノーマルモードに戻るようにする

2. 日本語キーボードを用いている場合，「入力メソッドの設定（Mozcを想定）」から以下のようにホットキーを設定し，Macっぽくする
    - 「入力メソッドをオンに」: Henkanmode (変換キー)，Hiraganakatakana (KANA)
    - 「入力メソッドをオフに」: Muhenkan (無変換キー)

3. 1.において，setxkbmapのバグ(?)が報告されているので，対処する。

``` sh
[hoge ~]$ setxkbmap -print
xkb_keymap {
	xkb_keycodes  { include "evdev+aliases(qwerty)"	};
	xkb_types     { include "complete"	};
	xkb_compat    { include "complete+japan"	};
	xkb_symbols   { include "pc+jp+inet(evdev)+capslock(escape)+terminate(ctrl_alt_bksp)"	};
	xkb_geometry  { include "pc(pc105)"	};
};
```

xkb_symbols の capslock(escape) がイカれているよう。

`/usr/share/X11/xkb/symbols/capslock`を開き，32行目辺りの記述を変更する。

Before:

```
partial hidden modifier_keys
xkb_symbols "escape" {
    key <CAPS> { [ Escape ] };
};
```

After:

```
partial hidden modifier_keys
xkb_symbols "escape" {
    key <CAPS> { [ Escape, Escape ] };
};
```

参考: [XKBでCapsLockをEscに割り当てる(Ubuntuでキーマッピング変更)](https://qiita.com/oyas/items/a39baab89908294516a7)

### VimをVSCodeで使う

Vimの拡張機能をインストールし，以下の設定を加える。1つ目の設定により，Escが遠い位置にある場合，"j"を2回打つことでノーマルモードに戻れる。2つ目は検索結果のハイライト表示をonにする。

``` json
  "vim.insertModeKeyBindings": [
      {
          "before": ["j", "j"],
          "after": ["<Esc>"]
      }
  ],

  "vim.hlsearch": true
```

参考: [VSCodeで始めるVim](https://qiita.com/jintz/items/d357478271179c90ffab)
