---
title: KSK プロパティ\_チューナー\_スキャン\_状態
description: KSK プロパティ\_チューナー\_SCAN\_STATUS プロパティは、スキャン操作の状態を示します。 このプロパティは、必要に応じて実装できます。
ms.assetid: ce7dd30b-84fc-46e2-847c-33c07e60e0f7
keywords:
- KSPROPERTY_TUNER_SCAN_STATUS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_SCAN_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c06b6766e4ea3833714e08661a4ab19e67c74e1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837903"
---
# <a name="ksproperty_tuner_scan_status"></a>KSK プロパティ\_チューナー\_スキャン\_状態


KSK プロパティ\_チューナー\_SCAN\_STATUS プロパティは、スキャン操作の状態を示します。 このプロパティは、必要に応じて実装できます。

### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>セット</th>
<th>的を絞る</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>ピン</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)"><strong>KSPROPERTY_TUNER_SCAN_STATUS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_STATUS_S</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、\_チューナー\_スキャン\_状態\_S のスキャン操作の状態を指定する、KSK プロパティです。

<a name="remarks"></a>解説
-------

*KsTvTune.ax*モジュールは、ドライバーの ksk プロパティ\_チューナー\_SCAN\_STATUS プロパティをいつでも呼び出すことができます。 ただし、 *KsTvTune.ax*は、通常、 [**KSEVENT\_\_チューナー**](ksevent-tuner-initiate-scan.md)を呼び出した後に\_の状態を\_スキャンし、スキャン操作を設定して、いつでも通知を設定するために、ksk プロパティ\_チューナーを呼び出します。スキャンが完了します。\_ *KsTvTune.ax*は、スキャン完了通知が発生するまで待機します。 最悪のシナリオとして、 *KsTvTune.ax*は、チューナーの**sett time**メンバーに指定されている時間が経過すると、[**アナログ\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)構造体\_待機します。 このドライバーは、アナログ\_TV\_ネットワークを使用して、 [ **\_の Ksk プロパティチューナー\_NETWORKTYPE\_SCAN\_caps**](ksproperty-tuner-networktype-scan-caps.md)プロパティへの呼び出しから、入力されたチューナー\_アナログ\_Cap\_S を返しました @no[**Ksk プロパティ\_チューナー\_NetworkType\_SCAN\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)構造体の**NetworkType**メンバーで設定されている、__ 型の値を設定します。\_ ただし、一般に、チューナーは、通常の**時間に指定**された時間よりも速く信号の状態を判断する必要があります。その後、イベントを通知して、スキャンが完了したことを*KsTvTune.ax*に通知する必要があります。

ドライバーは、チューニングデバイスでハードウェア支援型のスキャンがサポートされている場合にのみスキャン状態を返します。 このドライバーは、ksk プロパティの**fSupportsHardwareAssistedScanning**メンバー [ **\_チューナー\_スキャン\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)構造体を**TRUE**に設定することによって、このようなサポートを示してい[ **\_チューナー\_スキャン\_CAPS**](ksproperty-tuner-scan-caps.md)プロパティ。 ドライバーは、イベントを通知し、次のロックの種類のいずれかを返す必要があります\_チューナーは、Ksk プロパティの**Lockstatus**メンバー [ **\_スキャン\_状態\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)構造です。

-   **[チューナー\_LockType]\_** 、チューニングデバイスが信号をまったく検出できなかった場合には None です。

-   チューニングデバイスが正確な頻度にロックされている場合、**チューナー\_LockType\_ロック**されています。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンのオペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>ヘッダー</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSEVENT\_チューナー\_\_スキャンを開始します**](ksevent-tuner-initiate-scan.md)

[**KSK プロパティ\_チューナー\_NETWORKTYPE\_SCAN\_CAPS**](ksproperty-tuner-networktype-scan-caps.md)

[**KSK プロパティ\_チューナー\_NETWORKTYPE\_スキャン\_キャップ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)

[**KSK プロパティ\_チューナー\_スキャン\_CAPS**](ksproperty-tuner-scan-caps.md)

[**KSK プロパティ\_チューナー\_スキャン\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

[**KSK プロパティ\_チューナー\_スキャン\_状態\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)

[**チューナー\_アナログ\_キャップ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)

 

 






