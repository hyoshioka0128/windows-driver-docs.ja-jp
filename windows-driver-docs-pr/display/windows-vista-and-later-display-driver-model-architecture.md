---
title: Windows Display Driver Model (WDDM) のアーキテクチャ
description: Windows Display Driver Model (WDDM) のアーキテクチャ
ms.assetid: 1ae66fd3-8497-4098-9899-c2363671c2b0
keywords:
- ドライバー モデル WDK Windows Vista では、アーキテクチャを表示します。
- Windows Vista display driver モデル WDK、アーキテクチャ
- WDK の表示のアーキテクチャ
- ユーザー モード ドライバー WDK Windows Vista では、アーキテクチャの表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f0d6774937d17cbf1939807252a6086cc392c19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391134"
---
# <a name="windows-display-driver-model-wddm-architecture"></a>Windows Display Driver Model (WDDM) のアーキテクチャ


## <span id="ddk_longhorn_display_driver_model_architecture_gg"></span><span id="DDK_LONGHORN_DISPLAY_DRIVER_MODEL_ARCHITECTURE_GG"></span>


ディスプレイ ドライバー モデルのアーキテクチャの Windows 表示 Driver Model (WDDM)、以降、Windows Vista で利用できるは、ユーザー モードとカーネル モードの部分で構成されます。 次の図は、WDDM をサポートするために必要なアーキテクチャを示しています。

![wddm アーキテクチャを示す図](images/dx10arch.png)

グラフィックス ハードウェアのベンダーには、ユーザー モードのディスプレイ ドライバーとディスプレイのミニポート ドライバーを指定する必要があります。 ユーザー モードのディスプレイ ドライバーは、マイクロソフトの Direct3D ランタイムによって読み込まれるダイナミック リンク ライブラリ (DLL) です。 表示*ミニポート ドライバー* Microsoft DirectX グラフィックスのカーネル サブシステムと通信します。 ユーザー モードのディスプレイ ドライバーとディスプレイのミニポート ドライバーの詳細については、次を参照してください。、 [Windows 表示 Driver Model (WDDM) 参照](https://msdn.microsoft.com/library/windows/hardware/ff570595)します。

 

 





