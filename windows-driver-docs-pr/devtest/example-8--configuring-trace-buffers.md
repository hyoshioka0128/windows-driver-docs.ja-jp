---
title: 例 8 トレース バッファーの構成
description: 例 8 トレース バッファーの構成
ms.assetid: 7bcc076c-6feb-4660-88d7-dc4206b53dce
keywords:
- トレース バッファー WDK
- バッファーの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeacc40a9306854311cdbb6cefa93d9142553f94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378832"
---
# <a name="example-8-configuring-trace-buffers"></a>例 8:トレース バッファーの構成


## <span id="ddk_configuring_trace_buffers_tools"></span><span id="DDK_CONFIGURING_TRACE_BUFFERS_TOOLS"></span>


次のコマンドは、トレース ログ セッションを開始し、セッションのバッファーをカスタマイズします。

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -flag 2 -level ffff -b 128 -min 10 -max 30
```

コマンドは、"MyTrace"という名前のセッションを開始します。 使用して、 **- guid**プロバイダー ファイルを指定するパラメーター、および **-f**トレース ログの場所と名前を指定するパラメーター。

使用して、 **-フラグ**フラグ値を 2 に設定するパラメーター、および **-レベル**FFFF で、すべての使用可能なトレース メッセージを生成するレベルの値を設定するパラメーター。 これらの設定は、プロバイダーに固有です。

このコマンドを使用して、高いメッセージ率に合わせて、 **-b**パラメーター 128 kb は、各バッファーのサイズを増やす、**最小**パラメーターを 10、および、するバッファーの最小数を増やす **-最大**パラメーターを 30 にバッファーの最大数を増やします。

応答では、トレース ログは、トレース セッションを開始し、セッションのプロパティの一部を表示します。 コマンドによって設定されたプロパティを識別しやすく、太字で表示されます。

```
Logger Started...
Enabling trace to logger 2
Operation Status:       0L      The operation completed successfully.

Logger Name:            MyTrace
Logger Id:              2
Logger Thread Id:       00000D7C
Buffer Size:            128 Kb
Maximum Buffers:        30
Minimum Buffers:        10
Number of Buffers:      10
Free Buffers:           9
Buffers Written:        1
Events Lost:            0
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Enabled tracing:        0x00000002
Log Filename:           d:\traces\testtrace.etl 
```

注意することは常に、**失われたイベント**トレース セッションのプロパティの一覧でカウンター。 イベント、失われる場合は、増加のバッファー容量 (サイズ、番号、またはその両方) を持つトレース セッションを再実行します。 トレース セッションのプロパティを表示する使用**tracelog-l**または **tracelog q * * * SessionName*します。

 

 





