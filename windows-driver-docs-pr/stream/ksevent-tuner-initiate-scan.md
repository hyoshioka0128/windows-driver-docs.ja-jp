---
title: KSEVENT\_チューナー\_\_スキャンを開始します
description: KSEVENT\_チューナー\_は、ドライバーがスキャン操作を開始したことを示す\_イベント要求を開始し、ドライバーに関連付けられているチューニングデバイスがスキャン操作を完了したときにユーザーモードクライアントに通知します。
ms.assetid: 63f6917e-30d2-4734-92fa-49a4291efafd
keywords:
- KSEVENT_TUNER_INITIATE_SCAN ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_TUNER_INITIATE_SCAN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ab636034238f8f3a1d5616767a13910bb3b8b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844921"
---
# <a name="ksevent_tuner_initiate_scan"></a>KSEVENT\_チューナー\_\_スキャンを開始します


KSEVENT\_チューナー\_は、ドライバーがスキャン操作を開始したことを示す\_イベント要求を開始し、ドライバーに関連付けられているチューニングデバイスがスキャン操作を完了したときにユーザーモードクライアントに通知します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>イベント記述子の種類</th>
<th>イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)"><strong>KSEVENT_TUNER_INITIATE_SCAN_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

スキャン要求はすべて、非ブロッキングである必要があります。 つまり、ドライバーはスキャン操作が完了するのを待たずに制御を戻します。 実際、ドライバーはスキャン操作を実行するために別のスレッドを使用する必要があります。

KSEVENT\_チューナー\_開始\_SCAN イベントは、 [ **\_チューナー\_FREQUENCY**](ksproperty-tuner-frequency.md)、KSEVENT\_チューナーに依存しませんが、は KS\_チューナーに対応し\_**t_12_ チューニング\_** Ksk プロパティの**Tuningflags**メンバー [ **\_チューナー\_FREQUENCY\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)構造体の正確なチューニングフラグです。 つまり、スキャンは常に次のチャネルの正確な周波数を判断しようとします。 また、チューニングデバイスが従うチューニング戦略はドライバー (KS\_チューナー\_戦略\_\_ドライバーによって制御されます。**これは、** [**KSK プロパティ\_チューナー\_MODE\_MODE のメンバーからチューニングされます。\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)構造体)。 これらの固定フラグと戦略は、異なるフラグと戦略を使用して**Ksk プロパティ\_チューナーの\_頻度**を制御している場合でも常に続きます。

つまり、KSTUNER\_チューニング\_フラグと KSTUNER\_戦略の値は、\_スキャンの開始\_KSEVENT\_チューナーの動作には影響しません。

***<em>完了と状態</em>***

スキャン状態プロパティ[**ksproperty\_チューナー\_スキャン\_ステータス**](ksproperty-tuner-scan-status.md)には、現在の頻度とシグナルロックの状態に関する情報が表示されます。 アプリケーションは、KSK プロパティ\_チューナー\_SCAN\_STATUS プロパティからロックの状態を照会します。 また、アプリケーションは、 [**Ksk プロパティ\_チューナー\_標準\_モード**](ksproperty-tuner-standard-mode.md)プロパティにクエリを行い、自動シグナル標準の検出に関する情報を検索します。 要求された範囲内にシグナルが見つからなかった場合、KSK プロパティ\_チューナー\_SCAN\_STATUS プロパティは、**チューナー\_LockType**プロパティ\_チューナーの**lockstatus**メンバーのを返します。 [ **\_スキャン\_状態\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)構造体です。 チューニングデバイスが信号からチューナー標準を自動的に検出し、別の標準の信号が検出された場合、チューニングデバイス自体は、 [**Ksk プロパティ\_チューナー\_標準**](ksproperty-tuner-standard.md)プロパティへの要求を処理できます。 チューニングデバイスは、段階的ロックループ (PLL) ロックを超えて続行できない可能性があり、標準が不明であることが指定されている可能性があります。 または、チューニングデバイスが異なるシグナル標準に自動的に調整される場合があります。 また、チューニングデバイスでは、そのシグナル標準に対して完全なロックを取得し、代替規格を決定することもできます。 このような状況は、頻度スペクトルに複数のシグナル標準がある場合に発生する可能性があります。

***<em>境界条件</em>***

チャネルのセンター周波数がアプリケーションが提供する範囲を超えていることがドライバーによって検出された場合、ドライバーはその信号を無視し、次の信号に移動する必要があります。ドライバーは、指定された範囲内で最適な近似を返すことはできません。 アプリケーションがチャネルリストをコンパイルしようとしたときにチャネルが重複しないようにするには、ドライバーを次のシグナルに移動する必要があります。

同じ理由から、アプリケーションでは、予想されるチャネル帯域幅の半分 (アナログおよびデジタルテレビの場合は約 6/2 = 3MHz) を使用してクエリの範囲をシフトする必要があります。これにより、ハードウェアがハードウェアの信号を検出したときに、特にチャネルが二重にカウントされないようにします。デコードできません。 このような状況では、ドライバーが特定のチャネルを二重にカウントすることが困難になります。

***<em>複数標準の Spectra</em>***

スキャン操作は、新しいチャネルまたはシグナルが見つかったときに完了する必要があります。 ドライバーは、 [**Ksk プロパティ\_チューナー\_scan\_status**](ksproperty-tuner-scan-status.md)プロパティを通じてスキャンの状態を返します。 新たに見つかったチャネルが以前に適用された標準に一致しないと判断した場合でも、新しいチャネルが見つかるたびにスキャンを完了する必要があります。 アプリケーションは新しいチャネル情報を処理する必要があり、スキャン要求を再送信して、同じシグナル標準を持つ別のチャネルを検索する必要があります。

## <a name="see-also"></a>関連項目


[**KSEVENT\_チューナー\_\_スキャン\_S を開始します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**KSK プロパティ\_チューナー\_スキャン\_状態**](ksproperty-tuner-scan-status.md)

[**KSK プロパティ\_チューナー\_スキャン\_CAPS**](ksproperty-tuner-scan-caps.md)

[**KSK プロパティ\_チューナー\_STANDARD**](ksproperty-tuner-standard.md)

[**KSK プロパティ\_チューナー\_標準\_モード**](ksproperty-tuner-standard-mode.md)

 

 






