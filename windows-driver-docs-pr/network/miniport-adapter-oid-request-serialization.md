---
title: ミニポート アダプタ OID 要求のシリアル化
description: ミニポート アダプタ OID 要求のシリアル化
keywords:
- Oid WDK ネットワーク、ミニポート アダプターの要求
- ミニポート アダプタの WDK ネットワーク、OID 要求
- アダプターの WDK ネットワーク、OID 要求
- オブジェクト識別子の WDK ネットワーク
- OID のシリアル化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e48b115c2cc48a687311177eb30d5cf56c0057d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373952"
---
# <a name="miniport-adapter-oid-request-serialization"></a>ミニポート アダプタ OID 要求のシリアル化

除く NDIS ミニポート アダプターへのすべての OID 要求はシリアル化[OID 要求を送信](miniport-adapter-direct-oid-requests.md)、これに設計されたシリアル化されません。 ミニポート アダプタは、保留中の要求が完了するまで、新しい OID 要求を受信しません。 そのため、ミニポート アダプターでは、Oid を迅速に完了する必要があります。

>[!NOTE]
> ユーザーはパフォーマンスの遅延のことを確認しないため、1000 ミリ秒未満、または、1 秒間に、OID 要求を完了することをお勧めします。 OID 要求のタイミングの詳細については、次を参照してください。、 [NdisTimedOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete) Driver Verifier ルール。

この OID のシリアル化ルールを 1 つの例外は、WDI で、前の OID の完了に時間がかかる場合に、2 番目の OID 要求を参照してください可能性がありますを使用する Wi-fi ミニポート アダプターです。 次の例では、このような状況で発生する問題について説明します。

1. 最初の OID 要求は、WDI ミニポート アダプターに渡されます。
2. NIC は、OID、ドライバーで指定された制限時間内に応答しません。
3. WDI 呼び出してドライバーの[MINIPORT_WDI_ADAPTER_HANG_DIAGNOSE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose) NIC に関する診断データを収集するコールバック関数
4. 最初の OID はシリアル化をブロックすると見なされません。 つまり、最初の OID がシリアル化される場合でも、WDI ミニポート アダプターでは、他の OID 要求を受け取るようになりました。 ただし、これらの他の OID もシリアル化、つまり、WDI ミニポート アダプターが保留しない 2 つ以上の Oid に同時に (がまだ停止している最初の OID と 2 つ目の OID)。

## <a name="related-topics"></a>関連トピック

WDI UE ハング検出の詳細については、次を参照してください。 [UE ハング検出。手順 1 ~ 14](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-ue-hang-detection--step-1-to-step-14)します。

Ndis OID 要求の詳細については、次を参照してください。 [OID 要求ハンドラーを簡略化する](https://go.microsoft.com/fwlink/p/?linkid=846658)NDIS ブログ。

