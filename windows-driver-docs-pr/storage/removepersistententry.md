---
title: RemovePersistentEntry 関数
description: RemovePersistentEntry メソッドでは、指定されたポートに関連付けられたバインディングの一覧からバインドを削除します。
ms.assetid: f192367e-2e17-44e4-aa0b-7d23cd828b11
keywords:
- 記憶装置の RemovePersistentEntry 関数
topic_type:
- apiref
api_name:
- RemovePersistentEntry
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: af5f25f15372845c46293af3f925175633df1a69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530794"
---
# <a name="removepersistententry-function"></a>RemovePersistentEntry 関数


**RemovePersistentEntry**メソッドは、指定されたポートに関連付けられたバインディングの一覧から、バインドを削除します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void RemovePersistentEntry(
   [in, HBAType("HBA_WWN")] uint8                            PortWWN[8],
   [in, HbaType("HBA_FCPBINDINGENTRY2")] HBAFCPBindingEntry2 Binding,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                   HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN*   
永続的なバインドが変更するポートを示す世界中の名前。

*バインド*   
型の構造体[ **HBAFCPBindingEntry2** ](https://msdn.microsoft.com/library/windows/hardware/ff556035)バインドの指定されたポートの一覧から削除するバインディングを示します。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **RemovePersistentEntry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff563994)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_HBAFCPInfo WMI クラス](msfc-hbafcpinfo-wmi-class.md)します。

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
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**RemovePersistentEntry\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff563990)

[**RemovePersistentEntry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff563994)

 

 






