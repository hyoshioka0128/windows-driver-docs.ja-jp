---
title: OID_WWAN_DEVICE_CAPS_EX
description: OID_WWAN_DEVICE_CAPS_EX は、OID_WWAN_DEVICE_CAPS から似ていますが、別の OID です。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_DEVICE_CAPS_EX、ex デバイスの機能、executor あたりの OID
ms.date: 04/04/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6c80b2e2426d94638857e3465d09667fe3c3f7ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362854"
---
# <a name="oidwwandevicecapsex"></a>OID\_WWAN\_デバイス\_CAP\_例


OID\_WWAN\_デバイス\_CAP\_EX がのような[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)実行プログラムあたり OID_WWAN_ とは異なり、OID が、これは、デバイスごとの OID DEVICE_CAPS します。 この OID を LTE 接続 APN 構成など、省略可能な機能の拡張機能を含む、ハードウェアのデバイス/実行プログラムの機能を示すためには機能します。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_デバイス\_CAP\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)状態通知を含む、 [ **NDIS\_WWAN\_デバイス\_CAP\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)を格納する構造体、 [ **WWAN\_デバイス\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps_ex)構造体には、デバイスの機能に関する情報を提供します。

次の図は、クエリ要求を示しています。

![実行プログラムの機能のクエリ](images/multi-SIM_6_executorCapabilityQuery.png)

要求のセットには適用されません。

<a name="remarks"></a>注釈
-------

レポート サービスの拡張機能を実際のデバイス ドライバーを含む全体にドライバーが重要です。 ドライバーは、サービスをサポートしている基になるハードウェアでサポートされていない場合は、サービスの機能は FALSE としてマークする必要があります。

OID\_WWAN\_デバイス\_CAP\_EX は各 executor の機能の取得にも使用されます。 この OID は、既存の構造で同じ[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)が追加の**Executor ID**します。 ミニポート ドライバーでは、最上位の OID バージョンがサポートを報告する必要があります。

同様[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)、SIM カードにより変更が選択された実行プログラムのモデムの RF の機能を表すではなくこの OID のパラメーターはありません。 物理ハードウェア モデムが複数の executor があり、そのため、OID をサポートする複数のインターフェイスを実装することがあります\_WWAN\_デバイス\_CAP\_エク.

今後の更新、OS の要求されたバージョンが、デバイスでサポートされているバージョンより新しい場合、デバイスはサポート OID 構造体の最新バージョンにする必要があります返します。 OS の要求されたバージョンが最新のデバイスでサポートされているものよりも古い場合は、デバイスは、OS の仕様に一致するバージョンを返す必要があります。 Ihv OID のすべての変更履歴を確認するための要件が\_WWAN\_デバイス\_CAP\_EX がサポートされているの下位互換性とレガシ サポートします。

その他の Oid を初めて使用する Windows 10 バージョン 1703 であるとは異なり、モデムがマルチ SIM/マルチ executor をサポートしている場合に必要なだけこの OID 実装する必要がある Windows 10 のバージョン以降では、Microsoft が定義したサービス拡張機能をサポートするモデム1703 します。

Windows 10 バージョン 1703 より前の Windows のバージョンがまだ既存を使用[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md); マルチ executor 対応モデムでの動作がサポートされているシナリオではありません。 Ihv は、この動作を定義する必要があります。

### <a name="windows-10-version-1903"></a>Windows 10 バージョン 1903

Windows 10、バージョンが 1903 年以降 OID_WWAN_DEVICE_CAPS_EX は、リビジョン 2 にアップグレードされています。 ミニポート ドライバーでは、この OID とミニポート ドライバーは、5 G をサポートしている場合が含まれているデータ構造体のリビジョン 2 を使用する必要があります。

この OID を使用してホストのクエリ機能、ミニポート ドライバーする必要がありますオンと基になるハードウェアが 5 G 携帯電話の機能をサポートしているかどうか。 ミニポート ドライバー対応するビットマスクを設定する場合は、 **WwanDataClass**のフィールド、 [ **WWAN_DEVICE_CAPS_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps_ex)ハードウェア 1,000万に従って構造体。

さらに、 **WwanOptionalServiceCaps**のフィールド、 **WWAN_DEVICE_CAPS_EX**すべての新しい 5 G に関連する拡張機能のサポートをカバーする構造体の新しい省略可能なサービスのビットが定義されています。

5 G データ クラスのサポートに関する詳細については、次を参照してください。 [MB 5 G データ クラスのサポート](mb-5g-data-class-support.md)します。

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


[OID\_WWAN\_デバイス\_キャップ](oid-wwan-device-caps.md)

[**NDIS\_状態\_WWAN\_デバイス\_CAP\_例**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)

[**NDIS\_WWAN\_デバイス\_CAP\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

[**WWAN\_デバイス\_CAP\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps_ex)



