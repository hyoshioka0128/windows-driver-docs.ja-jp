---
title: OID_NDK_STATISTICS
description: クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID_NDK_STATISTICS OID ミニポート アダプターの NDK 統計情報を取得します。
ms.assetid: 30F16DEC-AEE6-49D4-8599-95374ACBD446
ms.date: 08/08/2017
keywords: -OID_NDK_STATISTICS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e1593888fc5104dfa3aafa0ae1c574d07a73986f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371810"
---
# <a name="oidndkstatistics"></a>OID\_NDK\_統計情報


クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID\_NDK\_統計 OID ミニポート アダプターの NDK 統計情報を取得します。

NDIS 6.30 と以降のミニポート ドライバー NDK サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

**注**  NDIS OID 要求インターフェイスを直接この OID をサポートしています。 直接の OID 要求インターフェイスの詳細については、次を参照してください。 [NDIS 6.1 Direct OID 要求インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

 

<a name="remarks"></a>コメント
-------

NDIS 問題では、この OID、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体を指す、 [**NDIS\_NDK\_統計\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)構造体。

NDK 対応のミニポート ドライバーを提供する必要があります、 **CounterSet**は、メンバー、 [ **NDIS\_NDK\_パフォーマンス\_カウンター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters)構造体。

カウンターがなどのツールに発行される[perfmon](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731067(v=ws.11)) (を参照してください、 [NetworkDirect アクティビティ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997022(v=ws.11))パフォーマンス カウンター) され、パフォーマンス データ ヘルパー (PDH) とパフォーマンスのプログラムで利用できますライブラリ (PERFLIB) プログラミング インターフェイスです。 これらのインターフェイスの詳細については、次を参照してください。[パフォーマンス カウンター](https://docs.microsoft.com/windows/desktop/PerfCtrs/performance-counters-portal)します。

これらのカウンターは、呼び出すことによっても使用可能な[Get NetAdapterStatistics](https://docs.microsoft.com/powershell/module/network-adapter/get-netadapterstatistics) PowerShell コマンドレットを**RdmaStatistics**属性。 詳細については、 **RdmaStatistics**属性は、「 [ **MSFT\_NetAdapterStatisticsSettingData**](https://docs.microsoft.com/previous-versions/windows/desktop/netadaptercimprov/msft-netadapterstatisticssettingdata)します。

<a name="requirements"></a>必要条件
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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[カーネル モードのパフォーマンスの監視](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-mode-performance-monitoring)

[**NDIS\_NDK\_パフォーマンス\_カウンター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters)

[**NDIS\_NDK\_統計\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

 

 




