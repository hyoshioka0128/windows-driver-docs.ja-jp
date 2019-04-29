---
title: logexts.logd
description: Logexts.logd 拡張機能には、ログ記録が無効にします。
ms.assetid: d3c3403d-f86b-4f2a-a261-c00eb0b2b756
keywords:
- デバッグ logexts.logd Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ee01792b89f84b6e777337e842425fb32f01b69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336135"
---
# <a name="logextslogd"></a>!logexts.logd


**! Logexts.logd**拡張機能は、ログ記録を無効にします。

```dbgcmd
    !logexts.logd 
```

## <span id="ddk__logexts_logd_dbg"></span><span id="DDK__LOGEXTS_LOGD_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [Logger と LogViewer](logger-and-logviewer.md)します。

<a name="remarks"></a>コメント
-------

これにより、プログラムを自由に実行を許可する取り組みの一環として削除するすべての API フック。 COM のフックは削除されません、ために再度有効にできません。

 

 





