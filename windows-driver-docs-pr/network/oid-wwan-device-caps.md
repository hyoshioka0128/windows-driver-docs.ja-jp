---
title: OID_WWAN_DEVICE_CAPS
description: OID_WWAN_DEVICE_CAPS 返します MB デバイスの機能、サポート、携帯電話テクノロジなどのパケット データをサポートしています、無線周波数をサポートしています、それが提供する音声サービスの種類のクラスおよびサブスクライバーを使用しているかどうかIdentity モジュール (SIM カード)。 サポートされている携帯電話テクノロジと、デバイスが SIM を使用するかどうかは、ネットワーク プロバイダーの選択と SIM ユーザー インターフェイスはこれら 2 つの機能の値に依存しているため特に重要です。 省略可能なフィールドとしては、製造元、ファームウェアのリビジョンが返されます。 要求のセットがサポートされていません。 ミニポート ドライバーする必要がありますクエリ要求を処理、非同期的に最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すと、後で、NDIS_WWAN_DEVICE_CAPS を含む NDIS_STATUS_WWAN_DEVICE_CAPS 状態通知の送信クエリ要求を完了するときは、MB デバイスの機能を示す構造体。
ms.assetid: bcf04d0b-70f3-48b7-a505-c82e50edadb2
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_CAPS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4efc9997106ba5df31a4ce9cdb2011a73aff2c52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386679"
---
# <a name="oidwwandevicecaps"></a>OID\_WWAN\_デバイス\_キャップ


OID\_WWAN\_デバイス\_CAP 返します方式のサポートを含む、MB デバイスの機能、サービスのパケット データをサポートしています、無線周波数をサポートしていますが、音声の種類のクラスこのオプションを提供すると、Subscriber Identity Module (SIM カード) を使用するかどうか。 サポートされている携帯電話テクノロジと、デバイスが SIM を使用するかどうかは、ネットワーク プロバイダーの選択と SIM ユーザー インターフェイスはこれら 2 つの機能の値に依存しているため特に重要です。 省略可能なフィールドとしては、製造元、ファームウェアのリビジョンが返されます。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567845)状態通知を含む、 [ **NDIS\_WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567907)クエリ要求を完了するときは、MB デバイスの機能を示す構造体。

<a name="remarks"></a>コメント
-------

Windows 8 以降、MB ドライバー モデルは、バージョン 2.0 に更新されましたがします。 Windows 8 のミニポート ドライバーを設定する必要があります、 **Header.Revision**のメンバー、 [ **NDIS\_WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567907)構造体を**NDIS\_WWAN\_デバイス\_CAP\_リビジョン\_2**の*クエリ*要求。 Windows 7 のミニポート ドライバーを設定する必要があります、 **Header.Revision**のメンバー、 **NDIS\_WWAN\_デバイス\_CAP**構造体を**NDIS\_WWAN\_デバイス\_CAP\_リビジョン\_1**の*クエリ*要求。

詳細については、この OID を使用して、次を参照してください。 [WWAN ドライバーの初期化プロシージャ](https://msdn.microsoft.com/library/windows/hardware/ff557186)します。

処理クエリ、操作が、プロバイダーのネットワークまたは Subscriber Identity Module (SIM カード) にアクセスしないでください、ミニポート ドライバーはデバイスのメモリにアクセスできます。

多くの「世界的な」MB デバイスは、2.5 g の頻度がバンドため、今日の周波数の複数のバンドをサポート/3 G が国によって異なります。 3 gpp 標準 (GSM ベースのネットワーク) と (CDMA ベースのネットワーク) 3GPP2 標準で指定された無線周波数は、次の表に示すすべての一覧。 両方の標準では、似たバンド分類手法を採用します。

**3 gpp (GSM ベース) の周波数帯クラス**

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
<th>3 gpp バンド</th>
<th>指定された範囲</th>
<th>業界の名前</th>
<th>アップリンク (BTS にミリ秒)</th>
<th>ダウンリンク (BTS MS を)</th>
<th>地域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バンドは</p></td>
<td><p>UMTS2100</p></td>
<td><p>IMT</p></td>
<td><p>1920-1980</p></td>
<td><p>2110-2170</p></td>
<td><p>ヨーロッパ、韓国、日本、中国</p></td>
</tr>
<tr class="even">
<td><p>バンド II</p></td>
<td><p>UMTS1900</p></td>
<td><p>PCS1900</p></td>
<td><p>1850-1910</p></td>
<td><p>1930-1990</p></td>
<td><p>北アメリカ、LATAM</p></td>
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
<td><p>AWS, 1.7/2.1</p></td>
<td><p>1710-1755</p></td>
<td><p>2110-2155</p></td>
<td><p>北アメリカ、LATAM</p></td>
</tr>
<tr class="odd">
<td><p>バンド V</p></td>
<td><p>UMTS850</p></td>
<td><p>GSM850</p></td>
<td><p>824-849</p></td>
<td><p>869-894</p></td>
<td><p>北アメリカ、LATAM</p></td>
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
<td><p>バンド第 7</p></td>
<td><p>UMTS2600</p></td>
<td><p>UMTS2600</p></td>
<td><p>2500-2570</p></td>
<td><p>2620-2690</p></td>
<td><p>ヨーロッパ</p></td>
</tr>
<tr class="even">
<td><p>バンド 8 部</p></td>
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

 

**3GPP2 (CDMA ベース) の周波数帯クラス**

3 gpp バンド業界名前アップリンク (BTS にミリ秒) (BTS ms) ダウンリンク バンド 0

800 MHz の携帯電話

824.025-844.995

869.025-889.995

バンドは

1900 MHz バンド

1850-1910

1930-1990

バンド II

TACS バンド

872.025-914.9875

917.0125-959.9875

バンド III

JTACS バンド

887.0125-924.9875

832.0125-869.9875

バンド IV

韓国語の PC のバンド

1750 - 1780

1840 - 1870

バンド V

450 MHz バンド

410 - 483.475

420 - 493.475

バンド VI

2 GHz バンド

1920 - 1979.950

2110 - 2169.950

バンド第 7

700 MHz バンド

776 - 794

746 - 764

バンド 8 部

1800 MHz バンド

1710 - 1784.950

1805 - 1879.95

バンド IX

900 MHz バンド

880 - 914.950

925 - 959.950

バンド X

セカンダリの 800 MHz バンド

806 - 900.975

851 - 939.975

バンド XI

400 MHz ヨーロッパ PAMR バンド

410 - 483.475

420 - 493.475

バンド 12 世

800 MHz PAMR バンド

870.125 - 875.9875

915.0125 - 920.9875

バンド 13 世

2.5 GHz IMT2000 拡張機能のバンド

2500 - 2570

2620 - 2690

バンド XIV

PC 1.9 GHz バンドの米国

1850 - 1915

1930 - 1995

バンドされます。

AWS バンド

1710 - 1755

2110 - 2155

バンド 16 世

2.5 GHz バンドの米国

2502 - 2568

2624 - 2690

バンド XVII

米国 2.5 GHz 前方リンクのみバンド

2624-2690

 

両方のテーブル内の無線周波数バンドの単位は、メガヘルツ (MHz) です。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_デバイス\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/ff567907)

[WWAN ドライバーの初期化の手順](https://msdn.microsoft.com/library/windows/hardware/ff557186)

 

 




