---
title: ボリューム テクスチャの作成処理
description: ボリューム テクスチャの作成処理
ms.assetid: d5f521df-cd52-4c7e-9ad2-5df343c96e8c
keywords:
- WDK DirectX 8.0 のテクスチャ
- Windows 2000 の WDK の表示、ボリュームのテクスチャの DirectX 8.0 リリース ノートします。
- ボリューム テクスチャ WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51953060e48bd859b438e6490123a80a8595ee96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369852"
---
# <a name="handling-the-creation-of-volume-textures"></a>ボリューム テクスチャの作成処理


## <span id="ddk_handling_the_creation_of_volume_textures_gg"></span><span id="DDK_HANDLING_THE_CREATION_OF_VOLUME_TEXTURES_GG"></span>


DirectX の 8.0 が導入されていますが、新しいセキュリティ機能ビット DDSCAPS2\_ボリューム。 このフラグを設定、 **ddsCapsEx.dwCaps2** 、画面のフィールド[ **DD\_画面\_詳細**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)構造体。 [ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))と[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)コールバックの下位ワードで見つかるボリューム テクスチャの深度、**dwCaps4**サーフェスの拡張機能のフィールド (**ddsCapsEx**)、画面の DD の\_画面\_多くの構造。 ドライバーは、「スライス ピッチ」を返す必要があります (つまり、ボリュームの 1 つの 2D スライスから次の位置に追加するバイト数) のボリュームのテクスチャの**dwBlockSizeY**サーフェス グローバル構造体のフィールド。

 

 





