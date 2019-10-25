---
title: IoMmu モデル
description: IoMmu モデルでは、各プロセスには、CPU とグラフィックス処理ユニット (GPU) の間で共有され、OS メモリマネージャーによって管理される仮想アドレス空間が1つあります。
ms.assetid: D8D5A2A8-F43A-4EC5-9355-C144EC15E754
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb63e371ec1554dab3aca75bb19d696e125c717b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840339"
---
# <a name="iommu-model"></a>IoMmu モデル


*IoMmu*モデルでは、各プロセスには、CPU とグラフィックス処理ユニット (GPU) の間で共有され、OS メモリマネージャーによって管理される仮想アドレス空間が1つあります。

メモリにアクセスするために、GPU は準拠している*IoMmu*にデータ要求を送信します。 要求には、共有仮想アドレスと*プロセスアドレス空間識別子*(パスワード id) が含まれています。 *IoMmu*単位は、共有ページテーブルを使用してアドレス変換を実行します。 次に例を示します。

![iommu プロセスのアドレス空間の変換](images/iommu-model.1.png)

カーネルモードドライバーは、 [**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)::**IoMmuSupported** caps を設定することによって、 *IoMmu*モデルのサポートを表します。 このフラグが設定されている場合、ビデオメモリマネージャーは、GPU を使用して自動的にプロセスを登録し、そのプロセスのアドレス空間の*id*を*取得します*。 デバイスの作成中に、パスワード*id*がドライバーに渡されます。

プライマリ割り当ては、ビデオメモリマネージャーによって表示される前に、ディスプレイコントローラーがこれらの割り当てに物理的にアクセスできることを確認するためにマップされます。

*IoMmu*モデルでは、ドライバーはビデオメモリマネージャーの[*割り当て*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)サービスを使用して、GPU のビデオメモリを引き続き割り当てます。 これにより、ユーザーモードドライバーは、常駐モデルに従うことができ、Microsoft DirectX リソース共有モデルがサポートされます。また、プライマリサーフェイスがカーネルに認識され、表示される前にアパーチャにマップされます。

最初のレベルの翻訳 (*共有 CPU/GPU アドレス*への*タイルリソースアドレス*) は、ユーザーモードドライバーによってユーザーモードで完全に管理されます。

 

 





