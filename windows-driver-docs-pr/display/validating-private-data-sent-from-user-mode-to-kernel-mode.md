---
title: ユーザー モードからカーネル モードに送信されるプライベート データの検証
description: ユーザー モードからカーネル モードに送信されるプライベート データの検証
ms.assetid: 7022af7b-80e7-41a5-bd53-32d7eafc4062
keywords:
- WDK の表示、プライベート データの検証
- プライベート データ検証 WDK の表示
- 無効なプライベート データ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 996e3a85697f5d7b7b1661be169b21d900a738b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539665"
---
# <a name="validating-private-data-sent-from-user-mode-to-kernel-mode"></a>ユーザー モードからカーネル モードに送信されるプライベート データの検証


ディスプレイのミニポート ドライバーする必要がありますすべてプライベート データ検証ミニポート ドライバーがクラッシュしていることを防ぐために、ユーザー モードのディスプレイ ドライバーから送信された応答していない (ハング) アサート、またはプライベート データが有効でない場合、メモリの破損します。 ただし、オペレーティング システムでは、「ハング」ハードウェアがリセットされ、ため、表示ミニポート ドライバーに送信する手順については GPU が「ハング」が発生するグラフィックス処理装置 (GPU) プライベート データは、次のものを含めることができます。

-   ミニポート ドライバーの送信バッファーの内容をコマンド[ **DxgkDdiRender** ](https://msdn.microsoft.com/library/windows/hardware/ff559793)または[ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)関数で、 **pCommand**のバッファーのメンバー、 [ **DXGKARG\_レンダリング**](https://msdn.microsoft.com/library/windows/hardware/ff557648)構造体。

-   次のミニポート ドライバー関数に送信されるデータ:
    -   [ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)で機能、 **pPrivateDriverData**バッファーのメンバー、 [ **DXGKARG\_CREATEALLOCATION** ](https://msdn.microsoft.com/library/windows/hardware/ff557559)と[ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)構造体。
    -   [ **DxgkDdiEscape** ](https://msdn.microsoft.com/library/windows/hardware/ff559653)で機能、 **pPrivateDriverData**のバッファーのメンバー、 [ **DXGKARG\_エスケープ**](https://msdn.microsoft.com/library/windows/hardware/ff557588)構造体。
    -   [ **DxgkDdiAcquireSwizzlingRange** ](https://msdn.microsoft.com/library/windows/hardware/ff559582)で機能、 **PrivateDriverData**の 32 ビットのメンバー、 [ **DXGKARG\_ACQUIRESWIZZLINGRANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff557539)構造体。
    -   [ **DxgkDdiReleaseSwizzlingRange** ](https://msdn.microsoft.com/library/windows/hardware/ff559786)で機能、 **PrivateDriverData**の 32 ビットのメンバー、 [ **DXGKARG\_RELEASESWIZZLINGRANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff557644)構造体。
    -   [ **DxgkDdiQueryAdapterInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff559746)で機能、 **pInputData**のバッファーのメンバー、 [ **DXGKARG\_QUERYADAPTERINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff557621)ときに構造体、DXGKQAITYPE\_UMDRIVERPRIVATE 値で指定、**型**メンバー。

 

 





