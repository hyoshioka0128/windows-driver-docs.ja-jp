---
title: GetFC3MgmtInfo 関数
description: GetFC3MgmtInfo WMI メソッドは、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を取得します。
ms.assetid: dea5d73f-22e2-4c5e-973a-aa8407955ef8
keywords:
- 記憶装置の GetFC3MgmtInfo 関数
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
ms.openlocfilehash: ee4a9079fb680385b6c1982ef53e92f0aeabafd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581570"
---
# <a name="getfc3mgmtinfo-function"></a>GetFC3MgmtInfo 関数


**GetFC3MgmtInfo** WMI メソッド、ファイバー チャネル アダプターに関連付けられている FC3 管理情報を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetFC3MgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [out] HBAFC3MgmtInfo                    MgmtInfo
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を示す WMI 修飾子の値を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetFC3MgmtInfo\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553946)構造体。

*MgmtInfo*   
返された場合は、型の構造体が含まれています。 [ **HBAFC3MgmtInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556032)ファイバー チャネル アダプターに関連付けられている FC3 管理情報を保持します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>コメント
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

<a name="requirements"></a>必要条件
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


[**GetFC3MgmtInfo\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553946)

[**HBAFC3MgmtInfo**](https://msdn.microsoft.com/library/windows/hardware/ff556032)

 

 






