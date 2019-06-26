---
title: GetBindingCapability 関数
description: GetBindingCapability メソッドは、指定されたポートのバインド機能を取得します。
ms.assetid: 8db1a3cc-5b79-4de9-a4cd-c75ac72c3785
keywords:
- 記憶装置の GetBindingCapability 関数
topic_type:
- apiref
api_name:
- GetBindingCapability
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7360423d6725ad97608e44457baa9f70316360e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378555"
---
# <a name="getbindingcapability-function"></a>GetBindingCapability 関数


**GetBindingCapability**メソッドは、指定されたポートのバインド機能を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetBindingCapability(
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
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetBindingCapability\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getbindingcapability_out)構造体。

*BindType*   
永続的なバインディングに関連する機能の特定のセットを提供するには、HBA の機能とそのミニポート ドライバーを示します。 このパラメーターには値の一覧は、の説明を参照して、 [HBA\_バインド\_型](hba-bind-type.md)WMI クラスの修飾子。

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


[**GetBindingCapability\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getbindingcapability_in)

[**GetBindingCapability\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getbindingcapability_out)

 

 






