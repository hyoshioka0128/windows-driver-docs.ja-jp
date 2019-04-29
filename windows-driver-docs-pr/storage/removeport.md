---
title: RemovePort 関数
description: RemovePort WMI メソッドは、WMI クライアントに指定されたポートに関連付けられたイベントを渡すことを停止するように、WMI プロバイダーを構成します。
ms.assetid: 6e466a89-273b-4ed9-a0fe-5a8df745b28a
keywords:
- 記憶装置の RemovePort 関数
topic_type:
- apiref
api_name:
- RemovePort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ac9d2e8003a0eda0fc5788f26844d58d62c01e33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330047"
---
# <a name="removeport-function"></a>RemovePort 関数


**RemovePort** WMI メソッドを WMI クライアントに指定されたポートに関連付けられたイベントを渡すことを停止するように、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void RemovePort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN*   
イベントは、WMI クライアントに報告するポートの一覧から削除するポートを示す世界中の名前。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **RemovePort\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564017)構造体。

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
<td align="left">Hbapiwmi.h (Hbapiwmi.h、Hbaapi.h、Hbaapi.h など)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**RemovePort\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564014)

[**RemovePort\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff564017)

 

 






