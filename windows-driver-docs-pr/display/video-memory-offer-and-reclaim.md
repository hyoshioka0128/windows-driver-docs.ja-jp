---
title: ビデオ メモリの提供と再利用
description: Windows Display Driver Model (WDDM) 1.2 以降のユーザーモード表示ドライバーでは、Windows 8 以降で使用可能なメモリプランと回収機能を使用して、ローカルメモリとシステムメモリ内の一時サーフェイスに必要なメモリオーバーヘッドを削減する必要があります。
ms.assetid: 8BB6A7A3-E102-4069-BFC2-9605DDE9F020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58691a688afc069ab6154c9cad99f3c4985b1721
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968221"
---
# <a name="video-memory-offer-and-reclaim"></a>ビデオ メモリの提供と再利用


Windows Display Driver Model (WDDM) 1.2 以降のユーザーモード表示ドライバーでは、Windows 8 以降で使用可能なメモリプランと回収機能を使用して、ローカルメモリとシステムメモリ内の一時サーフェイスに必要なメモリオーバーヘッドを削減する必要があります。

**最小 WDDM バージョン**: 1.2

**Windows の最小バージョン**: 8

**ドライバーの実装—完全なグラフィックスとレンダーのみ**: 必須

** [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)必要条件とテスト**:**デバイス...OfferReclaim**


 

特にモバイルシナリオでは、ハードウェアアクセラレータを必要とするグラフィックス集中型のアプリで GPU リソースを大量に使用する可能性があります。 また、多くのモバイルデバイスでは、GPU は CPU チップセットに統合されており、GPU はビデオメモリとしてシステムメモリの一部を使用します。 複数のアプリが1つの GPU を大量に使用し、システムメモリに対する需要が高い場合は、ディスプレイドライバーのメモリフットプリントを最小限に抑える必要があるので、システムパフォーマンスを十分に高めることができます。 この操作を行うためのメカニズムは、オファー/回収デバイスドライバーインターフェイス (DDIs) によって提供されます。

API は、不要なメモリを提供するアプリで使用できます。この場合、後で他の使用を再利用したり、最近破棄されたメモリを再利用したりすることができます。 Microsoft DirectX グラフィックスインフラストラクチャ (DXGI) アプリのプログラミングに関するトピック「 [dxgi 1.2 の機能強化](https://docs.microsoft.com/windows/desktop/direct3ddxgi/dxgi-1-2-improvements)」を参照してください。

## <a name="span-idoffer_and_reclaim_ddispanspan-idoffer_and_reclaim_ddispanspan-idoffer_and_reclaim_ddispanoffer-and-reclaim-ddi"></a><span id="Offer_and_reclaim_DDI"></span><span id="offer_and_reclaim_ddi"></span><span id="OFFER_AND_RECLAIM_DDI"></span>DDI の提供と再利用


Windows 8 以降では、ユーザーモードドライバーがメモリを提供または再利用するために、新しい関数を使用できます。

ドライバーは、これらのシステム指定の関数を呼び出してメモリ割り当てを提供または解放します。

-   [**pfnOfferAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocationscb)
-   [**pfnReclaimAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)

Microsoft Direct3D 10 ハードウェアがサポートされている場合、ドライバーは次の機能を実装します。

-   [*pfnOfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*pfnReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

ドライバーは、Microsoft Direct3D 9 ハードウェアをサポートする場合、次の機能を実装します。 また、direct3d 9 ハードウェアで実行されている Direct3D 11 API を使用しているときにアプリが割り当てを提供または再利用する場合、Direct3D ランタイムは次の関数を呼び出します。

-   [*OfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*ReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimresources)

これらの関連する構造体と列挙型を使用します。

-   [**D3DDDI \_ プランの \_ 優先度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddi_offer_priority)
-   [**D3DDDIARG \_ OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_offerresources)
-   [**D3DDDIARG \_ RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_reclaimresources)
-   [**D3DDDICB \_ OFFERALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_offerallocations)
-   [**D3DDDICB \_ RECLAIMALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations)
-   [**DXGI \_ DDI \_ ARG \_ OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_offerresources)
-   [**DXGI \_ DDI \_ ARG \_ RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_reclaimresources)
-   [**DXGI1 \_ 2 \_ DDI \_ 基本 \_ 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

オファー/回収機能をサポートするために、Windows 8 以降では、この構造には次の2つの新しいメンバーがあります。

-   [**D3DDDI の割り当て \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationlist)

割り当てが破棄された後、そのデータのすべてのデータが失われるため、ドライバーがこの機能を正しく処理していることを慎重にテストする必要があります。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細[について](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)は、**デバイス...OfferReclaim**。 これらの要件には、ドライバーが割り当てを提供する必要があるシナリオが一覧表示されます。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





