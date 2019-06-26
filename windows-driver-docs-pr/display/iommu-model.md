---
title: IoMmu モデル
description: IoMmu モデルでは、各プロセスには、CPU およびグラフィックス処理装置 (GPU) の間で共有し、OS のメモリ マネージャーによって管理されている 1 つの仮想アドレス空間があります。
ms.assetid: D8D5A2A8-F43A-4EC5-9355-C144EC15E754
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b49bd8fa1a2d4de28651cdda2eb9650a7c9a9001
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372924"
---
# <a name="iommu-model"></a>IoMmu モデル


*IoMmu*モデルの各プロセスが CPU およびグラフィックス処理装置 (GPU) の間で共有し、OS のメモリ マネージャーによって管理されている 1 つの仮想アドレス空間。

メモリにアクセスするには GPU データ要求を送信して、準拠している*IoMmu*します。 要求には、共有仮想アドレスと*プロセス アドレス空間識別子*(PASID)。 *IoMmu*ユニットは、共有のページ テーブルを使用してアドレス変換を実行します。 これは、次に示します。

![iommu プロセス アドレス領域の変換](images/iommu-model.1.png)

カーネル モード ドライバーのサポートの表現、 *IoMmu*モデルを設定して、 [ **DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)::**IoMmuSupported**キャップ。 このフラグが設定されている場合、ビデオ メモリ マネージャーで GPU を使用して任意のプロセスに自動的に登録されます、 *IoMmu*を取得し、 *PASID*そのプロセスのアドレス空間。 *PASID*デバイスの作成時に、ドライバーに渡されます。

プライマリの割り当てによってマップされますビデオ メモリ マネージャー aperture セグメントにする前に表示されたら、ディスプレイのコント ローラーはこれらの割り当てに物理的にアクセスします。

*IoMmu*モデルでは、引き続き、ドライバー、ビデオ メモリ マネージャーを使用して、GPU のビデオ メモリを割り当てる[ *Allocate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)サービス。 これにより、ユーザー モード ドライバー常駐モデルに従う、Microsoft DirectX リソース モデルの共有をサポートして、プライマリ サーフェスがカーネルに表示されるは、開口部に表示される前にマップであることを確認できます。

翻訳の最初のレベル (*リソースのアドレスをタイル*に*CPU/GPU アドレスを共有*)、ユーザー モード ドライバーによってユーザー モードで完全に管理されます。

 

 





