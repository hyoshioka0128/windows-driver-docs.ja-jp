---
title: OID_WWAN_SYS_CAPS_INFO
description: OID_WWAN_SYS_CAPS_INFO は、モデムに関する情報を取得します。 このファイルは、モデムによって公開されている任意の NDIS インスタンスで送信できます。
ms.assetid: D158432A-A715-4ABB-969C-F8F80D2DB845
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_SYS_CAPS_INFO ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 1e7a427d5cb7372ef5d7675917dc31c6979013bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843777"
---
# <a name="oid_wwan_sys_caps_info"></a>OID\_WWAN\_SYS\_CAP\_情報


OID\_WWAN\_SYS\_CAP\_情報は、モデムに関する情報を取得します。 このファイルは、モデムによって公開されている任意の NDIS インスタンスで送信できます。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_STATUS\_を返してから、後で[**ndis\_ステータス\_WWAN\_SYS を送信する前に、元の要求に必要な\_を返します。CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)の状態通知。 [**NDIS\_WWAN\_SYS\_CAPS\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)構造体を含みます。これには、 [**WWAN\_SYS\_CAPS\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_sys_caps_info)構造体が含まれています。モデムシステムの全体的な機能に関する情報を提供します。

次の図は、クエリ要求を示しています。

![システム機能クエリ](images/multi-SIM_5_systemCapabilityQuery.png)

Set 要求は適用できません。

<a name="remarks"></a>注釈
-------

ホストは、OID\_WWAN\_SYS\_CAPS\_INFO を使用して、モデムのデバイス数 (実行プログラム) とスロット、および同時にアクティブになっている可能性がある実行プログラムの数を照会します。 デュアルスタンバイモデムの同時実行性は1です。デュアルアクティブモデムでは、同時実行性が2になります。 この OID は実行プログラム固有ではなく、どの NDIS インスタンスにも送信される可能性があります。

このモデムでは、複数の構成が発生する可能性があります。 どの構成が選択されているかにかかわらず、このクエリは、現在構成されているとおりにモデムがサポートできるデバイスとスロットの最大数を返します。

OID\_WWAN\_SYS\_CAPS\_情報をサポートするモデムは、Oid\_[wwan\_デバイス\_cap\_EX](oid-wwan-device-caps-ex.md)もサポートする必要があります。 マルチ実行プログラムをサポートしている Windows のバージョンでは、基になるモデムが OID\_WWAN\_SYS\_CAPS\_INFO をサポートしている場合は、従来の[oid\_wwan\_デバイス\_cap](oid-wwan-device-caps.md)を使用しません。 以前のバージョンの OS (この OID のために Windows 10 バージョン1703より前のバージョン) では、マルチ実行プログラムモデムは複数の独立したモデムとして表され、既存の OID\_WWAN\_デバイス\_CAP、利用可能Windows 8 以降では、が使用されます。

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
<td><p>Windows 10 バージョン1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ステータス\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

[**WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_sys_caps_info)

[OID\_WWAN\_デバイス\_CAP\_EX](oid-wwan-device-caps-ex.md)

[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)

 

 




