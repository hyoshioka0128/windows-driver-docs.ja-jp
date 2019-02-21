---
title: 例 3 の一般的な Start コマンド
description: 例 3 の一般的な Start コマンド
ms.assetid: a0e8580d-b841-4077-82f5-6aaef57b0ff7
keywords:
- トレース セッションを開始、WDK
- コマンドを開始します。
- -コマンドの開始
- トレース セッションの起動
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d05d4f395db9c6f86c1b98cf8837d35f4af301a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553608"
---
# <a name="example-3-typical-start-command"></a>例 3: 一般的な Start コマンド

## <span id="ddk_typical_start_command_tools"></span><span id="DDK_TYPICAL_START_COMMAND_TOOLS"></span>

次のコマンド形式は通常、トレース セッションの開始に使用されます。

```
tracelog -start MyTrace -guid MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

コマンドは、"MyTrace"という名前のトレース セッションを開始します。

使用して、 **- guid** MyProvider.guid ファイル、プロバイダーのだけを含む単純なテキスト ファイルを指定するパラメーターは、GUID を制御します。 使用することも、[制御 GUID ファイル](control-guid-file.md)、Tracedrv.ctl などの **- guid**パラメーター。 含まれている Tracedrv.ctl、 [TraceDrv](https://go.microsoft.com/fwlink/p/?linkid=256197)サンプル。

コマンドが含まれています、 **-f**イベント トレース ログ ファイルの場所と名前を指定するパラメーター。 含まれています、 **-フラグ**フラグ セットを指定するパラメーター、および **-レベル**レベルの設定を指定するパラメーター。 これらのパラメーターを省略できますが、一部のトレース プロバイダー メッセージは生成されず、トレース フラグまたはレベルを設定していない場合。
