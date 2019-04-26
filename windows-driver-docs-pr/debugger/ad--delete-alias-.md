---
title: ad (エイリアスの削除)
description: Ad コマンドでは、エイリアスの一覧からエイリアスを削除します。
ms.assetid: 8ff223b6-5cfb-4d87-b45f-ad9bd51faf7f
keywords:
- ad (エイリアスの削除) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ad (Delete Alias)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e22b13edd36c4d97ed2a932e8e646b54972781bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354702"
---
# <a name="ad-delete-alias"></a>ad (エイリアスの削除)


**Ad**コマンド エイリアスの一覧からエイリアスを削除します。

```dbgcmd
ad [/q] Name 
ad * 
```

## <a name="span-idddkcmddeletealiasdbgspanspan-idddkcmddeletealiasdbgspanparameters"></a><span id="ddk_cmd_delete_alias_dbg"></span><span id="DDK_CMD_DELETE_ALIAS_DBG"></span>パラメーター


<span id="________q______"></span><span id="________Q______"></span> **/q**   
クワイエット モードを指定します。 このモードは、場合、エラー メッセージを非表示にエイリアスを*名前*を指定しますが存在しません。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名*   
削除する別名の名前を指定します。 アスタリスクを指定する場合 (\*)、すべてのエイリアスが削除されます (名前のエイリアスがある場合でも"\*")。

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

エイリアスを使用する方法の詳細については、次を参照してください。 [Using エイリアス](using-aliases.md)します。

<a name="remarks"></a>注釈
-------

使用することができます、 **ad**という名前のユーザーの任意のエイリアスを削除するコマンド。 ただし、このコマンドを使用して固定名のエイリアス ($u0 に u9 $) を削除することはできません。

 

 





