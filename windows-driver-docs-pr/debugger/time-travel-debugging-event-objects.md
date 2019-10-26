---
title: TTD イベントオブジェクト
description: このセクションでは、タイムトラベルデバッグに関連するイベントモデルオブジェクトについて説明します。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99c5a84dc57edad2eebac21fb6185fafc5595cb2
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916218"
---
# <a name="ttd-event-objects"></a>TTD イベントオブジェクト

## <a name="description"></a>説明
*TTD イベント*オブジェクトは、タイムトラベルトレース中に発生した重要なイベントに関する情報を提供するために使用されます。

## <a name="properties"></a>[プロパティ]

| プロパティ | 説明 |
| --- | --- |
| タスクバーの検索ボックスに | 発生したイベントの種類を示します。 使用可能な値: ThreadCreated、Threadcreated、ModuleLoaded、Moduleloaded、例外 |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| 位置 | イベントが発生した位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |
| 第 | 読み込まれたモジュールまたはアンロードされたモジュールに関する情報を格納している[モジュールオブジェクト](time-travel-debugging-module-objects.md)。 |
| レッド | 作成または終了されたスレッドに関する情報を格納している[スレッドオブジェクト](time-travel-debugging-thread-objects.md)。 |
| 例外的 | ヒットした例外に関する情報を格納している[例外オブジェクト](time-travel-debugging-exception-objects.md)。 |

これらの子オブジェクトの \* は、イベントの種類によって異なります。

## <a name="example-usage"></a>使用例



```dbgcmd
0:000> dx -r2 @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
@$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)                
    [0x0]            : Exception of type CPlusPlus at PC: 0X777663B0
        Position         : 13B7:0 [Time Travel]
        Type             : CPlusPlus
        ProgramCounter   : 0x777663b0
        Code             : 0xe06d7363
        Flags            : 0x1
        RecordAddress    : 0x0
    [0x1]            : Exception of type Hardware at PC: 0XF1260D0
        Position         : BC0F:0 [Time Travel]
        Type             : Hardware
        ProgramCounter   : 0xf1260d0
        Code             : 0x80000003
        Flags            : 0x0
        RecordAddress    : 0x0
```


## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)
