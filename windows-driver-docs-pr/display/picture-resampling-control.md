---
title: 画像のリサンプリング制御
description: 画像のリサンプリング制御
ms.assetid: 08d74812-3393-4461-91c4-644ecc5ad428
keywords:
- 画像の再サンプリング WDK DirectX VA
- 空間スケーラブルビデオコーディング WDK DirectX VA
- 参照画像の再サンプリング WDK DirectX VA
- 画像の再サンプリング WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 888a62ecd94a8d5ed0afa94ccacdaec5dfd7a8ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829803"
---
# <a name="picture-resampling-control"></a>画像のリサンプリング制御


## <span id="ddk_picture_resampling_control_gg"></span><span id="DDK_PICTURE_RESAMPLING_CONTROL_GG"></span>


[BDXVA\_Func 変数](bdxva-func-variable.md)が4の場合、指定された操作は画像の再サンプリングです。 この操作は、空間スケーラブルビデオコーディング、参照画像の再サンプリング、アップサンプリングまたは表示の画像として使用するための再サンプリングなどの目的で使用されます。

画像の再サンプリングは、「263の付属の空間のスケーラビリティ」で指定されたとおりに実行されます。また、画像の端にクリッピングが適用されています。これは、MPEG 2 と MPEG-4 での空間のスケーラビリティと同じ方法です。 この関数では、単純な2タップの分離可能なフィルター処理を使用します。

画像の再サンプリングコントロールでは、接続構成は必要ありません。 この操作では、適切な制限モード GUID のみがサポートされます。 画像の再サンプリング制御に必要な接続構成がないため、その操作に対して最小限の相互運用性セットを定義する必要はありません。

[**DXVA\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_picresample)の "格納" 構造体で定義された1つのバッファーの種類は、再サンプリングプロセスを制御します。

 

 





