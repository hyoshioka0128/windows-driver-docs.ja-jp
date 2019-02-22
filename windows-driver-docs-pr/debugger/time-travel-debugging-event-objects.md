---
title: TTD イベント オブジェクト
description: このセクションでは、タイム トラベルのデバッグに関連付けられているイベント モデル オブジェクトについて説明します。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3511933227006dc5a5fe22b8c8da99a75dbfe887
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537314"
---
# <a name="ttd-event-objects"></a>TTD イベント オブジェクト
## <a name="description"></a>説明
*TTD イベント*オブジェクトを使用して、タイム トラベルのトレース中に発生する重要なイベントに関する情報を提供します。

## <a name="properties"></a>プロパティ

| プロパティ | 説明 |
| --- | --- |
| 種類 | 発生したイベントの種類について説明します。 設定可能な値は、次のとおりです。ThreadCreated、ThreadTerminated、ModuleLoaded、ModuleUnloaded、例外 |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| 位置 | A[位置オブジェクト](time-travel-debugging-position-objects.md)イベントが発生した位置をについて説明します。 |
| モジュール * | A[モジュール オブジェクト](time-travel-debugging-module-objects.md)ロードまたはアンロードされたモジュールに関する情報を格納します。 |
| スレッド * | A[スレッド オブジェクト](time-travel-debugging-thread-objects.md)が作成または終了したスレッドに関する情報を格納します。 |
| 例外 * | [例外オブジェクト](time-travel-debugging-exception-objects.md)ヒットが発生した例外に関する情報を格納します。 |

\* これらの子オブジェクトの存在は、イベントの種類によって異なります。

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

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---


