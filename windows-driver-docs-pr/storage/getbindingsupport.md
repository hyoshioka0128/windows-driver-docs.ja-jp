---
title: GetBindingSupport 関数
description: GetBindingSupport メソッドは、指定されたポートが現在有効になっているバインディング機能を取得します。
ms.assetid: 50c90379-613f-42f1-80fe-7bc1b77a53bf
keywords:
- 記憶装置の GetBindingSupport 関数
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
ms.openlocfilehash: 8fd761893d6c2fbc3b44f2d3b116c3abcb1fd62d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551167"
---
# <a name="getbindingsupport-function"></a>GetBindingSupport 関数


**GetBindingSupport**メソッドは、指定されたポートが現在有効になっているバインディング機能を取得します。

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
永続的なバインドを取得するポートを示す世界中の名前。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetBindingSupport\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553917)構造体。

*BindType*   
永続的なバインディングに関連する機能の特定のセットを提供するには、HBA の機能とそのミニポート ドライバーを示すビットマップ。 このパラメーターには値の一覧は、の説明を参照して、 [HBA\_バインド\_型](hba-bind-type.md)WMI クラスの修飾子。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

これは、 **GetBindingSupport**メソッド返すは、現在有効になっているバインディング機能に対し、 [ **GetBindingCapability** ](getbindingcapability.md)メソッドは、バインドを示します特定のバインドが有効かどうかを指定せず、ポートの機能です。

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
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**GetBindingCapability**](getbindingcapability.md)

[**GetBindingSupport**](getbindingsupport.md)

[**GetBindingSupport\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553914)

[**GetBindingSupport\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553917)

 

 






