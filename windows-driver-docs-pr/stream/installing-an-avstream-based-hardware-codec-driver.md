---
title: AVStream ベースのハードウェア コーデック ドライバーのインストール
description: AVStream ベースのハードウェア コーデック ドライバーのインストール
ms.assetid: 7b3bbff7-c8e7-47ea-a455-66f01a552e3b
keywords:
- ハードウェアのコーデック サポート WDK AVStream、ドライバーをインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff4b47ff25c9ac37e7f1c15521ccbbf480d1102
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386498"
---
# <a name="installing-an-avstream-based-hardware-codec-driver"></a>AVStream ベースのハードウェア コーデック ドライバーのインストール


AVStream ベースのドライバーをサポートするハードウェア コーデックを持つその他の AVStream ミニドライバーのような INF ファイルを指定します。 ただし、ハードウェア ベンダーは、特定のドライバーの動作を容易に含めることができる 2 つの特定のエントリがあります。

1.  トランス コード トポロジでのみと再生トポロジではなく、デコーダーを使用することを指定するには、ドライバーの INF ファイル、デコーダーの AddReg セクションに、次を追加します。

    ```INF
    [shedVideoDecoder.Reader.AddReg]
    HKR,,CLSID,,%Proxy.CLSID%
    HKR,,FriendlyName,,%shedVideoDecoder.Reader.FriendlyName%
    HKR,,MFTMerit,0x00010001,7
    HKR,Capabilities,"{111EA8CD-B62A-4bdb-89F6-67FFCDC2458B}",0x00010001,1
    ```

    上記のコード例では、再生トポロジでは、デコーダーを除外します。 これには、ハードウェア ベンダーは、エンコーダーを使用するには、そのデコーダーを最適化するための要件があります。

2.  シェルで Windows Media Player (WMP) および Windows 7 のトランス コード機能によって選択されるデコーダー、エンコーダー、またはビデオのプロセッサを有効にするには、次のレジストリ キーを 1 に設定する必要があります。

    ```console
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableDecoders
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableEncoders
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableVideoProcessors
    ```
