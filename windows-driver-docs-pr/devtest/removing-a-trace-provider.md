---
title: トレース プロバイダーの削除
description: トレース プロバイダーの削除
ms.assetid: 3ea38137-9196-46a6-8cb5-04722cd43086
keywords:
- トレース プロバイダー WDK
- プロバイダーの WDK ソフトウェア トレース
- WDK、プロバイダーのセッションをトレースします。
- トレース プロバイダーを削除します。
- トレース プロバイダーを無効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 870f5b3c071c51123331ca58c502895f300899bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360734"
---
# <a name="removing-a-trace-provider"></a>トレース プロバイダーの削除


Traceview でウィンドウを使用すると、削除または実行中のトレース セッションからのトレース プロバイダーを無効にすることはできません。 ただし、traceview では、それが開始する前に、トレース セッションを作成するときにプロバイダーを削除することができます。

トレース セッションを作成するときに、次の手順を使用して、トレース プロバイダーを削除します。

1.  **ファイル** メニューのをクリックして**Create New Log Session**します。

2.  **名前**一覧で、削除するプロバイダーをクリックします。

3.  クリックして**プロバイダーを削除する**します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview では、コマンド プロンプト ウィンドウで、次のコマンドを入力して開始したセッションのトレース プロバイダーを無効にすることもできます。

```
traceview -disable SessionName -guid {#GUID | GUIDFile}
```

ただし、このコマンドは、トレース セッションを停止する traceview でを実行します。 続けるを使用して、**traceview で-スタート * * * SessionName*トレース セッションを再起動するコマンド。 詳細については、次を参照してください。 [ **traceview で管理コマンド**](traceview-control-commands.md)します。

 

 





