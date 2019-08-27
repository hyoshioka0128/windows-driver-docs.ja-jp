---
title: fileobj
description: Fileobj 拡張機能には、FILE_OBJECT 構造体に関する詳細情報が表示されます。
ms.assetid: ee9237e7-8a1f-473c-9e30-f2b0731a7519
keywords:
- FILE_OBJECT
- fileobj Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- fileobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1d56451c0849adc9f196cb4c3f6546e3cbb70f1
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025304"
---
# <a name="fileobj"></a>!fileobj


**! Fileobj**拡張機能は、ファイル\_オブジェクトの構造に関する詳細情報を表示します。

```dbgcmd
!fileobj FileObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
[FILE_OBJECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)構造体のアドレスを指定します。

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
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ファイルオブジェクトの詳細については、Microsoft Windows SDK のドキュメント、Windows Driver Kit (WDK) のドキュメント、および Mark Russinovich と David ソロモンによる*Microsoft windows の内部構造*に関するドキュメントを参照してください。

<a name="remarks"></a>コメント
-------

場合、ファイル\_オブジェクトの構造が関連付けられているキャッシュでは、 **! fileobj**を解析し、キャッシュ情報を表示しようとしています。

 

 





