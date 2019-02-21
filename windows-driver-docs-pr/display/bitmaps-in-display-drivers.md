---
title: ディスプレイ ドライバーのビットマップ
description: ディスプレイ ドライバーのビットマップ
ms.assetid: 3f0ed208-1cfb-4583-beaf-894cd210b459
keywords:
- ドライバー WDK Windows 2000 では、ビットマップを表示します。
- Windows 2000 の WDK のビットマップを表示します。
- ビット ブロック転送 WDK Windows 2000 の表示
- オフスクリーン メモリ WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 300dd7096c60a7095a7e44a6d71da51ef20305b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532704"
---
# <a name="bitmaps-in-display-drivers"></a>ディスプレイ ドライバーのビットマップ


## <span id="ddk_bitmaps_in_display_drivers_gg"></span><span id="DDK_BITMAPS_IN_DISPLAY_DRIVERS_GG"></span>


16 色 VGA ディスプレイなどの特定のデバイスは、非標準のビットマップのビット ブロック転送をより迅速に実行できます。 これをサポートするドライバーが接続できる**DrvCreateDeviceBitmap**します。

**DrvSaveScreenBits**します。 これらのドライバーが接続できる**DrvSaveScreenBits**ドライバーを保存または復元するときにすばやくメニュー詳細の表示の画像の四角形を指定するために呼び出すことができます、またはダイアログ ボックスが表示されます。

**注**  ビット ブロック転送呼び出しでは、GDI (ドライバーではなく) 処理*ポインター除外*と*クリップ領域ロック*します。

 


ドライバーのデバイスのビットマップを実装する[*オフスクリーン メモリ*](video-present-network-terminology.md#off_screen_memory)システムのパフォーマンスを大幅に向上させることができます。 デバイスがオフスクリーン ビットマップには、によってシステム パフォーマンスが向上します。

-   GDI の代わりにアクセラレータ ハードウェアを使用して、描画します。

-   画面に対してビットマップのビット ブロック転送の速度を向上させます。

-   (画面外のメモリに格納されているビットマップはメイン メモリでスペースが占有されていない) メイン メモリの需要を削減します。

-   マスク ビット ブロック転送し、ダブル バッファリングなど、OpenGL をサポートする操作を実行するハードウェアを活用できます。


ドライバーによってオフスクリーン メモリでデバイスのビットマップを実装する必要があります[ **DrvCreateDeviceBitmap**](https://msdn.microsoft.com/library/windows/hardware/ff556185)します。

 

 





