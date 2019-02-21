---
title: SetBindingSupport 関数
description: SetBindingSupport メソッドは、指定されたポートが現在有効になっているバインディング機能を設定します。
ms.assetid: 52a469df-b184-460b-b515-a0b6eb946f1f
keywords:
- 記憶装置の SetBindingSupport 関数
topic_type:
- apiref
api_name:
- SetBindingSupport
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc97c0ae362890b948f5a39fed41753ef0cd28a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536457"
---
# <a name="setbindingsupport-function"></a>SetBindingSupport 関数


**SetBindingSupport**メソッドは、指定されたポートが現在有効になっているバインディング機能を設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8               PortWWN[8],
   [in, HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE BindType,
   [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS     HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN*   
永続的なバインドを取得するポートを示す世界中の名前。

*BindType*   
永続的なバインディングに関連する機能の特定のセットを提供するには、HBA の機能とそのミニポート ドライバーを示すビットマップ。 このパラメーターには値の一覧は、の説明を参照して、 [HBA\_バインド\_型](hba-bind-type.md)WMI クラスの修飾子。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SetBindingSupport\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565575)構造体。

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
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**SetBindingSupport**](setbindingsupport.md)

[**SetBindingSupport\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565566)

[**SetBindingSupport\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565575)

 

 






