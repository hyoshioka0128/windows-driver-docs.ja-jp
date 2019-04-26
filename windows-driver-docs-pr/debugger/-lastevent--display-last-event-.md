---
title: .lastevent (最後のイベントの表示)
description: .Lastevent コマンドには、最新の例外または発生したイベントが表示されます。
ms.assetid: 6f722c22-cb0f-4a10-b719-a168f7ba0943
keywords:
- .lastevent (最後のイベントを表示する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .lastevent (Display Last Event)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc4137f1aa7b2ed47a26aedaabd990995d15a0eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336197"
---
# <a name="lastevent-display-last-event"></a>.lastevent (最後のイベントの表示)


**.Lastevent**コマンドは、最新の例外または発生したイベントが表示されます。

```dbgcmd
.lastevent 
```

## <span id="ddk_meta_display_last_event_dbg"></span><span id="DDK_META_DISPLAY_LAST_EVENT_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

例外とイベントの詳細については、次を参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)します。

<a name="remarks"></a>注釈
-------

常にデバッガーに重大な例外を作成します。 常に、*最後のイベント*デバッガーがコマンドの入力を許可するとします。 使用してデバッガーに割り込む場合[ **CTRL + C**](ctrl-c--break-.md)、 [CTRL + BREAK](debug---break.md)、またはデバッグ |Break 0x80000003 の例外コードが作成されます。

 

 





