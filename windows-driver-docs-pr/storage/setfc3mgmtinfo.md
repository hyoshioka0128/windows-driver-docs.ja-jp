---
title: SetFC3MgmtInfo 関数
description: SetFC3MgmtInfo WMI メソッドは、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を設定します。
ms.assetid: 180f9945-3b2e-494e-8e6d-648ff4369c3b
keywords:
- 記憶装置の SetFC3MgmtInfo 関数
topic_type:
- apiref
api_name:
- SetFC3MgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 43733e42ee08060048cdeb4119d42edba41a1d2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374630"
---
# <a name="setfc3mgmtinfo-function"></a>SetFC3MgmtInfo 関数


**SetFC3MgmtInfo** WMI メソッド、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SetFC3MgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in] HBAFC3MgmtInfo                     MgmtInfo
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SetFC3MgmtInfo\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_out)構造体。

*MgmtInfo*   
型の構造体[ **HBAFC3MgmtInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)ファイバー チャネル アダプターを構成するために使用する FC3 管理情報を保持します。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **SetFC3MgmtInfo\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_in)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

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
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**GetFC3MgmtInfo\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfc3mgmtinfo_out)

[**HBAFC3MgmtInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)

[**SetFC3MgmtInfo\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_in)

[**SetFC3MgmtInfo\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_out)

 

 






