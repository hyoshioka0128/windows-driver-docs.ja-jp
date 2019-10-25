---
title: AddTarget 関数
description: AddTarget WMI メソッドは、指定されたターゲットに関連付けられているイベントを WMI クライアントに通知するように WMI プロバイダーを構成します。
ms.assetid: 9aac339b-a9b4-4de7-99dd-fa5f8889a686
keywords:
- AddTarget 関数のストレージデバイス
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
ms.openlocfilehash: dce95704322cc9ea0eae5a3f0f48ff8ea99396aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845109"
---
# <a name="addtarget-function"></a>AddTarget 関数


**Addtarget** wmi メソッドは、指定されたターゲットに関連付けられているイベントを wmi クライアントに通知するように wmi プロバイダーを構成します。

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
WMI クライアントが受け取るイベントを持つローカルポートの世界規模の名前。

*DiscoveredPortWWN\[8\]*    
WMI クライアントが受け取るイベントの検出されたターゲットを指定する世界的な名前。

*Alltargets*   
報告するターゲットイベントのスコープ。 このメンバーがゼロの場合、WMI クライアントは、 *DiscoveredPortWWN*によって示されるポートに関連付けられたイベントを受け取ります。 このメンバーが0以外の場合、WMI クライアントは、現在検出されているすべてのターゲットに関連付けられているすべてのイベントと、今後検出されるターゲットを受け取ります。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Addtarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addtarget_out)構造体の**hbastatus**メンバーにこの情報を返します。

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


[**AddTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addtarget_in)

[**AddTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addtarget_out)

 

 






