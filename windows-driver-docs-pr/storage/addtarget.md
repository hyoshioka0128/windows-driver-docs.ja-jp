---
title: AddTarget 関数
description: AddTarget WMI メソッドは、WMI クライアントに指定されたターゲットに関連付けられているイベントを通知するために、WMI プロバイダーを構成します。
ms.assetid: 9aac339b-a9b4-4de7-99dd-fa5f8889a686
keywords:
- 記憶装置の AddTarget 関数
topic_type:
- apiref
api_name:
- AddTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 74d39de161128efbbb40607063bc0d3a085e72e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362684"
---
# <a name="addtarget-function"></a>AddTarget 関数


**AddTarget** WMI メソッドを WMI クライアントに指定されたターゲットに関連付けられているイベントを通知するために、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void AddTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN\[8\]*    
ローカル ポートがイベントを WMI クライアントは、世界中の名前。

*DiscoveredPortWWN\[8\]*    
世界中の名前、検出したターゲットを持つイベントを指定する WMI クライアントが表示されます。

*AllTargets*   
レポートを対象のイベントのスコープです。 このメンバーが 0 の場合は、WMI クライアントがで示されたポートに関連付けられたイベントを受け取ります*DiscoveredPortWWN*します。 このメンバーが 0 以外の場合は、WMI クライアントはすべての検出された現在のターゲットとして後で、検出されたターゲットに関連付けられているすべてのイベントを受信します。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **AddTarget\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_addtarget_out)構造体。

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


[**AddTarget\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_addtarget_in)

[**AddTarget\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_addtarget_out)

 

 






