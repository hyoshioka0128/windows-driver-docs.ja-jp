---
title: JPEG と PNG 画像の色の管理
description: JPEG と PNG 画像の色の管理
ms.assetid: ece0578d-bf03-4eee-9568-40ef684ba8a7
keywords:
- 印刷の WDK JPEG の色の管理
- 印刷の WDK PNG の色の管理
- CHECKJPEGFORMAT
- CHECKPNGFORMAT
- 圧縮されたイメージ WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be74cf5573c2ea74c487a64cabf8a096e48cb39d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580506"
---
# <a name="color-management-of-jpeg-and-png-images"></a>JPEG と PNG 画像の色の管理





圧縮されたイメージを JPEG や PNG のハードウェアのサポートを提供するプリンターでは、色の管理はドライバーまたはデバイスで処理する必要があり、GDI で処理することはできません。

アプリケーションは、圧縮 JPEG または PNG イメージをプリンターに送信する前にそれがコードを呼び出す ExtEscape いずれかで、CHECKJPEGFORMAT または CHECKPNGFORMAT エスケープします。 これは、結果、ドライバーの呼び出しで[ **DrvQueryDeviceSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff556260)関数、クエリの種類のいずれかの QDS\_CHECKJPEGFORMAT または QDS\_CHECKPNGFORMAT とバッファー圧縮されたイメージを含むです。

ドライバーは、イメージ データを確認し、イメージをサポートできるかどうかを判断できます。 イメージをサポートしている場合は、色変換を実行するも含める必要があります、 [ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)構造体の XO\_デバイス\_ICM フラグまたは XO\_ホスト\_GDI はこのようなイメージに対して色変換を実行することはできませんので、ICM フラグが設定されます。

これらの圧縮されたイメージの通常、イメージ データ内に色領域の情報が含まれます。 YCbCr エンコードであるし、既定の sRGB 領域は十分な概算 JFIF ファイルは例外です。 ただし、JFIF ファイルは、独自のアプリを含む可能性があります*x*場合、ドライバーが、色空間を使用してイメージを変換する必要があります、色空間を指定するマーカー。

JPEG や PNG サポートの詳細については、イメージを圧縮するは、「解説」を参照してください。 [ **DEVINFO**](https://msdn.microsoft.com/library/windows/hardware/ff552835)します。

 

 




