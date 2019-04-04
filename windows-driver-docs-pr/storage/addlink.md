---
title: AddLink 関数
description: AddLink WMI メソッドでは、WMI プロバイダーのファブリックのリンクのイベントを WMI クライアントに通知を構成します。
ms.assetid: 67c17627-3f41-429b-a0f7-ec7782f1b1f9
keywords:
- AddLink 関数ストレージ デバイス
topic_type:
- apiref
api_name:
- AddLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 02ebb17dd65988f398548f176bf367f9f21bbfb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550370"
---
# <a name="addlink-function"></a>AddLink 関数


**AddLink** WMI メソッドの fabric リンク イベントを WMI クライアントを通知するために、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void AddLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **AddLink\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff550129)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_EventControl WMI クラス](msfc-eventcontrol-wmi-class.md)します。

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
<td align="left">Hbapiwmi.h (Hbaapi.h または Hbapiwmi.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**AddLink\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff550129)

 

 






