---
title: ビデオ メモリの提供と再利用
description: Windows 表示 Driver Model (WDDM) 1.2 およびそれ以降のユーザー モードのディスプレイ ドライバーがメモリ プランを使用して、、メモリにローカルとシステムのメモリに一時的なサーフェイスに必要なオーバーヘッドを削減する、Windows 8 以降で利用可能な機能を再利用する必要があります。
ms.assetid: 8BB6A7A3-E102-4069-BFC2-9605DDE9F020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c03386efab6f3bd9d98d798b0f6ca522be330539
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365077"
---
# <a name="video-memory-offer-and-reclaim"></a>ビデオ メモリの提供と再利用


Windows 表示 Driver Model (WDDM) 1.2 およびそれ以降のユーザー モードのディスプレイ ドライバーがメモリ プランを使用して、、メモリにローカルとシステムのメモリに一時的なサーフェイスに必要なオーバーヘッドを削減する、Windows 8 以降で利用可能な機能を再利用する必要があります。

|                                                                                   |                                  |
|-----------------------------------------------------------------------------------|----------------------------------|
| WDDM の最小バージョン                                                              | 1.2                              |
| Windows の最小バージョン                                                           | 8                                |
| ドライバーの実装: 完全なグラフィックスとレンダリングのみ                               | 必須                        |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト | **Device.Graphics.OfferReclaim** |

 

特にモバイルのシナリオでハードウェア アクセラレータを必要とするグラフィックを多用するアプリケーションは GPU リソースの多用かかる場合がします。 また、多くのモバイル デバイスで、GPU は CPU、チップセットに統合され、ビデオ メモリとして GPU がシステム メモリの一部を使用します。 複数のアプリが頻繁にシステム メモリに大量の要求をさらに、GPU の使用を行うときは、適切なシステムのパフォーマンスを確実に、ディスプレイ ドライバーのメモリ使用量が最小化する必要があります。 プラン/再利用のデバイス ドライバー インターフェイス (Ddi) は、これを行う機構を提供します。

API は、システムが他の使用でも最近破棄されました。 メモリを再利用したり再利用後で不要なメモリを提供するアプリに対して使用できます。 Microsoft DirectX Graphics Infrastructure (DXGI) アプリのプログラミングのトピックを参照して[DXGI 1.2 改善](https://docs.microsoft.com/windows/desktop/direct3ddxgi/dxgi-1-2-improvements)します。

## <a name="span-idofferandreclaimddispanspan-idofferandreclaimddispanspan-idofferandreclaimddispanoffer-and-reclaim-ddi"></a><span id="Offer_and_reclaim_DDI"></span><span id="offer_and_reclaim_ddi"></span><span id="OFFER_AND_RECLAIM_DDI"></span>DDI を再利用は、


新しい関数は、プランまたはメモリを再利用するユーザー モード ドライバー用の Windows 8 以降で使用できます。

ドライバーは、提供またはメモリの割り当てを再利用するこれらのシステム指定の関数を呼び出します。

-   [**pfnOfferAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocationscb)
-   [**pfnReclaimAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)

ドライバーは、Microsoft direct3d10 ハードウェアをサポートしている場合、これらの関数を実装します。

-   [*pfnOfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*pfnReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

マイクロソフトの Direct3D 9 のハードウェアをサポートしている場合、ドライバーは、次の関数を実装します。 また、アプリは提供または Direct3D 9 ハードウェアで実行されている Direct3D 11 API を使用しているときに、割り当てを再利用、Direct3D ランタイムは、これらの関数を呼び出します。

-   [*OfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*ReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimresources)

これらの関連付けられている構造および列挙体を使用します。

-   [**D3DDDI\_提供\_優先順位**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddi_offer_priority)
-   [**D3DDDIARG\_OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_offerresources)
-   [**D3DDDIARG\_RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_reclaimresources)
-   [**D3DDDICB\_OFFERALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_offerallocations)
-   [**D3DDDICB\_RECLAIMALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations)
-   [**DXGI\_DDI\_ARG\_OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_offerresources)
-   [**DXGI\_DDI\_ARG\_RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_reclaimresources)
-   [**DXGI1\_2\_DDI\_ベース\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

プラン/再利用機能をサポートするためには、この構造体に、Windows 8 以降と、2 つの新しいメンバーがあります。

-   [**D3DDDI\_ALLOCATIONLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationlist)

ドライバーを処理するこの機能正しく割り当てを破棄すると、後にすべてのデータが失われるため、慎重にテストする必要があります。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.OfferReclaim**します。 これらの要件が、ドライバーが割り当てを提供する必要があります、シナリオを一覧表示することに注意してください。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





