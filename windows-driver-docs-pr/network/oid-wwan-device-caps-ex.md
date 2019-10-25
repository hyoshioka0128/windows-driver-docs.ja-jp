---
title: OID_WWAN_DEVICE_CAPS_EX
description: OID_WWAN_DEVICE_CAPS_EX は、OID_WWAN_DEVICE_CAPS とは似ていますが異なる OID です。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_DEVICE_CAPS_EX、実行プログラムごとの OID、デバイス機能 EX
ms.date: 04/04/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 849bed7c32575b91cdd9f428fd129116c2925915
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843863"
---
# <a name="oid_wwan_device_caps_ex"></a>OID\_WWAN\_デバイス\_CAP\_EX


OID\_WWAN\_デバイス\_CAPS\_EX は[oid\_WWAN\_デバイス\_cap](oid-wwan-device-caps.md)と似ていますが、デバイスごとの oid である OID_WWAN_DEVICE_CAPS とは異なり、実行プログラムごとの oid です。 この OID は、ハードウェアのデバイス/実行プログラムの機能を示すために機能します。これには、LTE attach APN 構成などの拡張オプション機能の機能が含まれます。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_状態\_を返してから、後で[**ndis\_ステータス\_WWAN\_デバイスを送信する前に、元の要求に必要な\_を返します。8_ CAPS\_EX**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)状態通知。 [**NDIS\_WWAN\_デバイス\_CAPS\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)構造体を含みます。これには、 [**WWAN\_DEVICE\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)構造体が含まれています。デバイスの機能に関する情報を提供します。

次の図は、クエリ要求を示しています。

![実行プログラムの機能のクエリ](images/multi-SIM_6_executorCapabilityQuery.png)

Set 要求は適用できません。

<a name="remarks"></a>注釈
-------

ドライバーがサービス拡張機能を全体として報告することは、ドライバーから実際のデバイスまでということが重要です。 ドライバーがサービスをサポートしていても、基になるハードウェアでサポートされていない場合は、サービス機能を FALSE としてマークする必要があります。

OID\_WWAN\_デバイス\_CAPS\_EX は、各実行プログラムの機能を取得するためにも使用されます。 この OID は、既存の[oid\_WWAN\_デバイス\_cap](oid-wwan-device-caps.md)と同じ構造で、実行**プログラム ID**が追加されています。 ミニポートドライバーは、サポートされている最も高い OID バージョンを報告する必要があります。

[Oid\_WWAN\_デバイス\_cap](oid-wwan-device-caps.md)の場合と同様に、この OID のパラメーターは SIM カードによって変更されることはありませんが、選択された実行プログラムのモデムの RF 機能を表します。 物理ハードウェアモデムには複数のエグゼキュータが存在する場合があります。したがって、OID\_WWAN\_デバイス\_CAP\_EX をサポートする複数のインターフェイスが存在する可能性があります。

将来の更新では、OS の要求されたバージョンがデバイスでサポートされているバージョンより新しい場合、デバイスはサポートしている OID 構造の最新バージョンを返す必要があります。 OS の要求されたバージョンがデバイスでサポートされている最新のバージョンより古い場合、デバイスは OS の仕様に一致するバージョンを返す必要があります。 \_デバイス\_CAP\_EX のすべて\_のリビジョンが旧バージョンとの互換性のためにサポートされているかどうかを確認するために、Ihv が必要としています。

モデムがマルチ SIM/マルチ実行プログラムをサポートしている場合にのみ必要な Windows 10 バージョン1703に新しく追加された Oid とは異なり、この OID は、Windows 10 バージョン以降で Microsoft が定義したサービス拡張機能をサポートする必要があるモデムに実装する必要があります。1703。

Windows 10 バージョン1703より前のバージョンの Windows でも、既存の[OID\_WWAN\_デバイス\_cap](oid-wwan-device-caps.md)が使用される場合があります。マルチ実行プログラム対応モデムでの動作は、サポートされるシナリオではありません。 Ihv はこの動作を定義する必要があります。

### <a name="windows-10-version-1903"></a>Windows 10 バージョン 1903

Windows 10 バージョン1903以降では、OID_WWAN_DEVICE_CAPS_EX はリビジョン2にアップグレードされました。 ミニポートドライバーは、この OID のリビジョン2と、ミニポートドライバーが5G をサポートしている場合に含まれるデータ構造を使用する必要があります。

ホストがこの OID を使用して機能を照会する場合、ミニポートドライバーは、基になるハードウェアが5G 携帯電話機能をサポートしているかどうかを確認する必要があります。 その場合、ミニポートドライバーは、ハードウェアできに従って、 [**WWAN_DEVICE_CAPS_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)構造体の**WwanDataClass**フィールドにビットマスクを設定します。

さらに、 **WWAN_DEVICE_CAPS_EX**構造体の**WwanOptionalServiceCaps**フィールドには、新しい5G 関連の拡張機能のサポートを対象とする新しいオプションのサービスビットが定義されています。

5G data クラスのサポートの詳細については、「 [MB 5G データクラスのサポート](mb-5g-data-class-support.md)」を参照してください。

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


[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)

[**NDIS\_ステータス\_WWAN\_デバイス\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)

[**NDIS\_WWAN\_デバイス\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

[**WWAN\_デバイス\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)



