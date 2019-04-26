---
title: 例 7 トレース メッセージのプレフィックスをカスタマイズします。
description: 例 7 トレース メッセージのプレフィックスをカスタマイズします。
ms.assetid: 75beccef-fd0b-4a4f-9ea2-11940b5baddf
keywords:
- Tracefmt WDK、プレフィックス
- WDK Tracefmt プレフィックス
- トレース メッセージのプレフィックス WDK Tracefmt
- カスタムのトレース メッセージのプレフィックス WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ef8258a2b8252951b6fd602a080af8d5cb7bb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352898"
---
# <a name="example-7-customizing-the-trace-message-prefix"></a>例 7:トレース メッセージのプレフィックスのカスタマイズ


各トレース メッセージの先頭が、[トレース メッセージのプレフィックス](trace-message-prefix.md)トレース メッセージに関するデータで構成されます。 トレースのトレース メッセージのプレフィックスの形式が格納されている\_形式\_%path% 環境変数のプレフィックス。 環境変数の値を変更すると、最もわかりやすい形式で、トレース メッセージに関する必要なデータを表示するトレース メッセージのプレフィックスをカスタマイズできます。 既定のトレース メッセージのプレフィックスで変数とトレース メッセージのプレフィックスに使用できるすべての変数については、トレース メッセージのプレフィックスのトピックで説明します。

次の表示では、既定のトレース メッセージのプレフィックスを示します。 トレース メッセージは、Tracedrv、Windows Driver Kit (WDK) でのトレースが有効なサンプル ドライバーによって生成されました。

```
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]IOCTL = 1
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]Hello, 1 Hi
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]Hello, 2 Hi
...
```

既定のプレフィックスの形式は次のとおりです。

```
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

これは、次のデータを表します。

```
[CPUNumber]ProcessID.ThreadID::SystemTime [MessageGUIDFriendlyName]
```

場所、 *MessageGUIDFriendlyName*ディレクトリの名前を既定では、トレース プロバイダーが構築されたのです。

新しいトレース メッセージのプレフィックスを作成するには、使用、**設定**トレース % の値にリセットするコマンド\_形式\_%path% 環境変数のプレフィックス。 以下に例を示します。

```
set TRACE_FORMAT_PREFIX=%2!s!: %!FUNC!: %8!04x!.%3!04x!: %4!s!:
```

このコマンドは、トレース メッセージのプレフィックスが次の形式を設定します。

```
SourceFile_LineNumber: FunctionName: ProcessID.ThreadID: SystemTime 
```

その結果、Tracefmt 出力は、次の表示に示すように、新しいトレース メッセージのプレフィックスを使用します。

```
tracedrv_c258: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  IOCTL = 1
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 1 Hi
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 2 Hi
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 3 Hi
```

...

**注**  コマンド ライン パラメーターの変数で、パーセントが表すをシンボル、コマンドまたはバッチ ファイルでトレースのプレフィックスを設定する場合、は、プレフィックス変数に連続する 2 つのパーセント記号を使用します。 たとえば、プレフィックスのシステム時刻は、次のように入力します。 **%%1**します。

 

 

 





