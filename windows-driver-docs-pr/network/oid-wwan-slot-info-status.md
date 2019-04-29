---
title: OID_WWAN_SLOT_INFO
description: OID_WWAN_SLOT_INFO は、UICC の指定されたスロットと (必要な場合) 内でカードの高度な集計の状態を取得します。 スロットのいずれかの状態が変更されたときに、請求の通知を配信するも使用可能性があります。
ms.assetid: 6267D480-5055-4A7A-B2A0-F4DF9154DCD7
ms.date: 08/08/2017
keywords: -OID_WWAN_SLOT_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 19e0ebe37bbed5dee1d598060a7f5b029216b739
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392399"
---
# <a name="oidwwanslotinfo"></a>OID\_WWAN\_スロット\_情報


OID\_WWAN\_スロット\_(あれば) 情報を指定 UICC スロットとその中のカードの高度な集計の状態を取得します。 スロットのいずれかの状態が変更されたときに、請求の通知を配信するも使用可能性があります。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782398)状態通知を含む、 [ **NDIS\_WWAN\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782408)を格納する構造体、 [ **WWAN\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt799892)構造に関する情報を提供しますモデム システムの全体的な機能です。

クエリ要求を指定[ **NDIS\_WWAN\_取得\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782404)入力として構造体します。 ミニポート ドライバーで ID が指定されたスロットに従ってスロットの状態を返す必要があります、 **SlotIndex**のメンバー、 [ **WWAN\_取得\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt799891)構造体。

次の図は、クエリ要求を示しています。

![スロットの状態のクエリ](images/multi-SIM_9_slotStatusQuery.png)

要求のセットには適用されません。

[ **NDIS\_状態\_WWAN\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782398)通知と共に、 [ **NDIS\_WWAN\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782408)構造がスロット/カードの状態が変更されたときのホストに送信されます。

<a name="remarks"></a>注釈
-------

ホストが OID を使用して\_WWAN\_スロット\_モデムの特定のスロットの状態を照会するには情報。 この OID は、executor 固有ではないと、1 つのモデムに属する任意の NDIS インスタンスに送信する場合があります。 スロットの状態は、スロットとカードの両方の状態の概要を表します。

報告される状態のセットは、スロットのハードウェアの機能によって制限されます。 最も制限の厳しい場合、スロット ハードウェアできる場合がありますのみ、カードが入ってときに存在しアクティブでことを確認する: このような場合、 **OffEmpty**と**オフ**状態は報告されません。

[OID\_WWAN\_準備\_情報](oid-wwan-ready-info.md)と OID\_WWAN\_スロット\_情報 SIM カードのスロット以外のデバイスの準備完了状態を取得するのと同じコア関数の実行、OID\_WWAN\_準備\_情報は、executor あたりのコマンドを OID\_WWAN\_スロット\_情報は、物理インスタンス (エグゼキュータ) で使用可能でありを返します、現時点ですべての executor にマップされていない場合でも適切なスロットの状態。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_STATUS\_WWAN\_SLOT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt782398)

[**NDIS\_WWAN\_SLOT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt782408)

[**WWAN\_SLOT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt799892)

[**NDIS\_WWAN\_GET\_SLOT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt782404)

[**WWAN\_GET\_SLOT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt799891)

[**WWAN\_UICCSLOT\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt799894)

[OID\_WWAN\_準備\_情報](oid-wwan-ready-info.md)

 

 




