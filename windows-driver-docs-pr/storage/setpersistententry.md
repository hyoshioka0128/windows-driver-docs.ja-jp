---
title: SetPersistentEntry 関数
description: SetPersistentEntry メソッドでは、指定されたポートに関連付けられたバインディングの一覧に、バインディングを追加します。
ms.assetid: 52680641-9f63-4c8e-9538-4c725b9074a3
keywords:
- 記憶装置の SetPersistentEntry 関数
topic_type:
- apiref
api_name:
- SetPersistentEntry
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8e12638d8ad8ba5c02646e759f888fbebc517c39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528541"
---
# <a name="setpersistententry-function"></a>SetPersistentEntry 関数


**SetPersistentEntry**メソッドは、指定されたポートに関連付けられたバインディングの一覧に、バインディングを追加します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SetPersistentEntry(
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
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SetPersistentEntry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565795)構造体。

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


[**SetPersistentEntry\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565790)

[**SetPersistentEntry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565795)

 

 






