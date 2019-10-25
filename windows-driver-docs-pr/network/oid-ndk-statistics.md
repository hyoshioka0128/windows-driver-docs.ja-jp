---
title: OID_NDK_STATISTICS
description: クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードのアプリケーションは、OID_NDK_STATISTICS OID を使用して、ミニポートアダプターの NDK 統計情報を取得します。
ms.assetid: 30F16DEC-AEE6-49D4-8599-95374ACBD446
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NDK_STATISTICS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 24373920041a5b176ec6036f37458e07582d95b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844101"
---
# <a name="oid_ndk_statistics"></a>OID\_NDK\_統計


クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションは、\_NDK\_STATISTICS OID を使用して、ミニポートアダプターの NDK 統計情報を取得します。

NDK サービスを提供する NDIS 6.30 以降のミニポートドライバーでは、この OID がサポートされている必要があります。 それ以外の場合、この OID は省略可能です。

**注**  NDIS では、この oid が直接 oid 要求インターフェイスでサポートされています。 直接 OID 要求インターフェイスの詳細については、「 [NDIS 6.1 DIRECT Oid Request interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

 

<a name="remarks"></a>注釈
-------

Ndis は、ndis [ **\_NDK\_STATISTICS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)構造体を指す NDIS [ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーで、この oid を発行します。

NDK 対応ミニポートドライバーは、 **CounterSet**メンバーを提供する必要があります。これは、 [**NDIS\_NDK\_PERFORMANCE\_カウンター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters)構造体です。

これらのカウンターは、 [perfmon](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731067(v=ws.11))などのツールに発行され ( [NetworkDirect アクティビティ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997022(v=ws.11))パフォーマンスカウンターを参照)、パフォーマンスデータヘルパー (PDH) およびパフォーマンスライブラリ (PERFLIB) プログラミングインターフェイスを使用してプログラムで使用できるようになっています。 これらのインターフェイスの詳細については、「[パフォーマンスカウンター](https://docs.microsoft.com/windows/desktop/PerfCtrs/performance-counters-portal)」を参照してください。

これらのカウンターは、 **Rdmastatistics**属性を使用して[NetAdapterStatistics](https://docs.microsoft.com/powershell/module/network-adapter/get-netadapterstatistics) PowerShell コマンドレットを呼び出すことによっても使用できます。 **Rdmastatistics**属性の詳細については、「 [**MSFT\_NetAdapterStatisticsSettingData**](https://docs.microsoft.com/previous-versions/windows/desktop/netadaptercimprov/msft-netadapterstatisticssettingdata)」を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>サポートなし</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[カーネル モードのパフォーマンスの監視](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-mode-performance-monitoring)

[**NDIS\_NDK\_パフォーマンス\_カウンター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters)

[**NDIS\_NDK\_統計\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




