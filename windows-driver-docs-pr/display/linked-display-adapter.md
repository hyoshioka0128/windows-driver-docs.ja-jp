---
title: リンクされたディスプレイ アダプター
description: アダプター (LDA) リンクを表示するリンクの各物理アダプターをサポートできましていない GpuMmu または IoMmu または両方のアドレス指定モード別に。
ms.assetid: 28B13BD7-6CC7-47C7-9FA3-BC55C73441DF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0eb506f15f574d236c61a63f4962901e4aa1dc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372879"
---
# <a name="linked-display-adapter"></a>リンクされたディスプレイ アダプター


アダプター (LDA) リンクを表示するリンクの各物理アダプターがサポートできる*GpuMmu*または*IoMmu*または両方のモードを個別にアドレス指定します。

## <a name="span-idiommusupportspanspan-idiommusupportspanspan-idiommusupportspaniommu-support"></a><span id="IoMmu_support"></span><span id="iommu_support"></span><span id="IOMMU_SUPPORT"></span>IoMmu サポート


リンクの各物理アダプターがサポートできる、 *IoMmu*モデルや、 *GpuMmu*モデル。

[*DxgkDdiCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)論理アダプターは、サポートに呼び出される、 *IoMmu*モデル。

## <a name="span-idgpummusupportspanspan-idgpummusupportspanspan-idgpummusupportspangpummu-support"></a><span id="GpuMmu_support"></span><span id="gpummu_support"></span><span id="GPUMMU_SUPPORT"></span>GpuMmu サポート


リンク内のすべての物理アダプターが同一のプロセス仮想アドレス空間を共有しますが、各グラフィックス処理ユニット (GPU) の独自のページ テーブルがあります。 一般に、ページのテーブルの内容は、各 GPU で異なります。

![リンクされたディスプレイ アダプター メモリ アドレス セグメント](images/linked-display-adapter.1.png)

各物理アダプターが含むことができます独自*GpuMmu*機能 (ページ テーブルのセグメント、ページ テーブルの更新プログラムのノード、仮想アドレスのレイアウトを基になるページの表形式、サイズなど)。 唯一の制限は、すべての物理アダプターは同じ仮想アドレスのサイズである必要があります。 **GpuMmuCaps.VirtualAddressBitCount**すべてのアダプターの同じである必要があります。 ドライバーが最小にアドレス空間のサイズを固定する必要がありますの物理 Gpu します。

Microsoft DirectX グラフィックスのカーネルがクエリを今すぐ実行*GpuMmu*リンク内のすべての物理アダプターの上限。 [*DxgkDdiQueryAdapterInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) (**DXGKQAITYPE\_PAGETABLELEVELDESC**) は、物理アダプターごとにも呼び出されます。

**InputDataSize**と**pInputData**の[ *DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)(**DXGKQAITYPE\_GPUMMUCAPS**) を指す**DXGK\_GPUMMUCAPSIN**します。

**InputDataSize**と**pInputData**の[ *DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)(**DXGKQAITYPE\_PAGETABLELEVELDESC**)指す**DXGK\_PAGETABLELEVELDESCIN**します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)

 

 






