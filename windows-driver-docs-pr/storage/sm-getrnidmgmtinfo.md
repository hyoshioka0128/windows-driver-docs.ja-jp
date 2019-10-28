---
title: SM\_GetRNIDMgmtInfo 関数
description: SM\_GetRNIDMgmtInfo WMI メソッドは、ファイバーチャネルアダプターに関連付けられている FC3 管理情報を取得します。
ms.assetid: 0d414701-6e60-4d9d-85ae-f82b742ee907
keywords:
- SM_GetRNIDMgmtInfo function Storage デバイス
topic_type:
- apiref
api_name:
- SM_GetRNIDMgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 69296d89c49a54f5a0e43cf8560af3bc5fe8d58c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845481"
---
# <a name="sm_getrnidmgmtinfo-function"></a>SM\_GetRNIDMgmtInfo 関数


SM\_GetRNIDMgmtInfo WMI メソッドは、ファイバーチャネルアダプターに関連付けられている FC3 管理情報を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetRNIDMgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [out] HBAFC3MgmtInfo                    MgmtInfo
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
操作の状態を示す WMI 修飾子値。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 この情報は、ミニポートドライバーによって、SM\_GetRNIDMgmtInfo\_OUT 構造の HBAStatus メンバーに返されます。

*MgmtInfo*   
ファイバーチャネルアダプターに関連付けられている FC3 管理情報を保持する HBAFC3MgmtInfo 型の構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_FabricAndDomainManagementMethods WMI クラスに属しています。

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

[**SM\_GetRNIDMgmtInfo\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getrnidmgmtinfo_out)

 

 






