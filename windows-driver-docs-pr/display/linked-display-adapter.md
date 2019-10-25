---
title: リンクされたディスプレイアダプター
description: リンクされたディスプレイアダプター (LDA) リンク内の各物理アダプターは、GpuMmu または IoMmu または両方のアドレス指定モードを個別にサポートできます。
ms.assetid: 28B13BD7-6CC7-47C7-9FA3-BC55C73441DF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038e01ffa52581a11a081c336f34b49a1570ffbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840395"
---
# <a name="linked-display-adapter"></a>リンクされたディスプレイアダプター


リンクされたディスプレイアダプター (LDA) リンク内の各物理アダプターは、 *Gpummu*または*IoMmu*または両方のアドレス指定モードを個別にサポートできます。

## <a name="span-idiommu_supportspanspan-idiommu_supportspanspan-idiommu_supportspaniommu-support"></a><span id="IoMmu_support"></span><span id="iommu_support"></span><span id="IOMMU_SUPPORT"></span>IoMmu サポート


リンク内の各物理アダプターは、 *IoMmu*モデルと*gpummu*モデルのどちらかまたは両方をサポートできます。

[*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)は、 *IoMmu*モデルをサポートする論理アダプターに対して呼び出されます。

## <a name="span-idgpummu_supportspanspan-idgpummu_supportspanspan-idgpummu_supportspangpummu-support"></a><span id="GpuMmu_support"></span><span id="gpummu_support"></span><span id="GPUMMU_SUPPORT"></span>GpuMmu のサポート


リンク内のすべての物理アダプターは、同じプロセス仮想アドレス空間を共有しますが、各グラフィックス処理ユニット (GPU) には独自のページテーブルがあります。 一般に、ページテーブルの内容は GPU ごとに異なります。

![リンクされたディスプレイアダプターのメモリアドレスセグメント](images/linked-display-adapter.1.png)

各物理アダプターは、独自の*Gpummu*機能を持つことができます (ページテーブルセグメント、ページテーブル更新ノード、仮想アドレスレイアウト、基になるページテーブル形式、サイズなど)。 唯一の制限は、すべての物理アダプターが同じ仮想アドレスサイズを持つ必要があることです。 **GpuMmuCaps**は、すべてのアダプターで同じである必要があります。 ドライバーは、アドレス空間のサイズを物理 Gpu の最小値にクランプする必要があります。

Microsoft DirectX グラフィックスカーネルによって、リンク内のすべての物理アダプターに対して*Gpummu*キャップが照会されるようになります。 [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) (**DXGKQAITYPE\_PAGETABLELEVELDESC**) は、物理アダプターごとにも呼び出されます。

[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)の**Inputdatasize**と**pinputdata** (**DXGKQAITYPE\_GPUMMUCAPS**) は**DXGK\_GPUMMUCAPSIN**を指します。

[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)の**Inputdatasize**と**pinputdata** (**DXGKQAITYPE\_PAGETABLELEVELDESC**) は**DXGK\_PAGETABLELEVELDESCIN**を指します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連項目


[*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)

 

 






