---
title: fileobj
description: Fileobj 拡張機能では、FILE_OBJECT 構造に関する詳細情報が表示されます。
ms.assetid: ee9237e7-8a1f-473c-9e30-f2b0731a7519
keywords:
- FILE_OBJECT
- Windows デバッグ fileobj
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- fileobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0d9870a802e1382572e5dbcbd8dbea12130826f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364322"
---
# <a name="fileobj"></a>!fileobj


**! Fileobj**拡張機能は、ファイルに関する詳細情報を表示します。\_オブジェクトの構造体。

```dbgcmd
!fileobj FileObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
アドレスを指定します、 [FILE_OBJECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)構造体。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ファイル オブジェクトについては、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

場合、ファイル\_オブジェクトの構造が関連付けられているキャッシュでは、 **! fileobj**を解析し、キャッシュ情報を表示しようとしています。

 

 





