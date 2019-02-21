---
title: DirectDraw ドライバー
description: DirectDraw ドライバー
ms.assetid: 6f3343d6-9544-4389-a753-f4520f21a65c
keywords:
- 描画の WDK DirectDraw、DirectDraw ドライバー
- DirectDraw WDK Windows 2000 の表示、DirectDraw ドライバー
- DirectDraw ドライバー WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35e33481ee4302317d53d11aac5d83cd390e64a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551091"
---
# <a name="the-directdraw-driver"></a>DirectDraw ドライバー


## <span id="ddk_the_directdraw_driver_gg"></span><span id="DDK_THE_DIRECTDRAW_DRIVER_GG"></span>


DirectDraw では、デバイスの独立性、DirectDraw ドライバーを提供します。 DirectDraw ドライバーは、通常、ディスプレイ ハードウェアの製造元によって提供されるデバイス固有インターフェイスです。 DirectDraw では、アプリケーションにメソッドを公開し、ハードウェアを直接操作する、ディスプレイ ドライバーの DirectDraw 部分を使用します。 アプリケーション、ディスプレイ ドライバー直接呼び出さないでください。

Windows 2000 以降、DirectDraw、ドライバーは常に 32 ビット コードとして実装されます。 DirectDraw ドライバーは、ディスプレイ ドライバーまたはドライバーの作成者によって定義されたプライベート インターフェイスを通じて、ディスプレイ ドライバーと通信する別の DLL の一部にすることができます。 DirectDraw ドキュメントでは、Windows 2000 以降、DirectDraw ドライバーが含まれている、ディスプレイ ドライバーを前提としています。

DirectDraw ドライバーでは、デバイスに依存するコードのみが含まれ、エミュレーションは実行されません。 関数は、ハードウェアによっては実行されず場合、DirectDraw ドライバーとして報告されませんが、ハードウェアの機能。 さらに、ドライバーが呼び出される前に、DirectDraw ランタイムはこのため、DirectDraw、ドライバーはパラメーターを検証しません。

 

 





