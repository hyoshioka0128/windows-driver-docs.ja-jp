---
title: .secure (保護モードのアクティブ化)
description: .Secure コマンドは、アクティブにまたは保護モードの状態を表示します。
ms.assetid: 58a8936e-898f-4608-b1b0-399d5152f410
keywords:
- .secure (セキュリティで保護されたモードをアクティブ化) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .secure (Activate Secure Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c22b9876bc2f237acf5faee7364301b2e6c278f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339809"
---
# <a name="secure-activate-secure-mode"></a>.secure (保護モードのアクティブ化)


**.Secure**コマンドをアクティブ化または保護モードの状態を表示します。

```dbgcmd
.secure 1 
.secure 
```

## <span id="ddk_meta_activate_secure_mode_dbg"></span><span id="DDK_META_ACTIVATE_SECURE_MODE_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

デバッガーは休止中にのみ、セキュリティで保護されたモードを有効にできます。 セキュリティで保護されたモードは、定義上、セキュリティで保護モードがユーザー モードのデバッグ操作を防止するため、カーネル モードのセッションにのみ適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[保護モード](secure-mode.md)します。

<a name="remarks"></a>注釈
-------

保護モードをアクティブ化するコマンドを使用して、 **.secure 1** (または **.secure**後に 0 以外の値)。

コマンドは、 **.secure**保護モードが現在アクティブかどうかが表示されます。

 

 





