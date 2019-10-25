---
title: RemovePersistentEntry 関数
description: RemovePersistentEntry メソッドは、指定されたポートに関連付けられているバインドの一覧からバインドを削除します。
ms.assetid: f192367e-2e17-44e4-aa0b-7d23cd828b11
keywords:
- RemovePersistentEntry function Storage デバイス
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
ms.openlocfilehash: cd42608261c2a6fc9f4eff82ac5bead090f46bfe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842708"
---
# <a name="removepersistententry-function"></a>RemovePersistentEntry 関数


**RemovePersistentEntry**メソッドは、指定されたポートに関連付けられているバインドの一覧からバインドを削除します。

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
永続的なバインドが変更されるポートを示すワールドワイド名。

*バインド*   
指定されたポートのバインディングリストから削除されるバインディングを示す[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)型の構造体。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**RemovePersistentEntry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removepersistententry_out)構造体の**hbastatus**メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_HBAFCPInfo WMI クラス](msfc-hbafcpinfo-wmi-class.md)に属しています。

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
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**RemovePersistentEntry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removepersistententry_in)

[**RemovePersistentEntry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removepersistententry_out)

 

 






