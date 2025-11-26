# Gemini CLI の使い方

提供された情報に基づき、このコマンドラインインターフェース（CLI）は、主に「エージェント」の作成、実行、評価、および提供を行うためのツールセットであると推測されます。

## 主なコマンド

### 1. `create`

新しいエージェントアプリケーションの雛形を作成します。

```bash
adk create <app_name> [OPTIONS]
```

**引数:**

-   `app_name`: 作成するエージェントのフォルダパス。

**オプション:**

-   `--model`: 使用するモデル名。
-   `--api-key`: Google APIキー。
-   `--project`: Google Cloudプロジェクト名。
-   `--region`: Google Cloudリージョン。

### 2. `run`

エージェントを対話的に実行します。

```bash
adk run <agent_path> [OPTIONS]
```

**引数:**

-   `agent_path`: 実行するエージェントのソースコードフォルダへのパス。

**オプション:**

-   `--save-session`: 終了時にセッションを保存します。
-   `--session-id <id>`: 保存するセッションのIDを指定します。
-   `--replay <file_path>`: 指定したJSONファイルからセッションを再現します。
-   `--resume <file_path>`: 保存されたセッションファイルから再開します。

### 3. `eval`

エージェントを評価セットを用いて評価します。

```bash
adk eval <agent_module_file_path> <eval_set_file_path> <config_file_path> [OPTIONS]
```

**引数:**

-   `agent_module_file_path`: エージェントモジュールのパス（例: `path/to/agent/__init__.py`）。
-   `eval_set_file_path`: 評価セットファイルのパス。複数指定可能です。
-   `config_file_path`: 設定ファイルのパス。

**オプション:**

-   `--print-detailed-results`: 詳細な評価結果をコンソールに出力します。

### 4. `api_server`

エージェントをFastAPIサーバーとして起動します。

```bash
adk api_server <agents_dir> [OPTIONS]
```

**引数:**

-   `agents_dir`: 各サブディレクトリが単一のエージェントである、エージェントのディレクトリ。

**オプション:**

-   `--host <ip>`: サーバーが待機するホストIP（デフォルト: `127.0.0.1`）。
-   `--port <port>`: ポート番号（デフォルト: `8000`）。
-   `--log-level <level>`: ログレベル（`INFO`, `DEBUG`など）。
-   `--allow-origins <origin>`: 許可するオリジンのリスト。
-   `--session-service-uri <uri>`: セッションサービスのURI。
-   `--artifact-service-uri <uri>`: アーティファクトサービスのURI。
-   `--reload`: コード変更時にサーバーをリロードします（デフォルト: `True`）。

---

## その他のツール

### 音声文字起こしCLI

Whisperモデルを利用して音声ファイルを文字に起こす機能も含まれているようです。

**コマンド例:**

```bash
whisper <audio_file> --model small --language Japanese
```

**主な引数・オプション:**

-   `audio`: 文字起こしする音声ファイル（複数指定可）。
-   `--model`: 使用するWhisperモデル名（`tiny`, `base`, `small`, `medium`, `large`など）。
-   `--output_dir, -o`: 出力ディレクトリ。
-   `--output_format, -f`: 出力形式（`txt`, `vtt`, `srt`, `json`など）。
-   `--language`: 音声ファイルの話言語。
-   `--task`: `transcribe`（文字起こし）または`translate`（英語へ翻訳）。
