---
title: SM\_AddTarget 関数
description: SM\_AddTarget WMI メソッドは、指定されたターゲットに関連付けられているイベントを WMI クライアントに通知するように WMI プロバイダーを構成します。
ms.assetid: 78e19496-1eb0-4d05-8637-f2e6d123208b
keywords:
- SM_AddTarget 関数記憶装置
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
ms.openlocfilehash: 800cadec0c88d95eff0f2e6717d1b69840b77155
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842602"
---
# <a name="sm_addtarget-function"></a>SM\_AddTarget 関数


SM\_AddTarget WMI メソッドは、指定されたターゲットに関連付けられているイベントを WMI クライアントに通知するように WMI プロバイダーを構成します。

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
WMI クライアントが受信するイベントを持つローカルポートのワールドワイド名 (WWN)。

*DiscoveredPortWWN*   
WMI クライアントが受信するイベントの検出されたターゲットを指定するワールド名 (WWN)。

*DomainPortWWN*   
WMI クライアントが受け取るイベントを持つローカルポートの、世界中の SAS ドメイン名を指定する、ワールドワイド名 (WWN)。

*Alltargets*   
報告するターゲットイベントのスコープ。 このメンバーがゼロの場合、WMI クライアントは、DiscoveredPortWWN によって示されるポートに関連付けられているイベントを受信します。 このメンバーが0以外の場合、WMI クライアントは、現在検出されているすべてのターゲットと、今後検出されるターゲットに関連付けられているすべてのイベントを受信します。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_AddTarget\_OUT 構造の HBAStatus メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_EventControl WMI クラスに属しています。

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

[**SM\_AddTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addtarget_in)

[**SM\_AddTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addtarget_out)

 

 






