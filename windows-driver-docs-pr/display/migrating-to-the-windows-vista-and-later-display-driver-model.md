---
title: Windows Display Driver Model (WDDM) への移行
description: Windows Display Driver Model (WDDM) への移行
ms.assetid: 7f926aa7-1698-4a4e-a1ce-54a316bdc0cd
keywords:
- ドライバー モデル WDK Windows Vista では、表示を移行します。
- Windows Vista のディスプレイ ドライバー モデル、WDK を移行します。
- 移行のディスプレイ ドライバー モデル WDK Windows Vista
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61e17f6a2b21b788cb515780879d5c1622c29930
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390825"
---
# <a name="migrating-to-the-windows-display-driver-model-wddm"></a>Windows Display Driver Model (WDDM) への移行


## <span id="ddk_migrating_to_the_longhorn_display_driver_model_gg"></span><span id="DDK_MIGRATING_TO_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


Windows 表示 Driver Model (WDDM) への移行) には、完全に別の表示とビデオのミニポート ドライバーを記述するためにドライバー作成者が必要です。 ような[Windows 2000 display driver model (XDDM)](windows-2000-display-driver-model-design-guide.md)WDDM が、ペアになっている必要がありますドライバーが表示されミニポート ドライバーを表示します。 ただし、WDDM、ディスプレイ ドライバーはユーザー モードで実行します。 また、モデルが、Windows グラフィックス デバイス インターフェイス (GDI) エンジンのサービスを使用しませんモデルでは、マイクロソフトの Direct3D ランタイムおよび Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) のサービスを使用します。

WDDM は、表示と XDDM に従って記述されたビデオのミニポート ドライバーをサポートします。 ただし、新しいドライバーが可能であれば、Windows Vista 以降で利用可能なソフトウェアとハードウェアの機能を活用するために、WDDM ドライバーとして書き込まれます。

新しいデバイス ドライバー インターフェイス (DDI) を書き直す必要がありますが、ドライバーの作成者は、WDDM ドライバーでの低レベルのハードウェアに依存するコードを再利用できるの関連コードです。 WDDMdrivers を記述する場合は、これらの点を考慮します。

-   ディスプレイのミニポート ドライバーでは、改訂された一連のオペレーティング システムおよび DirectX グラフィックスのカーネル サブシステムと対話するエントリ ポイント関数を実装する必要があります。 詳細については、次を参照してください。 [**ディスプレイ ミニポート ドライバーの DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556157)します。 ディスプレイのミニポート ドライバーでは、任意の文書化されているカーネル関数を呼び出すことができます。

-   ディスプレイのミニポート ドライバーは、適切な DirectX グラフィックスのカーネル サブシステムを動的に読み込みます。 ディスプレイのミニポート ドライバーと DirectX グラフィックスのカーネル サブシステム インターフェイスを介して相互に呼び出します。

-   ディスプレイのミニポート ドライバーでは、最もビデオの (IOCTL) I/O 制御コードを処理する必要なくなりました。 XDDM でカーネル モードのディスプレイ ドライバーは、ビデオのミニポート ドライバーとの通信にこれらのコードを使用します。 WDDM、ユーザー モードのディスプレイ ドライバーは、Direct3D ランタイムと通信します。WDDM グラフィックスのカーネル サブシステムは、ディスプレイのミニポート ドライバーと通信します。
    **注**  次 Ioctl は、WDDM で引き続き使用して、ディスプレイのミニポート ドライバーが処理する必要があります。[**IOCTL\_ビデオ\_クエリ\_色\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff567817)
    [**IOCTL\_ビデオ\_ハンドル\_VIDEOPARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567805)

     

<!-- -->

-   ユーザー モードのディスプレイ ドライバーを実装およびエクスポートする必要があります、 [ **OpenAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff568601)関数で、グラフィックス アダプターのインスタンスを開きます。 ユーザー モードのディスプレイ ドライバーを実装する必要がありますも、 [ **CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540634)関数で、表示状態のコレクションを処理するディスプレイ デバイスの表現を作成します。

-   ユーザー モードのディスプレイ ドライバーの[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)関数、ディスプレイのミニポート ドライバーのと共に[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)関数を置き換える、 [ *DdCanCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549213)、 [ *DdCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549263)、および[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840) XDDM で機能します。

-   ほとんどの残りのユーザー モード ディスプレイ ドライバー関数は、XDDM 用のカーネル モードのディスプレイ ドライバーが次のように実装されるのと同じ機能を実装します。
    -   [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)関数と[ **DP2** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)操作コード
    -   [補正コールバック関数のモーション](https://msdn.microsoft.com/library/windows/hardware/ff568441)と[DirectX ビデオ アクセラレータ構造体](https://msdn.microsoft.com/library/windows/hardware/ff553882)

 

 





