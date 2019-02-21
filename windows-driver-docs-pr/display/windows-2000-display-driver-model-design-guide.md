---
title: Windows 2000 Display Driver Model (XDDM) 設計ガイド
description: Windows 2000 Display Driver Model (XDDM) 設計ガイド
ms.assetid: 24cb232b-e289-45c8-8d55-42614a4dfd54
keywords:
- WDK のデバイスを表示します。
- ディスプレイ ドライバー モデル WDK Windows 2000
- Windows 2000 のディスプレイ ドライバー モデル WDK
- ディスプレイ ドライバー WDK、Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9215569fd9aedb45b36a8246a7c21f89d1cd8b72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530249"
---
# <a name="windows-2000-display-driver-model-xddm-design-guide"></a>Windows 2000 Display Driver Model (XDDM) 設計ガイド


## <span id="ddk_windows_2000_display_driver_model_gg"></span><span id="DDK_WINDOWS_2000_DISPLAY_DRIVER_MODEL_GG"></span>


Windows Vista で実行されるディスプレイ アダプター ドライバーが 2 つのモデルのいずれかに従うことができます。 [Windows 表示 Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)または Windows 2000 display driver model (XDDM)。 Windows Display Driver Model (WDDM) に準拠しているドライバーでは、Windows Vista でのみ以降を実行します。 XDDM に準拠しているドライバーは、Windows 2000 以降のオペレーティング システムが (Windows Vista および Windows 7 を含む) で実行されます。

**注**  XDDM と VGA ドライバーは、Windows 8 およびそれ以降のバージョンではコンパイルされません。 ディスプレイ ハードウェアが認定 WDDM 1.2 をサポートする、またはそれ以降であるドライバーがない Windows 8 コンピューターに接続されている場合は、Microsoft Basic 表示ドライバーを実行しているシステムが既定値です。

 

次のセクションでは、Windows 2000 のディスプレイ ドライバー モデルについて説明します。

-   [表示 (Windows 2000 モデル) の概要](introduction-to-display--windows-2000-model-.md)

-   [ディスプレイ ドライバー (Windows 2000 モデル)](display-drivers--windows-2000-model-.md)

-   [DirectDraw](directdraw.md)

-   [Direct3D DDI](direct3d.md)

-   [DirectX のビデオの高速化](directx-video-acceleration.md)

-   [Windows 2000 Display Driver Model でのビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)

-   [実装のヒントと Windows Display Driver Model (WDDM) の要件](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)

-   [GDI](gdi.md)

**注**   Windows 2000 のディスプレイ ドライバー モデルのドキュメントが、Microsoft Windows 98 で実行されているディスプレイ ドライバーを作成する方法についての情報が含まれなく/Me プラットフォーム。 Windows 98 のディスプレイ ドライバーを作成するかどうか、自分で使用できるリリース WDK ドキュメント Windows Vista/。 WDK の Windows Vista RTM から取得できます、 [Microsoft Connect web サイト](https://go.microsoft.com/fwlink/p/?linkid=101629)します。

 

 

 





