---
title: ミニポートアダプター OID 要求のシリアル化
description: ミニポートアダプター OID 要求のシリアル化
keywords:
- Oid WDK ネットワーク、ミニポートアダプター要求
- ミニポートアダプター WDK ネットワーク、OID 要求
- WDK ネットワークのアダプター、OID 要求
- オブジェクト識別子 WDK ネットワーク
- OID シリアル化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fb788aef9f194bb5fc59beab3eb3d01735ff3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844252"
---
# <a name="miniport-adapter-oid-request-serialization"></a>ミニポートアダプター OID 要求のシリアル化

ミニポートアダプターに対するすべての OID 要求は、シリアル化されないように設計された[直接 oid 要求](miniport-adapter-direct-oid-requests.md)を除き、NDIS によってシリアル化されます。 保留中の要求が完了するまで、ミニポートアダプターは新しい OID 要求を受け取りません。 そのため、ミニポートアダプターは、Oid をすぐに完了する必要があります。

>[!NOTE]
> OID 要求は1000ミリ秒未満で完了することをお勧めします。1秒未満の場合、ユーザーはパフォーマンスの遅延を確認できません。 タイムアウトの OID 要求の詳細については、「 [NdisTimedOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete) Driver Verifier rule」を参照してください。

この OID シリアル化規則の例外の1つは、WDI を使用する Wi-fi ミニポートアダプターです。これにより、前の OID を完了するのに時間がかかりすぎる場合に2つ目の OID 要求が表示されることがあります。 次の例では、この状況での処理について説明します。

1. 最初の OID 要求は、WDI ミニポートアダプターに渡されます。
2. NIC は、ドライバーによって指定された制限時間内に OID に応答しません。
3. WDI は、ドライバーの[MINIPORT_WDI_ADAPTER_HANG_DIAGNOSE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)コールバック関数を呼び出して、NIC に関する診断データを収集します。
4. 最初の OID は、シリアル化をブロックするとは見なされなくなりました。 これは、最初の OID がシリアル化されている場合でも、WDI ミニポートアダプターが他の OID 要求を受信できるようになったことを意味します。 ただし、これらの他の OID もシリアル化されます。つまり、WDI ミニポートアダプターは2つ以上の Oid を同時に保留しません (最初の OID がハングし、もう1つの OID)。

## <a name="related-topics"></a>関連トピック

WDI UE-V の検出の詳細については、「 [ue-v detection: 手順 1-14](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-ue-hang-detection--step-1-to-step-14)」を参照してください。

NDIS での OID 要求の詳細については、NDIS ブログの「 [oid 要求ハンドラーの簡略化](https://go.microsoft.com/fwlink/p/?linkid=846658)」を参照してください。

