---
title: DxApi インターフェイスの使用
description: DxApi インターフェイスの使用
ms.assetid: 9de96d20-6cfc-42e7-821b-8256e0dd9b38
keywords:
- カーネルモードビデオトランスポート WDK DirectDraw、DxApi インターフェイスの描画
- DirectDraw カーネルモードビデオトランスポート WDK Windows 2000 display、DxApi インターフェイス
- カーネルモードのビデオトランスポート WDK DirectDraw、DxApi インターフェイス
- video transport カーネルモード WDK DirectDraw、DxApi インターフェイス
- DxApi インターフェイス WDK DirectDraw
- ビデオキャプチャ WDK ビデオトランスポートのカーネルモード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42d0374afc71157c7e01cb106114516586324c89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829252"
---
# <a name="using-the-dxapi-interface"></a>DxApi インターフェイスの使用


## <span id="ddk_using_the_dxapi_interface_gg"></span><span id="DDK_USING_THE_DXAPI_INTERFACE_GG"></span>


「[カーネルモードのビデオトランスポートの使用](using-kernel-mode-video-transport.md)」で説明されているように、ビデオキャプチャドライバー (ハードウェアデコーダー) は、dxapi インターフェイスにアクセスするために、 [**dxapi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)関数を呼び出す必要があります。 「 [VPE とカーネルモードのビデオトランスポートアーキテクチャ](vpe-and-kernel-mode-video-transport-architecture.md)」で説明されているように、[ビデオミニポートドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)は、Windows 2000 以降のプラットフォームで dxapi インターフェイスを実装しています。 次のセクションでは、これらのプラットフォームで DxApi インターフェイスがどのようにサポートされるかについて説明します。

[Windows 2000 以降用の DxApi ミニポートドライバー関数](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)

 

 





