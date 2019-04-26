---
title: リンクされたディスプレイ アダプター
description: アダプター (LDA) リンクを表示するリンクの各物理アダプターをサポートできましていない GpuMmu または IoMmu または両方のアドレス指定モード別に。
ms.assetid: 28B13BD7-6CC7-47C7-9FA3-BC55C73441DF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 983e94a1b280423261980c4518c7a2b09519b5e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354266"
---
# <a name="linked-display-adapter"></a>リンクされたディスプレイ アダプター


アダプター (LDA) リンクを表示するリンクの各物理アダプターがサポートできる*GpuMmu*または*IoMmu*または両方のモードを個別にアドレス指定します。

## <a name="span-idiommusupportspanspan-idiommusupportspanspan-idiommusupportspaniommu-support"></a><span id="IoMmu_support"></span><span id="iommu_support"></span><span id="IOMMU_SUPPORT"></span>IoMmu サポート


リンクの各物理アダプターがサポートできる、 *IoMmu*モデルや、 *GpuMmu*モデル。

[*DxgkDdiCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559615)論理アダプターは、サポートに呼び出される、 *IoMmu*モデル。

## <a name="span-idgpummusupportspanspan-idgpummusupportspanspan-idgpummusupportspangpummu-support"></a><span id="GpuMmu_support"></span><span id="gpummu_support"></span><span id="GPUMMU_SUPPORT"></span>GpuMmu サポート


リンク内のすべての物理アダプターが同一のプロセス仮想アドレス空間を共有しますが、各グラフィックス処理ユニット (GPU) の独自のページ テーブルがあります。 一般に、ページのテーブルの内容は、各 GPU で異なります。

![リンクされたディスプレイ アダプター メモリ アドレス セグメント](images/linked-display-adapter.1.png)

各物理アダプターが含むことができます独自*GpuMmu*機能 (ページ テーブルのセグメント、ページ テーブルの更新プログラムのノード、仮想アドレスのレイアウトを基になるページの表形式、サイズなど)。 唯一の制限は、すべての物理アダプターは同じ仮想アドレスのサイズである必要があります。 **GpuMmuCaps.VirtualAddressBitCount**すべてのアダプターの同じである必要があります。 ドライバーが最小にアドレス空間のサイズを固定する必要がありますの物理 Gpu します。

Microsoft DirectX グラフィックスのカーネルがクエリを今すぐ実行*GpuMmu*リンク内のすべての物理アダプターの上限。 [*DxgkDdiQueryAdapterInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559746) (**DXGKQAITYPE\_PAGETABLELEVELDESC**) は、物理アダプターごとにも呼び出されます。

**InputDataSize**と**pInputData**の[ *DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)(**DXGKQAITYPE\_GPUMMUCAPS**) を指す**DXGK\_GPUMMUCAPSIN**します。

**InputDataSize**と**pInputData**の[ *DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)(**DXGKQAITYPE\_PAGETABLELEVELDESC**)指す**DXGK\_PAGETABLELEVELDESCIN**します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[*DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)

 

 






