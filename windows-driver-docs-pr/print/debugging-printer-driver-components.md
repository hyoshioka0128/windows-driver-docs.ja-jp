---
title: プリンター ドライバー コンポーネントのデバッグ
description: プリンター ドライバー コンポーネントのデバッグ
ms.assetid: 550cc8fe-5520-4521-8c4e-9c8c80521357
keywords:
- ドライバー WDK プリンターのデバッグ
- プリンター ドライバー WDK、デバッグ
- ユーザー モード デバッグの WDK プリンター
- WDK のプリンターをマクロ
- グローバル変数 WDK のデバッグ
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2fbe2ad35d80877ba3ebe3c1ef94c1bb581f3483
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572741"
---
# <a name="debugging-printer-driver-components"></a>プリンター ドライバー コンポーネントのデバッグ

プリンター ドライバーのプラグインでレンダリングまたはユーザー インターフェイスのプラグインを開発している場合は、これらのコンポーネントにデバッグ メッセージを有効にできます。 前述のデバッグのグローバル変数セクションでは、デバッガー ウィンドウに表示されるメッセージの詳細レベルを制御するのにデバッグのグローバル変数を使用できます。

メッセージ マクロのデバッグのセクションで説明したマクロを使用すると、さまざまな条件下で、デバッガー ウィンドウにメッセージを送信します。 さらに、このセクションでは、Microsoft のユニバーサル プリンター ドライバー (Unidrv) または PostScript プリンター ドライバー (Pscript) レンダラーにデバッグ メッセージを有効にする情報を使用できますがチェックされるときは、これらの Dll のビルドします。

次の 2 つのセクションでは、ユーザー モード ドライバーと一般的なデバッグのヒントをデバッグするための手順が含まれます。

## <a name="preparing-for-user-mode-debugging"></a>ユーザー モードのデバッグの準備

プリンター ドライバーとそのコンポーネントのデバッグを開始するには。

1. 最新のデバッグ ツールをインストールします。 参照してください[Windows 用デバッグ ツールをダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)

1. インストールから正しいシンボル[Windows シンボル パッケージ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)

> [!NOTE]
> 最新バージョンのデバッガーを使用することが非常に重要です。

デバッグしているコンポーネントのみのチェック ビルドをインストールすることをお勧めします。 通常、対応するチェック ビルドで、次の出荷版バイナリを置き換えますは。

- 問い合わせて
- Unidrvui.dll
- Unires.dll

Oemuni サンプルまたはデバッグしているプリンター ドライバーのチェック ビルドをインストールすることも必要があります。 全体のチェック ビルド システムでは、インストールではなく、このアプローチを使用する利点は、システム全体を低下は発生しないことです。

## <a name="starting-a-user-mode-debugging-session"></a>ユーザー モードのデバッグ セッションを開始します。

