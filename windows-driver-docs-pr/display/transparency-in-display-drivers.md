---
title: ディスプレイ ドライバーの透過性
description: ディスプレイ ドライバーの透過性
ms.assetid: 566706fb-66bd-44f5-b98c-23ed60e27970
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、透過性
- 透明 WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7015f9751dab0a06be349cac512e77556e7e9d11
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353422"
---
# <a name="transparency-in-display-drivers"></a>ディスプレイ ドライバーの透過性


## <span id="ddk_transparency_in_display_drivers_gg"></span><span id="DDK_TRANSPARENCY_IN_DISPLAY_DRIVERS_GG"></span>


ディスプレイ ハードウェアでは、透過性をサポートする場合、ディスプレイ ドライバーを実装する必要があります[ **DrvTransparentBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)します。

ビデオ メモリからの読み取りのコストを減らすためには、ソースと宛先の両方のサーフェスがビデオ メモリ内にある場合、ドライバーはこの関数を実装する必要があります。 ドライバーは、GDI システム メモリから、ビデオ メモリへの透過的なのビット ブロック転送を処理し、GDI も拡張のビット ブロック転送を処理できるようにをできるようにする必要があります。

 

 





