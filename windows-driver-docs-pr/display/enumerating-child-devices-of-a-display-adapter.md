---
title: ディスプレイアダプターの子デバイスの列挙
description: ディスプレイアダプターの子デバイスの列挙
ms.assetid: 3bec2117-aef4-41fc-b88a-0081c7c9fe3d
keywords:
- ビデオの現在のネットワーク WDK ディスプレイ、アダプターの子デバイスの表示
- VidPN WDK ディスプレイ、ディスプレイアダプターの子デバイス
- 子デバイス WDK ビデオの現在のネットワーク
- ディスプレイアダプターの子デバイス WDK ビデオの現在のネットワーク
- 子デバイスの列挙 WDK ビデオの現在のネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2cfd0a7aec3e60d34fecd4e2d11ee38d24eea59
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838948"
---
# <a name="enumerating-child-devices-of-a-display-adapter"></a>ディスプレイアダプターの子デバイスの列挙


次の一連の手順では、表示ポートドライバー、ディスプレイミニポートドライバー、およびビデオの現在のネットワーク (VidPN) マネージャーが初期化時に共同作業し、ディスプレイアダプターの子デバイスを列挙する方法について説明します。

1.  ディスプレイポートドライバーは、ディスプレイミニポートドライバーの[**DxgkDdiStartDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)関数を呼び出します。 *DxgkDdiStartDevice*は、ディスプレイアダプターの子である (またはドッキングによって取得される可能性がある) デバイスの数を ( *numberofchildren*パラメーターで) 返します。 また、 *DxgkDdiStartDevice*は、ディスプレイアダプターによってサポートされているビデオの現在の数 N を ( *NumberOfVideoPresentSources*パラメーターで) 返します。 ビデオの存在するソースは、0、1、...N-1。

2.  ディスプレイポートドライバーは、ディスプレイアダプターの子デバイスを列挙するディスプレイミニポートドライバーの[**DxgkDdiQueryChildRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数を呼び出します。 *DxgkDdiQueryChildRelations*は、子デバイスごとに1つずつ、 [**DXGK\_子\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_descriptor)の構造体の配列を格納します。 ディスプレイアダプタのすべての子デバイスがオンボードになっていることに注意してください。モニタや、ディスプレイアダプタに接続するその他の外部デバイスは、子デバイスとは見なされません。 詳細については、「[ディスプレイアダプターの子デバイス](child-devices-of-the-display-adapter.md)」を参照してください。 *DxgkDdiQueryChildRelations*は、可能な子デバイスだけでなく、初期化時に物理的に存在する子デバイスも列挙する必要があります。 たとえば、ラップトップコンピューターをドッキングステーションに接続すると新しいビデオ出力が表示される場合、 *DxgkDdiQueryChildRelations*は、初期化時にコンピューターがドッキングされているかどうかに関係なく、そのビデオ出力を列挙する必要があります。 また、ドングルをビデオ出力コネクタに接続すると、複数のモニターでコネクタを共有できるようになり、ドングルが接続されているかどうかに関係なく、 *DxgkDdiQueryChildRelations*はドングルの各分岐の子デバイスを列挙する必要があります。初期化時間。

3.  **HpdAwarenessInterruptible**または**HpdAwarenessPolled**という hpd 認識値がある各子デバイス (手順1で説明) に対して、ディスプレイポートドライバーはディスプレイミニポートドライバーの[**DxgkDdiQueryChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)を呼び出します。子デバイスに外部デバイスが接続されているかどうかを判断する関数。

4.  ディスプレイポートドライバーは、次のいずれかの条件を満たす子デバイスごとに PDO を作成します。
    -   子デバイスは、 **HpdAwarenessAlwaysConnected**の hpd 認識値を持ちます。
    -   子デバイスの**HpdAwarenessPolled**または**HpdAwarenessInterruptible**の hpd 認識値があるため、オペレーティングシステムは、前のクエリを認識しているか、子デバイスに外部デバイスが接続されていることを通知しています。

5.  ディスプレイポートドライバーは、次のいずれかの条件を満たす各子デバイスのディスプレイミニポートドライバーの[**DxgkDdiQueryDeviceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)関数を呼び出します。

    -   子デバイスは、外部デバイスが接続されていることがわかっています。
    -   子デバイスは、外部デバイスが接続されていることを前提としています。
    -   子デバイスの種類は**Typeother**です。

    接続モニター (またはその他のディスプレイデバイス) が EDID 記述子をサポートしている場合、 *DxgkDdiQueryDeviceDescriptor*は拡張表示情報データ (EDID) ブロックを返します。

    注: 初期化中、ディスプレイポートドライバーは各モニターの*DxgkDdiQueryDeviceDescriptor*を呼び出して、モニターの EDID の最初の128バイトのブロックを取得します。 これにより、初期化時に表示ポートドライバーに必要なもの (PnP ハードウェア ID、インスタンス ID、互換性のある Id、デバイステキスト) が表示されます。 後で、モニタークラスの関数ドライバー ( *DxgkDdiQueryDeviceDescriptor* ) は、各モニターの最初の128バイトの edid ブロックと追加の128バイトの edid 拡張ブロックを取得するために、それぞれのモニターに対して1つずつを呼び出します。 これは、ディスプレイミニポートドライバーが2回呼び出され、各モニターの EDID の最初の128バイトブロックが提供されることを意味します。

6.  VidPN マネージャーは、ディスプレイアダプターでサポートされているすべてのビデオの現在のソースとビデオの現在のターゲットの識別子を取得します。 ビデオの存在するソースは、0、1、...N-1。ここで N は、ディスプレイミニポートドライバーの*DxgkDdiStartDevice*関数によって返されるソースの数です。 ビデオの現在のターゲットには、 *DxgkDdiQueryChildRelations*中にディスプレイミニポートドライバーによって以前に作成された一意の整数識別子があります。 **TypeVideoOutput**型の各子デバイスはビデオの現在のターゲットに関連付けられており、子デバイスの DXGK\_子\_記述子構造体の**ChildUid**メンバーは、ビデオの現在のターゲットの識別子として使用されます。

7.  VidPN マネージャーでは、次の手順に従って、最初の VidPN を構築します。
    -   前回正常起動時の VidPN がレジストリに記録されている場合は、最初の VidPN として使用します。

    -   それ以外の場合は、表示ミニポートドライバーの[**DxgkDdiRecommendFunctionalVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)関数を呼び出して、最初の VidPN を取得します。

    -   *DxgkDdiRecommendFunctionalVidPn*が許容される機能的な vidpn を返すことができない場合は、1つのビデオが存在するパスを含む単純な vidpn を作成します。つまり、1 (ソース、ターゲット) のペアです。 表示ミニポートドライバーの[**DxgkDdiIsSupportedVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)関数を呼び出して、提案された VidPN が機能することを確認します。 *DxgkDdiIsSupportedVidPn*が、提案された vidpn が機能しないことを報告した場合は、適切な vidpn が見つかるまで試してみてください。

    -   表示ミニポートドライバーの[**DxgkDdiEnumVidPnCofuncModality**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)関数を呼び出して、VidPN で使用できるソースモードとターゲットモードを決定します。

 

 





