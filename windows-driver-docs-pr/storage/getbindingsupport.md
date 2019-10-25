---
title: GetBindingSupport 関数
description: GetBindingSupport メソッドは、指定されたポートに対して現在有効なバインディング機能を取得します。
ms.assetid: 50c90379-613f-42f1-80fe-7bc1b77a53bf
keywords:
- GetBindingSupport 関数のストレージデバイス
topic_type:
- apiref
api_name:
- GetBindingSupport
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1cb462f87b521ca83e316ace0d68eec018371938
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837852"
---
# <a name="getbindingsupport-function"></a>GetBindingSupport 関数


**Getbindingsupport**メソッドは、指定されたポートに対して現在有効なバインディング機能を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [out, HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE BindType
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN\[8\]*    
永続的なバインドを取得するポートを示す、世界規模の名前。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Getbindingsupport\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingsupport_out)構造体の**hbastatus**メンバーでこの情報を返します。

*Bindtype*   
永続的バインディングに関連する特定の機能セットを提供する、HBA とそのミニポートドライバーの機能を示すビットマップ。 このパラメーターに指定できる値の一覧については、「WMI クラス修飾子の[\_バインド\_HBA](hba-bind-type.md)の説明を参照してください。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この**Getbindingsupport**メソッドは、現在有効になっているバインディング機能を返します。一方、 [**getbindingsupport**](getbindingcapability.md)メソッドは、特定のバインドが有効になっているかどうかを参照せずに、ポートのバインディング機能を示します。じゃない。

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
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi .lib</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**GetBindingCapability ビリティ**](getbindingcapability.md)

[**GetBindingSupport**](getbindingsupport.md)

[**GetBindingSupport\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingsupport_in)

[**GetBindingSupport\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingsupport_out)

 

 






