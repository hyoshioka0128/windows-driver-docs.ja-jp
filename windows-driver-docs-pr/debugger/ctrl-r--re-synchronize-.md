---
title: (再同期) CTRL + R
description: CTRL + R キーを同期対象のコンピューターにします。
ms.assetid: 95ffa380-af90-4d56-b973-038e7ccc6760
keywords:
- Ctrl キーを押しながら R キー (再同期) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+R (Re-synchronize)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb95a8994c80d6cc36432ae71eb9ac064bb33229
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557762"
---
# <a name="ctrlr-re-synchronize"></a>(再同期) CTRL + R


CTRL + R キーを同期対象のコンピューターにします。

KD 構文

```dbgcmd
CTRL+R  ENTER 
```

WinDbg の構文

```dbgcmd
CTRL+ALT+R 
```

## <span id="ddk_meta_ctrl_r_dbg"></span><span id="DDK_META_CTRL_R_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>デバッガー</strong></p></td>
<td align="left"><p>KD と WinDbg のみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のメソッドの再ターゲットとの接続を確立するには、[対象のコンピューターに同期](synchronizing-with-the-target-computer.md)を参照してください。

<a name="remarks"></a>注釈
-------

これは、対象のコンピューターに、ホスト コンピューターの同期を試行します。 ターゲットが応答していない場合は、このキーを使用します。

1394 カーネルの接続を使用している場合の再同期は常に失敗します。

 

 





