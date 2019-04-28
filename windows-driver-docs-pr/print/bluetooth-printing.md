---
title: Bluetooth 印刷
description: Bluetooth 印刷
ms.assetid: 6c40c142-9b52-4878-a84b-82d411086304
keywords:
- プリンター ドライバー WDK、Bluetooth
- Bluetooth の WDK、印刷
- WDK のプリンターをワイヤレス接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cfa49f9ac332a3167380cc4014a7e05204fba22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360588"
---
# <a name="bluetooth-printing"></a>Bluetooth 印刷


印刷デバイスが Bluetooth をサポートする場合、次の要件を満たすように。

-   印刷デバイス、USB または並列バス 1284 ID を返します、Bluetooth バスは、1284 ID を返す必要があります。 目的の場合、[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)(PnP) id に、デバイス ID を返す 1284 並列または USB バスで、Bluetooth バスは PnP id の 1284 ID を使用する必要がありますもします。
    **注**  1284 ID がまだパラレル ポートまたは USB ポートがなかったデバイスに含まれている必要があります PnP、1284 ID を使用せず、印刷キューは作成されません。

     

-   デバイスは、その USB ドライブまたは並列バス返すには、Microsoft Windows オペレーティング システムが適切でデバイスを識別でき、異なるバスを介して接続されている同じデバイスとは混同しないでように 1284 のと同じ ID を返す必要があります。 場合は、バス上のデバイスでは、Bluetooth 経由で同じ ID を返す必要がある 1284 ID を使用します。

    Windows オペレーティング システムでは、複数のバスを介して接続されているデバイスを追跡するために 1284 ID を使用しません。 プリンターは、同じ 1284 ID を使用して、オペレーティング システムは、単一の INF エントリによって適切なドライバーを読み込むことができますようにする必要があります。 バスを指定しない場合、プリンターのバス ドライバーは PnP Id を作成します。 たとえば、Bluetooth プリンター ID を取得するフォームの"BTHPRINT\\hpdeskje1234"と"hpdeskje1234"形式の。 最初のフォームはバスに固有で、2 番目の形式はバス中立です。 作成できます、INF これらのいずれかで Id、ドライバー パッケージが完全にバスに依存しないかどうかによって異なります。

-   デバイスが Bluetooth ハード コピー置換プロファイル (HCRP) をサポートする必要があります。 Bluetooth の HCRP の詳細については、次を参照してください。、 [Bluetooth の Web サイト](https://go.microsoft.com/fwlink/p/?linkid=26268)します。
    **注**  マイクロソフトは、シリアル ポート プロファイル (SPP) をサポートしていますが、認証が必要です。 ただし、HCRP は優れたユーザー エクスペリエンスを提供するため、SPP ではなく HCRP お勧めします。

     

 

 




