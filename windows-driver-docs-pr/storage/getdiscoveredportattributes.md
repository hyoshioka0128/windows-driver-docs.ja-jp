---
title: GetDiscoveredPortAttributes 関数
description: GetDiscoveredPortAttributes WMI メソッドは、指定したリモート ファイバー チャネル ポートの属性を取得します。
ms.assetid: f71a02cf-035a-4de2-bb28-e1141a92795c
keywords:
- 記憶装置の GetDiscoveredPortAttributes 関数
topic_type:
- apiref
api_name:
- GetDiscoveredPortAttributes
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fde95e3872e481915bdfd6ee6cc7c61e9e051b86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571191"
---
# <a name="getdiscoveredportattributes-function"></a>GetDiscoveredPortAttributes 関数


**GetDiscoveredPortAttributes** WMI メソッドは、指定したリモート ファイバー チャネル ポートの属性を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetDiscoveredPortAttributes(
   [in] uint32                                                        PortIndex,
   [in] uint32                                                        DiscoveredPortIndex,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>パラメーター
----------

*PortIndex*   
Nx 型のローカル ポートのインデックス\_検出されたリモート ポートを照会するためのポート。 この情報は、ミニポート ドライバーに配信される、 **PortIndex**のメンバー、 [ **GetDiscoveredPortAttributes\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553927)構造体。

*DiscoveredPortIndex*   
クエリを実行するリモートのポートのインデックス。 この情報は、ミニポート ドライバーに配信される、 **DiscoveredPortIndex**のメンバー、 [ **GetDiscoveredPortAttributes\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553927)構造体。

*HBAStatus*   
に返された場合、操作の状態を示す WMI 修飾子の値を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetDiscoveredPortAttributes\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553930)構造体。

*PortAttributes*   
型の構造体[ **MSFC\_HBAPortAttributesResults** ](https://msdn.microsoft.com/library/windows/hardware/ff562510)で検出された fc 属性\_ポートを返すことができます。 ミニポート ドライバーには、この情報が返されます、 **PortAttributes**のメンバー、 [ **GetDiscoveredPortAttributes\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553930)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>コメント
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

<a name="requirements"></a>必要条件
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


[**GetDiscoveredPortAttributes\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553927)

[**GetDiscoveredPortAttributes\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff553930)

[**MSFC\_HBAPortAttributesResults**](https://msdn.microsoft.com/library/windows/hardware/ff562510)

 

 






