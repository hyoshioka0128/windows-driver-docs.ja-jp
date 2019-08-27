---
title: finddata
description: Finddata 拡張機能は、指定されたファイルオブジェクト内の特定のオフセットにキャッシュされたデータを表示します。
ms.assetid: 1d6f920b-5716-4ccc-8c2d-08b422f57124
keywords:
- キャッシュマネージャー
- finddata Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- finddata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a67d9c4ff7ceec340ba684c35b0776cf8e1f1fd
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025150"
---
# <a name="finddata"></a>!finddata


**! Finddata**拡張機能は、指定されたファイルオブジェクト内の特定のオフセットにキャッシュされたデータを表示します。

```dbgcmd
!finddata FileObject Offset
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
ファイルオブジェクトのアドレスを指定します。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span>*オフセット*   
オフセットを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

キャッシュ管理の詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンを参照してください。

その他のキャッシュ管理拡張機能の詳細については、 [ **! cchelp**](-cchelp.md)拡張機能に関する説明を参照してください。

 

 





