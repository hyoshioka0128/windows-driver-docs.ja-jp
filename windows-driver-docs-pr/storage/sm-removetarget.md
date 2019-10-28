---
title: SM\_RemoveTarget 関数
description: SM\_RemoveTarget WMI メソッドを使用すると、指定されたターゲットに関連付けられているイベントが WMI クライアントに渡されなくなるように WMI プロバイダーが構成されます。
ms.assetid: 9be2a40c-299a-4d92-b9a2-ef60eb6d90e9
keywords:
- SM_RemoveTarget function Storage デバイス
topic_type:
- apiref
api_name:
- SM_RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7c1b05b21b799385f821fa961068c5dfbcf09562
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845472"
---
# <a name="sm_removetarget-function"></a>SM\_RemoveTarget 関数


SM\_RemoveTarget WMI メソッドを使用すると、指定されたターゲットに関連付けられているイベントが WMI クライアントに渡されなくなるように WMI プロバイダーが構成されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_RemoveTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
イベントが WMI クライアントに報告されるポートの一覧から削除するローカルポートを一意に識別する、64ビットのワールドワイド名 (WWN)。 全世界の名前の詳細については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。

*DiscoveredPortWWN*   
イベントが WMI クライアントに報告されるポートの一覧から削除する必要がある、リモートで検出されたポートを示すワールドワイド名 (WWN)。

*Alltargets*   
レポートを停止するイベント。 このメンバーがゼロの場合、WMI プロバイダークライアントは、DiscoveredPortWWN によって示されたポートに関連付けられているイベントの報告を停止します。 このメンバーが0以外の場合、WMI プロバイダーは、すべてのターゲットに関連付けられているすべてのイベントの報告を停止します。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_RemoveTarget\_OUT 構造の HBAStatus メンバーにこの情報を返します。

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

[**SM\_RemoveTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removetarget_in)

[**SM\_RemoveTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removetarget_out)

 

 






