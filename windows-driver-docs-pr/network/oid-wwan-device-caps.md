---
title: OID_WWAN_DEVICE_CAPS
description: OID_WWAN_DEVICE_CAPS は、サポートしている携帯電話テクノロジ、サポートされているパケットデータのクラス、サポートしているラジオの周波数、提供する音声サービスの種類、サブスクライバーを使用するかどうかなど、MB デバイスの機能を返します。Id モジュール (SIM カード)。 ネットワークプロバイダーの選択と SIM のユーザーインターフェイスは、この2つの機能の値に依存するため、サポートされている携帯電話テクノロジと、デバイスが SIM を使用するかどうかは特に重要です。 製造元とファームウェアのリビジョンは、オプションのフィールドとして返されます。 Set 要求はサポートされていません。 ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻してから、NDIS_WWAN_DEVICE_CAPS を含む NDIS_STATUS_WWAN_DEVICE_CAPS ステータス通知を送信する必要があります。クエリ要求の完了時に、MB デバイスの機能を示す構造体。
ms.assetid: bcf04d0b-70f3-48b7-a505-c82e50edadb2
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DEVICE_CAPS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 47da6d6fb38509d23ba6568bda6e823db1e449f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843861"
---
# <a name="oid_wwan_device_caps"></a>OID\_WWAN\_デバイス\_CAP


OID\_WWAN\_デバイス\_CAP は、サポートしている携帯電話テクノロジ、サポートされるパケットデータのクラス、サポートする無線周波数、サポートする音声サービスの種類など、MB デバイスの機能を返します。サブスクライバー Id モジュール (SIM カード) を使用するかどうか。 ネットワークプロバイダーの選択と SIM のユーザーインターフェイスは、この2つの機能の値に依存するため、サポートされている携帯電話テクノロジと、デバイスが SIM を使用するかどうかは特に重要です。 製造元とファームウェアのリビジョンは、オプションのフィールドとして返されます。

Set 要求はサポートされていません。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_の状態\_返して、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_デバイスに送信する必要があり\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)クエリ要求の完了時に、MB デバイスの機能を示す[**NDIS\_WWAN\_デバイス\_caps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)構造体を含む cap 状態通知。

<a name="remarks"></a>注釈
-------

Windows 8 以降では、MB ドライバーモデルがバージョン2.0 に更新されました。 Windows 8 ミニポートドライバーでは、 [**ndis\_wwan\_device\_caps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)構造体の**Header. Revision**メンバーを**ndis\_WWAN\_デバイス\_cap\_リビジョン\_2**に設定する必要があります。*クエリ*要求。 Windows 7 ミニポートドライバーでは、 **ndis\_wwan\_device\_caps**構造体の**Header. Revision**メンバーを**ndis\_WWAN\_デバイス\_cap\_リビジョン**\_1*に設定する必要があります。クエリ*要求。

この OID の使用方法の詳細については、「 [WWAN ドライバーの初期化手順](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)」を参照してください。

ミニポートドライバーは、クエリ操作を処理するときにデバイスのメモリにアクセスできますが、プロバイダーネットワークまたはサブスクライバー Id モジュール (SIM カード) にはアクセスできません。

現在、多くの "世界中の" MB デバイスでは複数の周波数帯がサポートされています。これは、2.5 G/3G の周波数バンドが国と国によって異なるためです。 3GPP 標準 (GSM ベースのネットワークの場合) および3GPP2 標準 (CDMA ベースのネットワークの場合) で指定されているすべての無線周波数の一覧を次の表に示します。 どちらの標準も、同様のバンド分類スキームを採用しています。

