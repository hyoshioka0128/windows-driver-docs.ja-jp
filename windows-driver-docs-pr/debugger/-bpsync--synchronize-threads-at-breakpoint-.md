---
title: .bpsync (ブレークポイントのスレッドの同期)
description: スレッドには、ブレークポイントに達すると、.bpsync コマンドは、ブレークポイントを適用するスレッドがステップ実行、ブレークポイントまで他のすべてのスレッドを停止します。
ms.assetid: 3e97ea97-77b8-4a22-b49c-c99739b42d59
keywords:
- .bpsync (ブレークポイントでのスレッドの同期) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bpsync (Synchronize Threads at Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e646158b0e11a9cd337c7ab3a0973cc55d50b19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336982"
---
# <a name="bpsync-synchronize-threads-at-breakpoint"></a>.bpsync (ブレークポイントのスレッドの同期)


スレッドが、ブレークポイントに達すると、 **.bpsync**コマンド ブレークポイントを適用するスレッドがステップ実行、ブレークポイントまで他のすべてのスレッドがフリーズします。

```dbgcmd
.bpsync 1
.bpsync 0
.bpsync 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______1______"></span> **1**   
1 つのスレッドがブレークポイントに達したときに固定するのには、すべてのスレッドをによりします。 ブレークポイント ステップ実行、ブレークポイントを適用するスレッドが、他のスレッドが凍結できません。

<span id="_______0______"></span> **0**   
1 つのスレッドがブレークポイントに達したときに実行を続行するには、他のスレッドを使用できます。 これは既定の動作です。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

パラメーターのないです。 **.bpsync**コマンドは、現在の同期のブレークポイントの動作を制御するルールを表示します。

**.Bpsync**両方ソフトウェア ブレークポイント コマンドに適用されます (設定[ **bp**](bp--bu--bm--set-breakpoint-.md)、 **bu**、または**bm**)プロセッサのブレークポイントに (セット[ **ba**](ba--break-on-access-.md))。

複数のスレッドが、同じコードを実行している可能性がある場合、 **.bpsync 1**コマンドは、ブレークポイントの出現箇所をすべてのキャプチャに役立ちます。 このコマンドでは、常に、ブレークポイントに到達する最初のスレッド、デバッガーは一時的にブレークポイントを設定するためのブレークポイントの発生箇所が欠落する可能性があります。 ブレークポイントが削除されたとき、短い期間で他のスレッドでしたコード内の同じ位置に到達し、意図どおりにブレークポイントをトリガーします。

一時的なブレークポイントの削除では、デバッガーの操作の通常の側面です。 デバッガーでブレークポイントを一時的に削除するが、ターゲットは、ブレークポイントに達するし、再開は、ターゲットが実際のコードを実行できるようにします。 実際の命令が実行された後、デバッガーは中断を reinserts します。 これを行うには、デバッガー、コードの復元 (またはデータの区切りをオフに)、シングル ステップを行い、中断を戻します。

使用する場合に注意する **.bpsync 1**、固定されているスレッド間でデッドロックの危険性があります。

 

 





