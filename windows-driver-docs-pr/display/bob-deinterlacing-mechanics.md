---
title: Bob のノンインターレース機構
description: Bob のノンインターレース機構
ms.assetid: 1735f9c6-ac83-4a6a-bc6f-4d4a193876dd
keywords:
- bob のノンインターレース化 WDK DirectX VA、機構
- インターリーブフィールド WDK DirectX VA
- stride WDK DirectX VA
- WDK DirectX VA、bob、力学のノンインターレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36cf638e9cf03e4a092c54fd84be1eceb2f37a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839065"
---
# <a name="bob-deinterlacing-mechanics"></a>Bob のノンインターレース機構


## <span id="ddk_bob_deinterlacing_mechanics_gg"></span><span id="DDK_BOB_DEINTERLACING_MECHANICS_GG"></span>


ビットブロック転送を実行できるすべてのグラフィックスアダプターは、簡単な bob スタイルのインターレース解除を行うことができます。 サーフェイスにインターリーブされた2つのフィールドが含まれている場合は、各フィールドを分離するために、サーフェイスのメモリレイアウトを再解釈できます。 これは、元のサーフェイスのストライドを2倍にし、サーフェイスの高さを半分に分割することで実現されます。 2つのフィールドがこのように分離された後は、個々のフィールドを適切なフレームの高さに拡張することで、分割を解除できます。

追加の横方向の拡大または縮小を適用して、ビデオイメージのピクセルの縦横比を修正することもできます。 ディスプレイドライバーは、これを DirectX Video ミキシングレンダラー (VMR) に対して実行できるかどうかを判断できます。 個々のフィールドの高さは、行レプリケーションによって、またはフィルター処理された拡張によって垂直方向に拡張できます。 行レプリケーション方法を使用した場合、結果のイメージの外観はむらになります。 フィルター処理された伸縮が使用されている場合、結果のイメージの外観が若干あいまいになる可能性があります。

次の図は、2つのインターリーブフィールドを含むビデオ画面を示しています。

![2つのインターリーブフィールドを含むサーフェイスのメモリレイアウトを示す図](images/deinterlace.png)

ビデオサンプルに、 **DXVA\_SampleFieldInterleavedEvenFirst**および**DXVA\_SampleFieldInterleavedOddFirst**で指定された2つのインターリーブフィールドが含まれている場合、 [**DXVA\_sampleformat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)列挙体のメンバーでは、次のように、 [**DXVA\_VideoSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample)構造体の**Rtstart**メンバーと**rtend**メンバーを使用して、2番目のフィールドの開始時刻が計算されます。

(**Rtstart** + **rtend**)/2

最初のフィールドの終了時刻は、2番目のフィールドの開始時刻です。

 

 





