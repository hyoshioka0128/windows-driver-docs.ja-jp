---
title: TTD Thread オブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられているスレッドモデルオブジェクトについて説明します。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0d38085e78f03dc80ee63facaf3a16dab87c6b4e
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916137"
---
# <a name="ttd-thread-objects"></a>TTD Thread オブジェクト

## <a name="description"></a>説明

*TTD Thread*オブジェクトは、タイムトラベルトレース中にスレッドとその有効期間に関する情報を提供するために使用されます。

## <a name="properties"></a>[プロパティ]

| プロパティ | 説明 |
| --- | --- |
| UniqueId | トレース全体のスレッドの一意の ID。 |
| Id | スレッドの TID。 |


## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| 最短 | スレッドの有効期間を記述する[TTD range オブジェクト](time-travel-debugging-range-objects.md)。 |
| ActiveTime | スレッドがアクティブであった時刻を示す[TTD range オブジェクト](time-travel-debugging-range-objects.md)。 |


## <a name="example-usage"></a>使用例

この dx コマンドを使用して、配列内のすべてのスレッドを表示します。

```dbgcmd
0:0:000> dx -g @$curprocess.TTD.Threads
=================================================================================================================
=                             = (+) UniqueId = (+) Id    = (+) Lifetime                 = (+) ActiveTime        =
=================================================================================================================
= [0x0] : UID: 2, TID: 0x2428 - 0x2          - 0x2428    - [0:0, 6F0C4:0]               - [50C63:0, 6F0C4:0]    =
= [0x1] : UID: 3, TID: 0x3520 - 0x3          - 0x3520    - [0:0, FFFFFFFFFFFFFFFE:0]    - [5115A:0, 56B07:0]    =
= [0x2] : UID: 4, TID: 0x18E8 - 0x4          - 0x18e8    - [0:0, FFFFFFFFFFFFFFFE:0]    - [52F65:0, 56B1E:0]    =
= [0x3] : UID: 5, TID: 0x5690 - 0x5          - 0x5690    - [0:0, FFFFFFFFFFFFFFFE:0]    - [5300D:0, 5D4FA:0]    =
= [0x4] : UID: 6, TID: 0x46FC - 0x6          - 0x46fc    - [0:0, FFFFFFFFFFFFFFFE:0]    - [53782:0, 5433B:0]    =
= [0x5] : UID: 7, TID: 0x58D0 - 0x7          - 0x58d0    - [0:0, FFFFFFFFFFFFFFFE:0]    - [542FE:0, 543B9:0]    =
= [0x6] : UID: 8, TID: 0x950  - 0x8          - 0x950     - [0:0, FFFFFFFFFFFFFFFE:0]    - [543C4:0, 544B8:0]    =
= [0x7] : UID: 9, TID: 0x4514 - 0x9          - 0x4514    - [0:0, 6D61B:0]               - [5DBBD:0, 6D61B:0]    =
=================================================================================================================
```

この dx コマンドを使用して、配列内の最初のスレッドに関する情報を表示します。

```dbgcmd
0:0:000 dx -r2 @$curprocess.TTD.Threads[0]
@$curprocess.TTD.Threads[0]                 : UID: 2, TID: 0x2428
    UniqueId         : 0x2
    Id               : 0x2428
    Lifetime         : [0:0, 6F0C4:0]
        MinPosition      : Min Position [Time Travel]
        MaxPosition      : 6F0C4:0 [Time Travel]
    ActiveTime       : [50C63:0, 6F0C4:0]
        MinPosition      : 50C63:0 [Time Travel]
        MaxPosition      : 6F0C4:0 [Time Travel]
```

[タイムトラベル] リンクを使用すると、スレッドがアクティブであったときのトレース内の特定の位置に対する SeekTo () へのリンクが提供されます。 

```dbgcmd
0:0:000> dx @$curprocess.TTD.Threads[0].@"ActiveTime".@"MinPosition".SeekTo()
Setting position: 50C63:0
@$curprocess.TTD.Threads[0].@"ActiveTime".@"MinPosition".SeekTo()
(40b4.2428): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 50C63:0
ntdll!NtTestAlert+0x14:
00007ffb`e3e289d4 c3              ret
```


## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)
