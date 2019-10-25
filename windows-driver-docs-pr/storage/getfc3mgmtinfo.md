---
title: GetFC3MgmtInfo 関数
description: GetFC3MgmtInfo WMI メソッドは、ファイバーチャネルアダプターに関連付けられている FC3 管理情報を取得します。
ms.assetid: dea5d73f-22e2-4c5e-973a-aa8407955ef8
keywords:
- GetFC3MgmtInfo function Storage デバイス
topic_type:
- apiref
api_name:
- GetFC3MgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cc04e41c371a7e8cc85539a368c6da5c8ceb8e66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837973"
---
# <a name="getfc3mgmtinfo-function"></a>GetFC3MgmtInfo 関数


**GetFC3MgmtInfo** WMI メソッドは、ファイバーチャネルアダプターに関連付けられている FC3 管理情報を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetFC3MgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [out] HBAFC3MgmtInfo                    MgmtInfo
);
```

<a name="parameters"></a>parameters
----------

*Hbastatus*   
返されるときに、操作の状態を示す WMI 修飾子値を格納します。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**GetFC3MgmtInfo\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc3mgmtinfo_out)構造体の**hbastatus**メンバーにこの情報を返します。

*MgmtInfo*   
返されると、ファイバーチャネルアダプターに関連付けられている FC3 管理情報を保持する[**HBAFC3MgmtInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)型の構造体を格納します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>解説
-------

この WMI メソッドは、 [Msfc\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)に属しています。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲットプラットフォーム</p></td>
<td align="left">デスクトップ</td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**GetFC3MgmtInfo\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc3mgmtinfo_out)

[**HBAFC3MgmtInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)

 

 






