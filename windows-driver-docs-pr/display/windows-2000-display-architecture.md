---
title: Windows 2000 ディスプレイのアーキテクチャ
description: Windows 2000 ディスプレイのアーキテクチャ
ms.assetid: c18e1464-13b7-4e55-b3e1-77aaf9270f60
keywords:
- VGA WDK Windows 2000 の表示
- ディスプレイ ドライバー モデル WDK Windows 2000 では、アーキテクチャ
- Windows 2000 のディスプレイ ドライバー モデル WDK、アーキテクチャ
- アーキテクチャの WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9d1bb10a8645cb33cbdcc884d5d195ddd28f60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391178"
---
# <a name="windows-2000-display-architecture"></a>Windows 2000 ディスプレイのアーキテクチャ


## <span id="ddk_display_architecture_gg"></span><span id="DDK_DISPLAY_ARCHITECTURE_GG"></span>


次の図は、Windows 2000 以降での表示に必要なコンポーネントを示しています。

![windows 2000 以降を示す図は、サブシステムを表示します。](images/dpy1.png)

上記の図で影付きの要素は、Windows 2000 以降に提供されるサービスを表します。 影なしの要素は、サード パーティ製のディスプレイ ドライバーとビデオのミニポート ドライバーが Windows 2000 以降のシステムで表示するグラフィックス アダプターの順序で必要なことを示します。

NT ベースのオペレーティング システムで使用できるグラフィックス カードのすべての型に対して、ディスプレイ ドライバーと対応するビデオのミニポート ドライバーの両方に必要があります。 グラフィックス アダプターが 1 つ (またはアダプターのファミリ) 専用のミニポート ドライバーが書き込まれます。 ディスプレイ ドライバーは、任意の数、共通の描画インターフェイスを共有するアダプターの用として記述できます。たとえば、VGA または ET4000 のいずれかのミニポート ドライバーを使用した、VGA ディスプレイ ドライバーを使用できます。 これは、モードの設定し、ハードウェアのドライバーに関する情報を提供など、ミニポート ドライバーが操作を実行している間、ディスプレイ ドライバーが描画されるためです。 特定のミニポート ドライバーでは; を使用する 1 つ以上のディスプレイ ドライバーのこともできます。たとえば、16 と 256 色 SVGA のディスプレイ ドライバーでは、同じのミニポート ドライバーを使用できます。

次のセクションでは、画面とビデオのミニポート ドライバーの主な責務をについて説明します。 責任の内訳がないと、ハードおよび高速です。モジュール性とパフォーマンスのバランスとは、キーです。 たとえば、VGA ドライバーのハードウェアのポインターのコードは、ミニポート ドライバーで存在します。 これにより、同じのディスプレイ ドライバーは、ハードウェアのポインターを持つ、ビデオの 7 つ VRAM とがサポートするいないと、ET4000 の両方を処理できるように、モジュール性を昇格させます。

[Windows 2000 のディスプレイ ドライバーの責任](windows-2000-display-driver-responsibilities.md)

[Windows 2000 のビデオのミニポート ドライバー責任](windows-2000-video-miniport-driver-responsibilities.md)

 

 





