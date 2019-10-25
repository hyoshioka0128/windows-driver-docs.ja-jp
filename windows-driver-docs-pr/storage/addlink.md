---
title: AddLink 関数
description: AddLink WMI メソッドは、wmi プロバイダーに対して、ファブリックリンクイベントの WMI クライアントを通知するように構成します。
ms.assetid: 67c17627-3f41-429b-a0f7-ec7782f1b1f9
keywords:
- AddLink 関数のストレージデバイス
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
ms.openlocfilehash: df71b5b3022bb1af53bed06adbf4cd46da2b638a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845115"
---
# <a name="addlink-function"></a>AddLink 関数


**Addlink** wmi メソッドは、wmi プロバイダーに対して、ファブリックリンクイベントの wmi クライアントを通知するように構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void AddLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Addlink\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addlink_out)構造体の**hbastatus**メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_EventControl WMI クラス](msfc-eventcontrol-wmi-class.md)に属しています。

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
<td align="left">Hbapiwmi (Hbaapi .h または Hbapiwmi を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**AddLink\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addlink_out)

 

 






