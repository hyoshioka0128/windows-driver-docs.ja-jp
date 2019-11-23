---
title: SM\_AddLink 関数
description: SM\_AddLink WMI メソッドは、wmi プロバイダーに対して、ファブリックリンクイベントの WMI クライアントを通知するように構成します。
ms.assetid: 29ddfdb7-232a-4715-bf36-5f64554ee608
keywords:
- SM_AddLink 関数記憶装置
topic_type:
- apiref
api_name:
- SM_AddLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a84618f2916d18812d527906607165215e3d6223
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842604"
---
# <a name="sm_addlink-function"></a>SM\_AddLink 関数


SM\_AddLink WMI メソッドは、wmi プロバイダーに対して、ファブリックリンクイベントの WMI クライアントを通知するように構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_AddLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_AddLink\_OUT 構造の HBAStatus メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_EventControl WMI クラスに属しています。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**SM\_AddLink\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addlink_out)

 

 






