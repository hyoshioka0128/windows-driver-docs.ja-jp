---
title: SM\_GetRNIDMgmtInfo 関数
description: SM\_GetRNIDMgmtInfo WMI メソッド、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を取得します。
ms.assetid: 0d414701-6e60-4d9d-85ae-f82b742ee907
keywords:
- 記憶装置の SM_GetRNIDMgmtInfo 関数
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
ms.openlocfilehash: 477a1af3ba754dafa024713ecc84ddb59c2fe683
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384308"
---
# <a name="smgetrnidmgmtinfo-function"></a>SM\_GetRNIDMgmtInfo 関数


SM\_GetRNIDMgmtInfo WMI メソッド、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を取得します。

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

*HBAStatus*   
操作の状態を示す WMI 修飾子の値。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_GetRNIDMgmtInfo\_構造体。

*MgmtInfo*   
HBAFC3MgmtInfo、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を保持する型の構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_FabricAndDomainManagementMethods WMI クラスです。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SM\_GetRNIDMgmtInfo\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_getrnidmgmtinfo_out)

 

 