**3GPP (GSM ベース) 周波数バンドクラス**

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>3GPP バンド</th>
<th>指定されたスペクトル</th>
<th>業界名</th>
<th>アップリンク (MS から BTS へ)</th>
<th>ダウンリンク (BTS ~ MS)</th>
<th>地域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バンド I</p></td>
<td><p>UMTS2100</p></td>
<td><p>IMT</p></td>
<td><p>1920-1980</p></td>
<td><p>2110-2170</p></td>
<td><p>ヨーロッパ、韓国、日本、中国</p></td>
</tr>
<tr class="even">
<td><p>帯域幅2</p></td>
<td><p>UMTS1900</p></td>
<td><p>PCS1900</p></td>
<td><p>1850-1910</p></td>
<td><p>1930-1990</p></td>
<td><p>北米、LATAM</p></td>
</tr>
<tr class="odd">
<td><p>バンド III</p></td>
<td><p>UMTS1800</p></td>
<td><p>DCS1800</p></td>
<td><p>1710-1785</p></td>
<td><p>1805-1880</p></td>
<td><p>ヨーロッパ、中国</p></td>
</tr>
<tr class="even">
<td><p>バンド IV</p></td>
<td><p>AWS</p></td>
<td><p>AWS、1.7/2.1</p></td>
<td><p>1710-1755</p></td>
<td><p>2110-2155</p></td>
<td><p>北米、LATAM</p></td>
</tr>
<tr class="odd">
<td><p>帯域幅 V</p></td>
<td><p>UMTS850</p></td>
<td><p>GSM850</p></td>
<td><p>824-849</p></td>
<td><p>869-894</p></td>
<td><p>北米、LATAM</p></td>
</tr>
<tr class="even">
<td><p>バンド VI</p></td>
<td><p>UMTS800</p></td>
<td><p>UMTS800</p></td>
<td><p>830-840</p></td>
<td><p>875-885</p></td>
<td><p>日本</p></td>
</tr>
<tr class="odd">
<td><p>バンド VII</p></td>
<td><p>UMTS2600</p></td>
<td><p>UMTS2600</p></td>
<td><p>2500-2570</p></td>
<td><p>2620-2690</p></td>
<td><p>ヨーロッパ</p></td>
</tr>
<tr class="even">
<td><p>バンド VIII</p></td>
<td><p>UMTS900</p></td>
<td><p>EGSM900</p></td>
<td><p>880-915</p></td>
<td><p>925-960</p></td>
<td><p>ヨーロッパ、中国</p></td>
</tr>
<tr class="odd">
<td><p>バンド IX</p></td>
<td><p>UMTS1700</p></td>
<td><p>UMTS1700</p></td>
<td><p>1750-1785</p></td>
<td><p>1845-1880</p></td>
<td><p>日本</p></td>
</tr>
<tr class="even">
<td><p>バンド X</p></td>
<td></td>
<td></td>
<td><p>1710-1770</p></td>
<td><p>2110-2170</p></td>
<td></td>
</tr>
</tbody>
</table>

 

**3GPP2 (CDMA ベース) 周波数バンドクラス**

3GPP バンド業界名アップリンク (MS から BTS) ダウンリンク (BTS から MS) バンド0

800MHz 携帯電話

824.025-844.995

869.025-889.995

バンド I

1900MHz 帯域

1850-1910

1930-1990

帯域幅2

TACS 帯域

872.025-914.9875

917.0125-959.9875

バンド III

JTACS 帯域

887.0125-924.9875

832.0125-869.9875

バンド IV

韓国語 PC の帯域

1750 ~ 1780

1840 ~ 1870

帯域幅 V

450 MHz バンド

410 ~ 483.475

420 ~ 493.475

バンド VI

2 GHz の帯域

1920 ~ 1979.950

2110 ~ 2169.950

バンド VII

700 MHz バンド

776 ~ 794

746 ~ 764

バンド VIII

1800 MHz バンド

1710 ~ 1784.950

1805 ~ 1879.95

バンド IX

900 MHz バンド

880 ~ 914.950

925 ~ 959.950

バンド X

2番目の 800 MHz 帯域

806 ~ 900.975

851 ~ 939.975

バンド XI

400 MHz 欧州 PAMR バンド

410 ~ 483.475

420 ~ 493.475

バンド XII

800 MHz の PAMR バンド

870.125 ~ 875.9875

915.0125 ~ 920.9875

バンド XIII

2.5 GHz IMT2000 拡張帯域幅

2500 ~ 2570

2620 ~ 2690

帯域 XIV

米国 PC 1.9 GHz バンド

1850 ~ 1915

1930 ~ 1995

バンド XV

AWS バンド

1710 ~ 1755

2110 ~ 2155

バンド XVI

米国 2.5 GHz バンド

2502 ~ 2568

2624 ~ 2690

バンド XVII

米国 2.5 GHz の前方リンクのみのバンド

2624-2690

 

両方のテーブルの無線周波数バンドの単位は、メガヘルツ (MHz) です。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_デバイス\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

[WWAN ドライバーの初期化手順](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)

 

 




