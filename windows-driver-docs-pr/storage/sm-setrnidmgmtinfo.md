---
title: SM\_SetRNIDMgmtInfo 関数
description: SM\_SetRNIDMgmtInfo WMI メソッド、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を設定します。
ms.assetid: 235beb52-0e09-402d-ace1-0543ad3ee74f
keywords:
- 記憶装置の SM_SetRNIDMgmtInfo 関数
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
ms.openlocfilehash: 0031be8539786d513f528577b8b306ba89f349f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559198"
---
# <a name="smsetrnidmgmtinfo-function"></a>SM\_SetRNIDMgmtInfo 関数


SM\_SetRNIDMgmtInfo WMI メソッド、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を設定します。

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
HBAFC3MgmtInfo、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を保持する型の構造体。

*HBAStatus*   
操作の状態を示す WMI 修飾子の値。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_GetRNIDMgmtInfo\_構造体。

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

[**SM\_SetRNIDMgmtInfo\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566337)

[**SM\_SetRNIDMgmtInfo\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566338)

 

 






