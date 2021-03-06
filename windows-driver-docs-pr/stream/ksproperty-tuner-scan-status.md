---
title: KSPROPERTY\_チューナー\_スキャン\_状態
description: KSPROPERTY\_チューナー\_スキャン\_STATUS プロパティは、スキャン操作の状態をについて説明します。 このプロパティは、必要に応じて実装できます。
ms.assetid: ce7dd30b-84fc-46e2-847c-33c07e60e0f7
keywords:
- KSPROPERTY_TUNER_SCAN_STATUS ストリーミング メディア デバイス
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
ms.openlocfilehash: eefa78f154e9782c32179320f2c92eda302baf48
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355969"
---
# <a name="kspropertytunerscanstatus"></a>KSPROPERTY\_チューナー\_スキャン\_状態


KSPROPERTY\_チューナー\_スキャン\_STATUS プロパティは、スキャン操作の状態をについて説明します。 このプロパティは、必要に応じて実装できます。

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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)"><strong>KSPROPERTY_TUNER_SCAN_STATUS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_STATUS_S</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_チューナー\_スキャン\_状態\_構造をスキャン操作の状態を指定します。

<a name="remarks"></a>注釈
-------

*KsTvTune.ax*モジュールは、ドライバーの KSPROPERTY を呼び出すことができます\_チューナー\_スキャン\_いつでも STATUS プロパティ。 ただし、 *KsTvTune.ax*は KSPROPERTY\_チューナー\_スキャン\_ステータスを呼び出した後、 [ **KSEVENT\_チューナー\_開始\_スキャン**](ksevent-tuner-initiate-scan.md)イベント スキャン操作を設定して、スキャンが完了したときの通知を設定します。 *KsTvTune.ax*スキャン完了通知を発生を待ちます。 最悪のシナリオとして*KsTvTune.ax*で指定されている時間にわたって待機、 **SettlingTime**のメンバー、 [**チューナー\_アナログ\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tuner_analog_caps_s)構造体。 データが設定されたチューナーのドライバーが返されますが\_アナログ\_CAP\_への呼び出しからその[ **KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP** ](ksproperty-tuner-networktype-scan-caps.md)アナログ プロパティ\_テレビ\_ネットワーク\_型の値の設定、 **NetworkType**のメンバー、 [ **KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)構造体。 ただし、チューナーでする必要がありますで指定されている時間よりも高速のシグナルの状態を確認通常**SettlingTime**し、その後に通知する必要があります*KsTvTune.ax*でスキャンが完了します。イベントを通知します。

ドライバーは、チューニングのデバイスがハードウェア依存のスキャンをサポートしている場合にのみのスキャン状態を返します。 ドライバーを設定してこのようなサポートを示します、 **fSupportsHardwareAssistedScanning**のメンバー、 [ **KSPROPERTY\_チューナー\_スキャン\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)構造体を**TRUE**への呼び出しでその[ **KSPROPERTY\_チューナー\_スキャン\_CAP**](ksproperty-tuner-scan-caps.md)プロパティ。 ドライバーは、イベントを通知しで次のロックの種類のいずれかを返す必要があります、 **LockStatus**のメンバー、 [ **KSPROPERTY\_チューナー\_スキャン\_の状態\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)構造体。

-   **チューナー\_LockType\_None**チューニング デバイスでした、信号をまったく見つけられない場合。

-   **チューナー\_LockType\_ロック**正確な頻度にチューニングのデバイスがロックされている場合。

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
<td><p>Windows Vista およびそれ以降のバージョンのオペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSEVENT\_チューナー\_開始\_スキャン**](ksevent-tuner-initiate-scan.md)

[**KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_キャップ**](ksproperty-tuner-networktype-scan-caps.md)

[**KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)

[**KSPROPERTY\_チューナー\_スキャン\_キャップ**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY\_チューナー\_スキャン\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

[**KSPROPERTY\_チューナー\_スキャン\_状態\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)

[**チューナー\_アナログ\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tuner_analog_caps_s)

 

 






