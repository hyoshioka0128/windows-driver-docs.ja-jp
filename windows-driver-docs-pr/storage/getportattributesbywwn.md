---
title: GetPortAttributesByWWN 関数
description: GetPortAttributesByWWN メソッドは、ポートの名前で指定されたポートの属性を取得します。
ms.assetid: 24b62b1c-9f47-40f1-aa72-849fabcbfbae
keywords:
- 記憶装置の GetPortAttributesByWWN 関数
topic_type:
- apiref
api_name:
- GetPortAttributesByWWN
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1109369b42d33c9430b166631c1ed2095b9bc067
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536481"
---
# <a name="getportattributesbywwn-function"></a>GetPortAttributesByWWN 関数


**GetPortAttributesByWWN**メソッドは、ポートの名前で指定されたポートの属性を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetPortAttributesByWWN(
   [in, HBAType("HBA_WWN")] uint8                                     wwn[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>パラメーター
----------

*wwn\[8\]*   
属性を持つがクエリを実行するには、ポートの名前。 この情報は、ミニポート ドライバーに配信される、 **wwn**のメンバー、 [ **GetPortAttributesByWWN\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff554967)構造体。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetPortAttributesByWWN\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff554969)構造体。

*PortAttributes*   
型の構造体[ **MSFC\_HBAPortAttributesResults** ](https://msdn.microsoft.com/library/windows/hardware/ff562510)で検出された fc 属性\_ポートを返すことができます。 ミニポート ドライバーには、この情報が返されます、 **PortAttributes**のメンバー、 [ **GetDiscoveredPortAttributes\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553930)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h (Hbapiwmi.h、Hbaapi.h、Hbaapi.h など)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**GetPortAttributesByWWN\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff554967)

[**GetPortAttributesByWWN\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff554969)

[**MSFC\_HBAPortAttributesResults**](https://msdn.microsoft.com/library/windows/hardware/ff562510)

 

 






