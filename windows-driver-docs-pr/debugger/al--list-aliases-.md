---
title: al (エイリアスの一覧)
description: Al コマンドは、現在定義されているすべてのユーザーというエイリアスの一覧を表示します。
ms.assetid: 40e20edb-4545-4c5a-bb56-61e00b064efc
keywords:
- al (一覧のエイリアス) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- al (List Aliases)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7cac3302ab00f1c88cbf4a3e35d054b942ec36b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527789"
---
# <a name="al-list-aliases"></a>al (エイリアスの一覧)


**Al**コマンドは、現在定義されているすべてのユーザーというエイリアスの一覧を表示します。

```dbgcmd
al
```

## <span id="ddk_cmd_list_aliases_dbg"></span><span id="DDK_CMD_LIST_ALIASES_DBG"></span>


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

エイリアスを使用する方法の詳細については、[Using エイリアス](using-aliases.md)を参照してください。

<a name="remarks"></a>注釈
-------

**Al**コマンドには、すべてのユーザーという名前のエイリアスが一覧表示します。 ただし、このコマンドでは固定名のエイリアス ($u0 に u9 ドル) は表示されません。

 

 





