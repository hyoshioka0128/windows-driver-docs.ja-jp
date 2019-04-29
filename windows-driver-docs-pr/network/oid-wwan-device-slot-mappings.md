---
title: OID_WWAN_DEVICE_SLOT_MAPPING_INFO
description: OID_WWAN_DEVICE_SLOT_MAPPING_INFO を設定または MB デバイス (つまり、executor スロット マッピング) のデバイスのスロットのマッピングを返します。
ms.assetid: 54AF3447-7918-49CE-945A-DC8DC1E78CBF
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SLOT_MAPPING_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: aecf6883c3ec790778ff1c86e5c32e1d04cf73b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386681"
---
# <a name="oidwwandeviceslotmappinginfo"></a>OID\_WWAN\_デバイス\_スロット\_マッピング\_情報


OID\_WWAN\_デバイス\_スロット\_マッピング\_情報が (つまり、executor スロット マッピング) MB デバイスのデバイスのスロットのマッピングを取得または設定します。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782397)状態通知を含む、 [ **NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782403) executor、スロットのマッピングに関する情報を提供する構造体。

次の図は、クエリ要求を示しています。

![スロットのマッピングのクエリ](images/multi-SIM_8_slotMappingQuery.png)

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782397)状態通知を含む、 [ **NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782403)を格納する構造体、 [ **WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt799890)構造体を現在のマッピングの状態を示します。 これは、セットの要求が失敗した場合でもは、true を保持します。 OID のセット要求、構造体の\_WWAN\_デバイス\_スロット\_マッピング\_情報[ **NDIS\_WWAN\_設定\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782405)します。

次の図は、セットの要求を示しています。

![スロットのマッピングの設定](images/multi-SIM_7_slotMappingSet.png)

<a name="remarks"></a>注釈
-------

ホストは、最初の起動時に、モデム必要があるスロットと executor の既定のマッピングが必要です。 ホストは OID. 1.3 で設定操作を実行します\_WWAN\_デバイス\_スロット\_マッピング\_各 executor にバインドされているスロットを定義する情報。 ホストが再起動し、削除/挿入の間でマッピングを維持するために、モデムが必要です。 この OID は、executor 固有ではないと、デバイス上の任意の NDIS インスタンスに送信できます。 現在のマッピングは、上記のようにもクエリー可能性があります。

<a name="requirements"></a>必要条件
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


[**NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782397)

[**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782403)

[**NDIS\_WWAN\_設定\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782405)

 

 




