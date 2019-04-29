---
title: TTD スレッド オブジェクト
description: このセクションでは、タイム トラベルのデバッグに関連付けられているスレッド モデル オブジェクトについて説明します。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5694c648acd00d3933db17cac8e46e661b8f0211
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330956"
---
# <a name="ttd-thread-objects"></a>TTD スレッド オブジェクト
## <a name="description"></a>説明
*スレッドの TTD*についてスレッドとその有効期間を時間帯に出張のトレース情報を提供するオブジェクトを使用します。

## <a name="properties"></a>プロパティ

| プロパティ | 説明 |
| --- | --- |
| 一意の Id | トレースの間でのスレッドの一意の ID。 |
| ID | スレッド TID します。 |


## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| 有効期間 | A [TTD range オブジェクト](time-travel-debugging-range-objects.md)スレッドの有効期間をについて説明します。 |
| ActiveTime | A [TTD range オブジェクト](time-travel-debugging-range-objects.md)スレッドがアクティブだった時間をについて説明します。 |


## <a name="example-usage"></a>使用例

配列内のすべてのスレッドを表示するのにには、この dx コマンドを使用します。

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

配列の最初のスレッドに関する情報を表示するのにには、この dx コマンドを使用します。

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

[タイム トラベル] リンクでは、スレッドがアクティブなときに、SeekTo() へのリンクがトレースに特定の位置までに提供します。 

```dbgcmd
0:0:000> dx @$curprocess.TTD.Threads[0].@"ActiveTime".@"MinPosition".SeekTo()
Setting position: 50C63:0
@$curprocess.TTD.Threads[0].@"ActiveTime".@"MinPosition".SeekTo()
(40b4.2428): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 50C63:0
ntdll!NtTestAlert+0x14:
00007ffb`e3e289d4 c3              ret
```


## <a name="see-also"></a>関連項目

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---


