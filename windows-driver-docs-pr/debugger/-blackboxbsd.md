---
title: blackboxbsd
description: Blackboxbsd 拡張機能では、ブートの状態データ (BSD) のセカンダリ ブート情報が表示されます。
keywords:
- Windows デバッグ blackboxbsd
ms.author: windowsdriverdev
ms.date: 12/06/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- blackboxbsd
api_type:
- NA
ms.openlocfilehash: 7e877e718858133e836b2408cd38d31c68fb264a
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866515"
---
# <a name="blackboxbsd"></a>!blackboxbsd

**! Blackboxbsd**拡張機能では、カーネル モードのダンプ ファイルを利用可能なときにキャッシュされた Boot ステータス データ (BSD) 情報が表示されます。   バグチェックが発生し、常に使用できない時点で保存されたカーネル モードのダンプにキャッシュされたデータから情報が取得されます。

構文

```dbgcmd
!blackboxbsd  
```

## <a name="span-idparametersspanparameters"></a><span id="Parameters"></span>パラメーター
*None*   


## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ext.dll


## <a name="span-idremarksspanremarks"></a><span id="Remarks"></span>「解説」

ドライバー開発者は、ダンプ ファイルをセカンダリ ブート情報を追加できます。 ドライバー開発者 (と OS)、ダンプ ファイルにこの情報を追加するときに決定できます。 これはすべてカーネル モードのダンプ ファイルがセカンダリ ブート情報を含めることを意味します。 詳細については、次を参照してください。[バグ チェック理由コールバック ルーチンを記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-bug-check-callback-routine)します。

### <a name="example-command-output"></a>コマンドの出力の例

```dbgcmd
0: kd> !ext.blackboxbsd
Version: 136
Product type: 1

Auto advanced boot: FALSE
Advanced boot menu timeout: 30
Last boot succeeded: TRUE
Last boot shutdown: FALSE
Sleep in progrees: FALSE

Power button timestamp: 0
System running: TRUE
Connected standby in progress: FALSE
User shutdown in progress: FALSE
System shutdown in progress: FALSE
Sleep in progress: 6
Connected standby scenario instance id: 5
Connected standby entry reason: 12
Connected standby exit reason: 31
System sleep transitions to on: 8
Last reference time: 0x1d3645f716b79e3
Last reference time checksum: 0xb6ae84b7
Last update boot id: 6

Boot attempt count: 1
Last boot checkpoint: TRUE
Checksum: 0x7f
Last boot id: 6
Last successful shutdown boot id: 2
Last reported abnormal shutdown boot id: 5

Error info boot id: 0
Error info repeat count: 0
Error info other error count: 0
Error info code: 0
Error info other error count: 0

Power button last press time: 0x1d365b105eb9e3b
Power button cumulative press count: 6
Power button last press boot id: 6
Power button last power watchdog stage: 0x20
Power button watchdog armed: FALSE
Power button shutdown in progress: FALSE
Power button last release time: 0x1d36112993b1191
Power button cumulative release count: 5
Power button last release boot id: 6
Power button error count: 0
Power button current connected standby phase: 1
Power button transition latest checkpoint id: 9
Power button transition latest checkpoint type: 0
Power button transition latest checkpoint sequence number: 77
```

 





