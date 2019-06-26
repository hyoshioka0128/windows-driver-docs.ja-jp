---
title: RemoveTarget 関数
description: RemoveTarget WMI メソッドは、WMI クライアントに指定されたターゲットに関連付けられたイベントを渡すことを停止するように、WMI プロバイダーを構成します。
ms.assetid: 413cee3c-5e3a-4012-925b-b4699fbd2e1b
keywords:
- 記憶装置の RemoveTarget 関数
topic_type:
- apiref
api_name:
- RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 130a61c45e1adc3a0e420417091e2b0145956829
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368908"
---
# <a name="removetarget-function"></a>RemoveTarget 関数


**RemoveTarget** WMI メソッドを WMI クライアントに指定されたターゲットに関連付けられたイベントを渡すことを停止するように、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void RemoveTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
64 ビット世界名 (WWN) イベントは、WMI クライアントに報告するポートの一覧から削除するローカル ポートを一意に識別します。 世界中の名の詳細については、T11 委員会を参照してください。*ファイバー チャネル HBA API*仕様。

*DiscoveredPortWWN*   
イベントは、WMI クライアントに報告するポートの一覧から削除するか、リモート検出されたポートを示す WWN します。

*AllTargets*   
レポートを停止するイベントです。 このメンバーが 0 の場合は、WMI プロバイダーのクライアントはレポートで示されたポートに関連付けられたイベントに停止*DiscoveredPortWWN*します。 このメンバーが 0 以外の場合は、WMI プロバイダーは任意のターゲットがすべてのイベントに関連付けられているレポートを停止します。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **RemoveTarget\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_removetarget_out)構造体。

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


[**RemoveTarget\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_removetarget_in)

[**RemoveTarget\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_removetarget_out)

 

 






