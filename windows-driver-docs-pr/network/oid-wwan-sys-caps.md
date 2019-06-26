---
title: OID_WWAN_SYS_CAPS_INFO
description: OID_WWAN_SYS_CAPS_INFO では、モデムに関する情報を取得します。 モデムによって公開される NDIS インスタンスのいずれかに送信できます。
ms.assetid: D158432A-A715-4ABB-969C-F8F80D2DB845
ms.date: 08/08/2017
keywords: -OID_WWAN_SYS_CAPS_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dafacd0c537322ea57ad67e993dc002cbe9bb822
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372498"
---
# <a name="oidwwansyscapsinfo"></a>OID\_WWAN\_SYS\_CAP\_情報


OID\_WWAN\_SYS\_CAP\_INFO モデムについての情報を取得します。 モデムによって公開される NDIS インスタンスのいずれかに送信できます。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)状態通知を含む、 [ **NDIS\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)を格納する構造体、 [ **WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_sys_caps_info)構造体には、全体的なモデム システムの機能に関する情報を提供します。

次の図は、クエリ要求を示しています。

![システムの機能のクエリ](images/multi-SIM_5_systemCapabilityQuery.png)

要求のセットには適用されません。

<a name="remarks"></a>注釈
-------

ホストが OID を使用して\_WWAN\_SYS\_CAP\_デバイス (実行プログラム) とモデムのスロットの数と同時にアクティブにできる executor の数を照会するには情報。 デュアル スタンバイ モデムが 1 の同時実行性が必要があります。デュアル アクティブ モデムには、2 の同時実行性があります。 この OID は、executor 固有ではないと、任意の NDIS インスタンスに送信することがあります。

モデムは、executor とスロットの数が異なるで複数の構成を公開できます。 構成を選択するに関係なく、このクエリはデバイスとは、現在構成されているモデムをサポートするスロットの最大数を返します。

OID をサポートしているモデム\_WWAN\_SYS\_CAP\_情報がサポートすることも想定[OID\_WWAN\_デバイス\_CAP\_EX](oid-wwan-device-caps-ex.md). マルチ executor モデムをサポートする Windows のバージョンでは、従来は使用しません[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)基になるモデムに OID がサポートしている場合\_WWAN\_SYS\_CAP\_情報。 従来のバージョンの OS (任意のバージョン Windows 10 バージョン 1703 の前にこの OID の目的で) では、マルチ executor モデムを複数の独立したモデムと既存の OID として示されます\_WWAN\_デバイス\_CAP使用可能な Windows 8 以降が使用されます。

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


[**NDIS\_状態\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

[**WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_sys_caps_info)

[OID\_WWAN\_デバイス\_CAP\_例](oid-wwan-device-caps-ex.md)

[OID\_WWAN\_デバイス\_キャップ](oid-wwan-device-caps.md)

 

 




