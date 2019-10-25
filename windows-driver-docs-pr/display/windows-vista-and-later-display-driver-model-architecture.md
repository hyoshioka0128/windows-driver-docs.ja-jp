---
title: Windows Display Driver Model (WDDM) のアーキテクチャ
description: Windows Display Driver Model (WDDM) のアーキテクチャ
ms.assetid: 1ae66fd3-8497-4098-9899-c2363671c2b0
keywords:
- ディスプレイドライバーモデル WDK Windows Vista、アーキテクチャ
- Windows Vista display driver model WDK、architecture
- アーキテクチャ WDK ディスプレイ
- ユーザーモード表示ドライバー WDK Windows Vista、アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0156b3cd3424298ffbb1b536484288736f23b27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825184"
---
# <a name="windows-display-driver-model-wddm-architecture"></a>Windows Display Driver Model (WDDM) のアーキテクチャ


## <span id="ddk_longhorn_display_driver_model_architecture_gg"></span><span id="DDK_LONGHORN_DISPLAY_DRIVER_MODEL_ARCHITECTURE_GG"></span>


Windows Vista 以降で使用可能な Windows Display Driver Model (WDDM) のディスプレイドライバーモデルアーキテクチャは、ユーザーモードとカーネルモードの部分で構成されています。 次の図は、WDDM をサポートするために必要なアーキテクチャを示しています。

![wddm アーキテクチャを示す図](images/dx10arch.png)

グラフィックスハードウェアベンダーは、ユーザーモードの表示ドライバーとディスプレイミニポートドライバーを提供する必要があります。 ユーザーモードの表示ドライバーは、Microsoft Direct3D ランタイムによって読み込まれるダイナミックリンクライブラリ (DLL) です。 ディスプレイ*ミニポートドライバー*は、Microsoft DirectX グラフィックスのカーネルサブシステムと通信します。 ユーザーモード表示ドライバーとミニポートドライバーの表示の詳細については、「 [Windows Display Driver Model (WDDM) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_display/)」を参照してください。

 

 





