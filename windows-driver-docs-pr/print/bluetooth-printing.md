---
title: Bluetooth 印刷
description: Bluetooth 印刷
ms.assetid: 6c40c142-9b52-4878-a84b-82d411086304
keywords:
- プリンタードライバー WDK、Bluetooth
- Bluetooth WDK, 印刷
- ワイヤレス接続の WDK プリンター
ms.date: 06/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: bbf317201be82595af1bdf2edd4c4efcd616ca96
ms.sourcegitcommit: f0e54ea159d168a77643bf2e098d6b90e92b528c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455564"
---
# <a name="bluetooth-printing"></a>Bluetooth 印刷

印刷デバイスが Bluetooth をサポートしている場合は、次の要件を満たしている必要があります。

- 印刷デバイスが USB またはパラレルバスで 1284 ID を返す場合、Bluetooth バスは 1284 ID を返す必要があります。 [プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)(PnP) と識別の目的で、デバイスがパラレルまたは USB バスで 1284 id を返す場合は、Bluetooth バスでも PnP 識別に 1284 id を使用する必要があります。

  > [!NOTE]
  > 並列または USB ポートを持たない skimmingDevices がまだ 1284 ID を保持している必要がある場合でも、ユーザーに通知する必要がある情報。 1284 ID が指定されていない場合、PnP は印刷キューを作成しません。

- デバイスは、USB またはパラレルバスから返されたものと同じ 1284 ID を返す必要があります。これにより、Microsoft Windows オペレーティングシステムでは、デバイスを正しく識別し、別のバスを介して接続されている同じデバイスと混同しないようにすることができます。 バス上のデバイスで 1284 ID が使用されている場合、その同じ ID が Bluetooth 経由で返される必要があります。

  Windows オペレーティングシステムでは、1284 ID を使用して、複数のバス経由で接続されているデバイスを追跡しません。 プリンターは同じ 1284 ID を使用する必要があるため、オペレーティングシステムは1つの INF エントリを使用して適切なドライバーを読み込むことができます。 プリンタバスドライバは、バスが指定されていない状態で PnP Id を作成します。 たとえば、Bluetooth プリンターは、"BTHPRINT hpdeskje1234" という形式の ID \\ と、"hpdeskje1234" という形式の ID を取得します。 最初の形式はバス固有で、2番目の形式はバスに依存しません。 ドライバーパッケージが完全にバス中立であるかどうかに応じて、これらのいずれかの Id で INF を作成できます。

- デバイスは、Bluetooth ハードコピー交換プロファイル (HCRP) をサポートしている必要があります。 Bluetooth の HCRP の詳細については、 [Bluetooth Web サイト](https://www.bluetooth.com/specifications/profiles-overview)を参照してください。

  > [!NOTE]
  > Microsoft はシリアルポートプロファイル (SPP) をサポートしていますが、認証が必要です。 HCRP はより優れたユーザーエクスペリエンスを提供するため、SPP ではなく HCRP を使用することをお勧めします。
