---
title: .abandon (プロセスの破棄)
description: .Abandon コマンドでは、デバッグ セッションを終了が、対象のアプリケーション デバッグ状態のままにします。 これは、休止モードにデバッガーを返します。
ms.assetid: e44ae9b8-b6a2-4648-911d-61ff3c94527c
keywords:
- .abandon (電話放棄呼プロセス) の Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .abandon (Abandon Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5227a6f1aaa507204ddf470c718241671895f07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334832"
---
# <a name="abandon-abandon-process"></a>.abandon (プロセスの破棄)


**.Abandon**コマンドはデバッグ セッションを終了しますが、対象のアプリケーション デバッグ状態のままになります。 これは、休止モードにデバッガーを返します。

```dbgcmd
.abandon [/h|/n] 
```

## <a name="span-idddkmetaabandonprocessdbgspanspan-idddkmetaabandonprocessdbgspanparameters"></a><span id="ddk_meta_abandon_process_dbg"></span><span id="DDK_META_ABANDON_PROCESS_DBG"></span>パラメーター


<span id="________h______"></span><span id="________H______"></span> **/h**   
未処理のデバッグ イベントは続きし、処理済みとしてマークします。 これが既定値です。

<span id="________n______"></span><span id="________N______"></span> **/n**   
ハンドルされていないすべての未処理のデバッグ イベントが継続します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、Windows XP および Windows の以降のバージョンでのみサポートされます。

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
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ターゲットのデバッグ状態の場合、新しいデバッガーを接続しています。 参照してください[対象アプリケーションを再アタッチ](reattaching-to-the-target-application.md)詳細についてはします。 ただし、プロセスを 1 回破棄された後に復元できませんを実行中の状態にデバッガーをアタッチせずします。

 

 





