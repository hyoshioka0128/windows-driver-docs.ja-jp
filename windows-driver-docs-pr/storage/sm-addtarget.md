---
title: SM\_AddTarget 関数
description: SM\_AddTarget WMI メソッドを WMI クライアントに指定されたターゲットに関連付けられているイベントを通知するために、WMI プロバイダーを構成します。
ms.assetid: 78e19496-1eb0-4d05-8637-f2e6d123208b
keywords:
- 記憶装置の SM_AddTarget 関数
topic_type:
- apiref
api_name:
- SM_AddTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c9a6e693b3b4cdabb27426c1b2453d3f382af595
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384319"
---
# <a name="smaddtarget-function"></a>SM\_AddTarget 関数


SM\_AddTarget WMI メソッドを WMI クライアントに指定されたターゲットに関連付けられているイベントを通知するために、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_AddTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DomainPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
世界中のローカル ポート WMI クライアントは、イベント名 (WWN)

*DiscoveredPortWWN*   
検出したターゲットを持つイベントを指定する世界中の名 (WWN)、WMI クライアントが表示されます。

*DomainPortWWN*   
WMI クライアントは、イベントのローカル ポートの SAS のドメイン世界中の名前を指定する世界名 (WWN)。

*AllTargets*   
レポートを対象のイベントのスコープです。 このメンバーがゼロの場合、WMI クライアントは DiscoveredPortWWN で示されたポートに関連付けられているイベントを受け取ります。 このメンバーが 0 以外の場合は、WMI クライアントは、すべての検出された現在のターゲットとして後で、検出されたターゲットに関連付けられているすべてのイベントを受け取ります。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_AddTarget\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_EventControl WMI クラスです。

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

[**SM\_AddTarget\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_addtarget_in)

[**SM\_AddTarget\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_addtarget_out)

 

 






