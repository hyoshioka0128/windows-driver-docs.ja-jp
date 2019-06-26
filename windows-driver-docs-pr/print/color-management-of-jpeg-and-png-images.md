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
ms.openlocfilehash: b5849337b4b3b7b56a1fca94f7c1144458d6852c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374671"
---
# <a name="color-management-of-jpeg-and-png-images"></a>JPEG と PNG 画像の色の管理





圧縮されたイメージを JPEG や PNG のハードウェアのサポートを提供するプリンターでは、色の管理はドライバーまたはデバイスで処理する必要があり、GDI で処理することはできません。

アプリケーションは、圧縮 JPEG または PNG イメージをプリンターに送信する前にそれがコードを呼び出す ExtEscape いずれかで、CHECKJPEGFORMAT または CHECKPNGFORMAT エスケープします。 これは、結果、ドライバーの呼び出しで[ **DrvQueryDeviceSupport** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydevicesupport)関数、クエリの種類のいずれかの QDS\_CHECKJPEGFORMAT または QDS\_CHECKPNGFORMAT とバッファー圧縮されたイメージを含むです。

ドライバーは、イメージ データを確認し、イメージをサポートできるかどうかを判断できます。 イメージをサポートしている場合は、色変換を実行するも含める必要があります、 [ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)構造体の XO\_デバイス\_ICM フラグまたは XO\_ホスト\_GDI はこのようなイメージに対して色変換を実行することはできませんので、ICM フラグが設定されます。

これらの圧縮されたイメージの通常、イメージ データ内に色領域の情報が含まれます。 YCbCr エンコードであるし、既定の sRGB 領域は十分な概算 JFIF ファイルは例外です。 ただし、JFIF ファイルは、独自のアプリを含む可能性があります*x*場合、ドライバーが、色空間を使用してイメージを変換する必要があります、色空間を指定するマーカー。

JPEG や PNG サポートの詳細については、イメージを圧縮するは、「解説」を参照してください。 [ **DEVINFO**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)します。

 

 




