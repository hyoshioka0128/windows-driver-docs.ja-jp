---
title: UMDF での一般 I/O ターゲット
description: UMDF での一般 I/O ターゲット
ms.assetid: 46fac165-3afd-4481-b68d-8d3474e0ff52
keywords:
- 一般的な I/O ターゲット WDK UMDF
- I/O ターゲット WDK UMDF、[全般]
- ローカルの I/O ターゲット WDK UMDF
- リモートの I/O ターゲット WDK UMDF
- 一般的な I/O に関する一般的な I/O ターゲット WDK の UMDF を対象と
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d35cd8b7f8d79eec794211b7211411cd59ef8c98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573422"
---
# <a name="general-io-targets-in-umdf"></a>UMDF での一般 I/O ターゲット


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

一般的な I/O ターゲットでは、いずれかになります*ローカル*または*リモート*、I/O ターゲットが USB 要求のブロックなどの特殊なデバイスに固有のデータ形式をサポートしていません。 ドライバーは、一般的な I/O ターゲットにデータを送信、前に、I/O のターゲットとデバイスを解釈できる形式での書き込みバッファーにデータを配置する必要があります。 同様に、ドライバーは、一般的な I/O ターゲットからのデータを読み取り、ときに、ドライバーは、ターゲットから受け取ったデータ バッファーの内容を解釈することである必要があります。

<a href="" id="local-i-o-targets-------"></a>**ローカルの I/O ターゲット**   
ドライバーは、次の下位ドライバーはドライバー スタックに多くの場合、I/O 要求を送信します。 したがって、それぞれ UMDF ドライバーは、 *I/O の既定のターゲット*デバイスごとに、これは、デバイスの次の下位ドライバー。 最下位レベルの UMDF ベースのドライバーの既定の I/O ターゲットは、カーネル モード[reflector](overview-of-the-umdf.md)します。

場合があります UMDF ドライバーでは、ファイルやネットワーク ソケットなどファイル ハンドル ベースの I/O ターゲットに I/O 要求を送信する必要があります。 そのため、フレームワークには、I/O ターゲット オブジェクトのファイル ハンドル ベースも提供します。

I/O の既定のターゲットと I/O ターゲットのファイル ハンドル ベースの両方が呼び出されます*ローカル I/O ターゲット*UMDF ベースのドライバーでは、これらのターゲットを使用して、I/O 要求をドライバー スタックでサポートされるデバイスに送信するためです。

<a href="" id="remote-i-o-targets-------"></a>**リモートの I/O ターゲット**   
場合によっては、ドライバーは、別のドライバー スタックに、I/O 要求を送信する必要があります。 また、framework にはそのため、*リモートの I/O ターゲット*のすべてのローカルの I/O ターゲットを除く I/O ターゲットで構成されます。

リモートの I/O ターゲット ドライバー スタックがサポートされていないデバイス、そのデバイス上のファイルがありますまたは[デバイス インターフェイス](using-device-interfaces-in-umdf-drivers.md)デバイスにします。

次のセクションでは、初期化、および一般的な I/O ターゲットを使用する方法について説明します。

-   [UMDF で一般的な I/O ターゲットの初期化](initializing-a-general-i-o-target-in-umdf.md)
-   [UMDF で一般的な I/O ターゲットへの I/O 要求を送信します。](sending-i-o-requests-to-a-general-i-o-target-in-umdf.md)
-   [UMDF で一般的な I/O ターゲットの状態を制御します。](controlling-a-general-i-o-target-s-state-in-umdf.md)
-   [UMDF で一般的な I/O ターゲットに関する情報を取得します。](obtaining-information-about-a-general-i-o-target-in-umdf.md)

 

 





