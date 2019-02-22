---
title: MPEG およびプログレッシブ コンテンツ
description: MPEG およびプログレッシブ コンテンツ
ms.assetid: 6973011a-dcee-4411-9382-8c0af2bd85b1
keywords:
- WDK の MPEG ビデオ ポートの拡張機能
- コンテンツの識別をプログレッシブ WDK ビデオ ポートの拡張機能
- PROGRESSIVE_FRAME
- TOP_FIELD_FIRST
- REPEAT_FIRST_FIELD
- DirectX VPE サポート WDK DirectDraw、プログレッシブのコンテンツの識別
- 描画 VPEs WDK DirectDraw、プログレッシブのコンテンツの識別
- DirectDraw VPEs WDK Windows 2000 の表示、プログレッシブのコンテンツの識別
- 拡張機能のビデオ ポート WDK DirectDraw、プログレッシブのコンテンツの識別
- VPEs WDK DirectDraw、プログレッシブのコンテンツの識別
- 3 2 プルダウン WDK のビデオ ポート拡張機能
- プログレッシブのコンテンツを識別します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 867da7bac3ce569becb1388d4e8afcd9b4a90f7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527613"
---
# <a name="mpeg-and-progressive-content"></a>MPEG およびプログレッシブ コンテンツ


## <span id="ddk_mpeg_and_progressive_content_gg"></span><span id="DDK_MPEG_AND_PROGRESSIVE_CONTENT_GG"></span>


Mpeg-2 構文は、累進コンテンツと 3:2 プルダウンを識別するために必要な情報を提供します。 この情報は、次の 1 ビット フラグでは、各フレームのヘッダーに格納されます。

-   プログレッシブ\_フレーム。ときに**TRUE**、同時にインスタント (プログレッシブ フィルム) から (フレーム) の 2 つのフィールドが実際にはことを示します。 ときに**FALSE**、これは、フィールドは、フレーム時間間隔 (インター レースのビデオ) の半分である可能性を示します。

-   上部\_フィールド\_最初。フィールドは早い時間を示します。

-   繰り返し\_最初\_フィールド。3:2 プルダウンのフィールドを繰り返す必要があるかどうかを示します。

VPE と DirectX の最新のリリースで、DirectDraw、ビデオできます常に表示される実行可能では最高品質の場合、これらのフラグ、またはこれらのフラグから派生したシグナルは、フィールド単位でシステムに伝えることができます。 インター レースのビデオは、かどうか、非圧縮ビデオ メディアのサンプルが完全なフレームまたは、フィールドとその他の情報のいずれかを示すためにメディアのサンプルでは新しいフラグを使用、DirectShow によってもサポートできます。 」の説明に従って、 [VPE にインターリーブされるビデオを表示する](displaying-interleaved-video-with-vpe.md) セクションで、DirectShow を指示してフレーム ベースのメディア サンプルまたはメディアのフィールドに基づくサンプルを使用して、フレームごとに表示モードを切り替えることができます。

 

 





