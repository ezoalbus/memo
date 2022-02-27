# 環境設定（Windows編）

## Python
- Pythonのインストール
    - Windows版Python: https://www.python.org/downloads/windows/
    - あるいは、miniconda
- パッケージのインストール
    - poetry: https://python-poetry.org/docs/
    - python全般: flake8, ...
    - data science系: numpy, pandas, sklearn,...
    - 【備考】VS Codeでのpipによるインストール中に"WARNING: Failed to write executable - trying to use .deleteme logic"といったエラーが出る場合は以下のいずれかを実施する
      - cmdかPSを管理者で実行してインストール
      - VS Codeを管理者権限で実行
      - "C:\Python3x" （xは数字）フォルダのプロパティでユーザー追加（権限付与）を行う


## VS Code
- VS Codeをインストール
- 拡張機能をインストール
    - Python (ms-python.python) by Microsoft
    - Vim (vscodevim)
    - Remote - WSL
    - Docker
    - Markdown All in One
    - Marp for VS Code

- 設定
    - 自動保存
    - 以下の設定を加える。
        - 1つ目の設定により、"j"を2回打つことでノーマルモードに戻れる。
        - 2つ目は検索結果のハイライト表示をonにする。

        ``` json
        "vim.insertModeKeyBindings": [
            {
                "before": ["j", "j"],
                "after": ["<Esc>"]
            }
        ],

        "vim.hlsearch": true
        ```
    - linter
        - 「Python > Linting: Flake8 Enabled」の下にある「Whether to lint Python files using flake8」をチェック
        - 「Python > Linting: Pylint Enabled」の下にある「Whether to lint Python files using pylint」のチェックを外す
      
      
## 開発の要領
- Flake8の赤波線が見づらい場合は、Alt + F8 でインライン表示できる
