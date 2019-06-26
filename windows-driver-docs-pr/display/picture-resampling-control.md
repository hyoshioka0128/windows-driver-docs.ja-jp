---
title: 画像のリサンプリング制御
description: 画像のリサンプリング制御
ms.assetid: 08d74812-3393-4461-91c4-644ecc5ad428
keywords:
- 再サンプリング WDK DirectX VA を画像します。
- コーディングの VA の WDK DirectX 空間の拡張性の高いビデオ
- 再サンプリング WDK DirectX VA の画像を参照します。
- WDK DirectX VA の画像を再サンプリングします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2911efa93b961e1b1f71e4db6dd3687f38e74323
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385567"
---
# <a name="picture-resampling-control"></a>画像のリサンプリング制御


## <span id="ddk_picture_resampling_control_gg"></span><span id="DDK_PICTURE_RESAMPLING_CONTROL_GG"></span>


ときに、 [bDXVA\_Func 変数](bdxva-func-variable.md)が画像の再サンプリングしますが、操作 4 に等しい、指定します。 再サンプリングをアップ サンプルされるとして使用したり、画像を表示または再サンプリングすると、参照の画像のコーディング空間のスケーラブルなビデオなどの目的でこの操作が使用されます。

画像が再サンプリングが実行される H.263 Annex O 空間スケーラビリティまたは H.263 Annex P で使用して指定した画像のエッジでクリッピング、mpeg-2 および mpeg-4 における空間スケーラビリティの形式をいくつかのように画像が再サンプリングの同じメソッドであります。 この関数は、簡単な 2 つタップ分離可能なフィルターを使用します。

再サンプリング コントロールの画像に注意してくださいでは、接続の構成は必要ありません。 その操作には、適切な制限付きモード GUID のサポートのみが必要です。 画像コントロールを再サンプリングは、接続の構成は必要ありません、ために、その操作の最小限の相互運用性のセットを定義する必要がありますはありません。

1 つのバッファー型で定義されて、 [ **DXVA\_PicResample** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_picresample)構造が再サンプリング プロセスを制御します。

 

 





