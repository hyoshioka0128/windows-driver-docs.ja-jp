---
title: RemoveTarget 関数
description: RemoveTarget WMI メソッドは、指定されたターゲットに関連付けられたイベントが WMI クライアントに渡されるのを停止するように、WMI プロバイダーを構成します。
ms.assetid: 413cee3c-5e3a-4012-925b-b4699fbd2e1b
keywords:
- RemoveTarget 関数のストレージデバイス
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
ms.openlocfilehash: ebab0c1eaae0936aaff6b04db55726cfd5976eb0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842700"
---
# <a name="removetarget-function"></a>RemoveTarget 関数


**Removetarget** wmi メソッドは、指定されたターゲットに関連付けられたイベントが wmi クライアントに渡されるのを停止するように、wmi プロバイダーを構成します。

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
イベントが WMI クライアントに報告されるポートの一覧から削除するローカルポートを一意に識別する、64ビットのワールドワイド名 (WWN)。 全世界の名前の詳細については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。

*DiscoveredPortWWN*   
イベントが WMI クライアントに報告されるポートの一覧から削除する必要がある、検出されたリモートポートを示す WWN。

*Alltargets*   
レポートを停止するイベント。 このメンバーがゼロの場合、WMI プロバイダークライアントは、 *DiscoveredPortWWN*によって示されるポートに関連付けられたイベントの報告を停止します。 このメンバーが0以外の場合、WMI プロバイダーは、任意のターゲットに関連付けられているすべてのイベントのレポートを停止します。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Removetarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removetarget_out)構造の**hbastatus**メンバーでこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_EventControl WMI クラス](msfc-eventcontrol-wmi-class.md)に属しています。

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
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**RemoveTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removetarget_in)

[**RemoveTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removetarget_out)

 

 