ユーザー モードのデバッグを開始する、**ファイル**で Windbg デバッガーを選択します] メニューの [**プロセスにアタッチする**します。 デバッガーをアタッチするプロセスは、デバッグしようとしているシナリオによって異なります。 プリンター ドライバーには、アプリケーションの印刷するか、デバッガーをアタッチまたは、スプーラーに (Spoolsv.exe) を処理する必要があります。 印刷アプリケーションでは、スプーラーのプロセスがレンダリング モジュールを読み込み中に、構成/ユーザー インターフェイスのモジュールが読み込まれることに留意してください。 ただし、の違いがあります"ファイル:"、スプールが行われないと、その結果、レンダリング モジュールは、印刷アプリケーションにより読み込まれることはもを印刷します。 したがって正しいプロセスにアタッチすることを確認する必要があります。

> [!NOTE]
> ユーザー モード デバッグは、2 つの個別のマシンは必要ありません。

次の手順が揃って Oemuni サンプルをデバッグする準備ができています。

1. Oemuni サンプルをインストール、"ファイル:"ポート。
1. クリックしてワードパット アプリケーションを起動、**開始** メニューの 選択**すべてのプログラム**選択**アクセサリ**、し を選択**ワードパッド**.
1. WinDbg で**ファイル**メニューの **プロセスにアタッチする**します。 使用可能なプロセスの一覧で選択**WordPad.exe**します。
1. ワードパッドの印刷ジョブを開始します。 Oemuni サンプルをデバッグする準備が整いました。

GiDebugLevel 変数の有効化して詳細なデバッグを有効にすることができます。 既定値は、あることを示す警告を 3 には。 かどうか 1 を設定することを示します詳細。 問い合わせてで後者の値を設定するには、デバッガーで、次のコマンドを入力します。

```cmd
> ed unidrv!giDebugLevel 1
```

Oemuni サンプルを実行しているときに、同じデバッグ変数も適用されます、そのため、次のコマンドを入力する詳細なデバッグを有効にします。

```cmd
> ed oemuni!giDebugLevel 1
```

Oemuni サンプルに、独自のデバッグ ステートメントを追加することもできます。

デバッグ値の設定の詳細については、使用可能なコマンドについて説明し、ユーザー モードのデバッグを設定するために必要な手順について説明します WinDbg ドキュメントを参照してください。 WinDbg で、ドキュメントにアクセスする**ヘルプ**メニューの **内容**します。

## <a name="global-debug-variable"></a>デバッグ グローバル変数

GiDebugLevel グローバル変数は、その Debug.h と Debug.cpp ファイルで、Oemui と Oemuni サンプルで宣言されます。 によって giDebugLevel の値を変更できます。

- デバッガーでは、その値を変更します。
- プラグインでは、その値を再定義します。

GiDebugLevel は、次の値のいずれかに設定できます。

```cpp
#define DBG_VERBOSE 1
#define DBG_TERSE   2
#define DBG_WARNING 3
#define DBG_ERROR   4
#define DBG_RIP     5
```

## <a name="debug-message-macros"></a>デバッグ メッセージ マクロ

次のマクロは、デバッグ目的で使用されます。 操作は、デバッグ メッセージがどのコントロールが生成される giDebugLevel グローバル変数が特定の値に設定されている場合にのみいくつかの実行します。 マクロは、無料のビルド時に空白文字を展開します。 ここでは、その実行内容とそのパラメーターの簡単な説明です。

**ASSERT**(*単独*)

- 確認するかどうかのブール式*単独*は**TRUE**します。 そうでない場合、マクロは、ブレークポイントを強制します。

**ASSERTMSG**(*cond,* (*msg*))

- 確認するかどうかのブール式*単独*は**TRUE**します。 そうでない場合、マクロは、メッセージを表示します*msg、* し、ブレークポイントを強制します。

**ERR**((*msg*))

- メッセージが表示されます*msg*場合は、現在のデバッグ レベル&lt;= DBG\_エラー。 メッセージの形式です。

    ```cpp
    ERR filename (linenumber): msg
    ```

**RIP**((*msg*))

- メッセージが表示されます*msg*し、ブレークポイントを強制します。

**TERSE**((*msg*))

- メッセージが表示されます*msg*場合は、現在のデバッグ レベル&lt;= DBG\_小文字です。

**VERBOSE**((*msg*))

- メッセージが表示されます*msg*場合は、現在のデバッグ レベル&lt;= DBG\_詳細。

**WARNING**((*msg*))

- メッセージが表示されます*msg*場合は、現在のデバッグ レベル&lt;= DBG\_警告します。 メッセージの形式です。

    ```cpp
    WRN filename (linenumber): msg
    ```

注意してください、マクロのすべてを*msg*引数がこの引数を囲むかっこの追加のペアが必要です。 この要件を示す 2 つの例を次に示します。

```cpp
ASSERTMSG(x > 0, ("x is less than 0\n"));
```

```cpp
WARNING( ("App passed NULL pointer, ignoring...\n") );
```

マクロが含まれている、 *msg* Debug.h ヘッダーに Oemui と Oemuni サンプルによって引数が定義されます。