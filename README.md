# 第8章　実践ハンズオン❷　ひらがな変換アプリを開発

以下の解説文はChatGPTに作成してもらった。

↓

各ファイルの内容を解析し、それぞれの役割について解説します。

### 1. app_notifier_provider.dart
概要: 
app_notifier_provider.dart はアプリの状態管理を行う AppNotifier クラスを定義しています。このクラスは、ユーザーが入力した文章をサーバーに送信し、ひらがなに変換された結果を受け取って状態を更新します。

詳細:
build() メソッドで初期状態を Input に設定しています。
reset() メソッドで状態をリセットして、再度 Input 状態に戻す機能があります。
convert() メソッドでは、ユーザーの入力を API に送信し、結果を受け取った後に Data 状態に更新します。API 呼び出しには http パッケージを使い、POST リクエストを送信します。


### 2. app_notifier_provider.g.dart
概要: 
このファイルは Riverpod のジェネレーターによって自動生成されるファイルで、AppNotifier クラスを Provider として登録しています。

詳細: 
このファイルには appNotifierProvider という AutoDisposeNotifierProvider が定義されており、AppNotifier のインスタンスを提供します。開発者はこのプロバイダを利用してアプリの状態管理を行えます。


### 3. app_state.dart
概要: 
アプリケーションの状態を表すクラスが定義されています。Input, Loading, Data という異なる状態が存在し、それぞれが AppState クラスを継承しています。

詳細:
Input: 初期状態で、ユーザーの入力を待機している状態。
Loading: 入力データがサーバーで処理されている状態。
Data: サーバーから結果が返ってきた後の状態で、ひらがな変換後の文を保持しています。


### 4. convert_result.dart
概要: 
変換結果を表示するウィジェット ConvertResult が定義されています。

詳細: 
コンストラクタで受け取ったひらがな変換後の文章を Text ウィジェットで表示します。


### 5. data.dart
概要: 
API リクエストおよびレスポンスデータのモデルが定義されています。

詳細:
Request クラス: sentence（変換したい文章）と appId（APIキー）を含むリクエストモデル。
Response クラス: converted プロパティで変換結果を保持し、サーバーからのレスポンスを表現します。


### 6. data.g.dart
概要: 
data.dart のモデルクラス用に自動生成されたコードが含まれています。

詳細: 
Request や Response の JSON シリアライズ・デシリアライズの関数が定義されており、データを JSON 形式に変換したり、JSON からデータを再構築するために使用されます。


### 7. input_form.dart
概要: 
ユーザーが文章を入力するフォームを提供するウィジェット InputForm が定義されています。

詳細:
TextEditingController を使ってユーザー入力を管理し、ボタン押下時に convert メソッドを呼び出します。
Provider を使って AppNotifier にアクセスし、ユーザーの入力を処理することでアプリの状態を更新します。


### 8. loading_indicator.dart
概要: 
ローディング中に表示するウィジェット LoadingIndicator が定義されています。

詳細: 
CircularProgressIndicator を使ってアニメーション表示を行い、処理待機中のインジケータとして機能します。


### 9. main.dart
概要: 
アプリのエントリーポイントを定義しています。ProviderScope を使ってプロバイダー管理を有効にし、アプリの全体構造を構築します。

詳細:
MyApp クラス: MaterialApp を使い、アプリのテーマやホーム画面を設定します。
HomeScreen クラス: アプリのメイン画面で、状態に応じて異なるウィジェット（LoadingIndicator, InputForm, ConvertResult）を表示します。 ​
