---
title: ビデオ ハードウェアのアンロード
description: ビデオ ハードウェアのアンロード
ms.assetid: 31bea975-1c4b-4157-aec9-49bb7ad69cd0
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、ビデオ ハードウェアのアンロード
- ビデオ ハードウェア アンロード WDK Windows 2000 の表示
- ハードウェアが Windows 2000 の WDK の表示をアンロードします。
- アンロードのビデオ ハードウェア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa7f47616d7556c506af4c114f7902cc2b0e840
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353399"
---
# <a name="unloading-video-hardware"></a>ビデオ ハードウェアのアンロード


## <span id="ddk_unloading_video_hardware_gg"></span><span id="DDK_UNLOADING_VIDEO_HARDWARE_GG"></span>


サーフェスが不要な GDI の呼び出しを[ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)サーフェスを作成して現在のハードウェア デバイスのディスプレイ ドライバーに通知[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)無効にすることができます。 ドライバーは、画面を使用していたすべてのリソースを解放もする必要があります。

GDI を呼び出して、サーフェスを無効にすると、 [ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)ハードウェア デバイスが不要になったドライバーに通知します。 ドライバーの処理中に割り当てられたリソース、メモリを解放し[ **DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)します。

最後に、GDI は呼び出すことによって、ディスプレイ ドライバーを無効にします[ **DrvDisableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)します。 ドライバーは、中に割り当てられているリソースを解放する必要があります[ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)とビデオ ハードウェアを既定の状態に復元します。 ドライバーから返された後、 *DrvDisableDriver*関数、GDI がドライバーのコードとデータがメモリから削除し、ドライバーによって割り当てられたメモリを解放します。

次の図は、GDI のビデオ ハードウェアを無効にするための呼び出し元のシーケンスを示します。

![ビデオ ハードウェアを無効にするかを示す図](images/202-02.png)

 

 





