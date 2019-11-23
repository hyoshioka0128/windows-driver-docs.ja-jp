---
title: SM\_SetRNIDMgmtInfo 関数
description: SM\_SetRNIDMgmtInfo WMI メソッドは、ファイバーチャネルアダプターに関連付けられている FC3 管理情報を設定します。
ms.assetid: 235beb52-0e09-402d-ace1-0543ad3ee74f
keywords:
- SM_SetRNIDMgmtInfo 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SetRNIDMgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dfad0e4df3b0afb974d20afc2b1525d94ed64cf1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845442"
---
# <a name="sm_setrnidmgmtinfo-function"></a>SM\_SetRNIDMgmtInfo 関数


SM\_SetRNIDMgmtInfo WMI メソッドは、ファイバーチャネルアダプターに関連付けられている FC3 管理情報を設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SetRNIDMgmtInfo(
   [in] HBAFC3MgmtInfo                     MgmtInfo,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*MgmtInfo*   
ファイバーチャネルアダプターに関連付けられている FC3 管理情報を保持する HBAFC3MgmtInfo 型の構造体。

*Hbastatus*   
操作の状態を示す WMI 修飾子値。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 この情報は、ミニポートドライバーによって、SM\_GetRNIDMgmtInfo\_OUT 構造の HBAStatus メンバーに返されます。

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

[**SM\_SetRNIDMgmtInfo\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setrnidmgmtinfo_in)

[**SM\_SetRNIDMgmtInfo\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setrnidmgmtinfo_out)

 

 






