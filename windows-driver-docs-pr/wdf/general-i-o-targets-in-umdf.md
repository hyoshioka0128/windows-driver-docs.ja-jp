---
title: UMDF での一般 I/O ターゲット
description: UMDF での一般 I/O ターゲット
ms.assetid: 46fac165-3afd-4481-b68d-8d3474e0ff52
keywords:
- 一般的な i/o ターゲット WDK UMDF
- I/o ターゲット WDK UMDF、general
- ローカル i/o ターゲット (WDK UMDF)
- リモート i/o ターゲット (WDK UMDF)
- 一般的な i/o ターゲット WDK UMDF、一般的な i/o ターゲットについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5f01e28c9c1526df005dce70ada77977d0caff7
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209932"
---
# <a name="general-io-targets-in-umdf"></a>UMDF での一般 I/O ターゲット


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

一般的な i/o ターゲットは、*ローカル*または*リモート*のどちらでもかまいません。 I/O ターゲットは、USB 要求ブロックなど、特殊なデバイス固有のデータ形式をサポートしていません。 ドライバーは、一般 i/o ターゲットにデータを送信する前に、i/o ターゲットとデバイスが解釈できる形式でデータを書き込みバッファーに格納する必要があります。 同様に、ドライバーが一般的な i/o ターゲットからデータを読み取る場合、ドライバーはターゲットから受信するデータバッファーの内容を解釈できる必要があります。

<a href="" id="local-i-o-targets-------"></a>**ローカル I/o ターゲット**   
ドライバーは、多くの場合、ドライバースタック内の次に小さいドライバーに i/o 要求を送信します。 そのため、各 UMDF ベースのドライバーには、デバイスごとに*既定の i/o ターゲット*があります。これは、デバイスの次の下位のドライバーです。 最下位レベルの UMDF ベースのドライバーの既定の i/o ターゲットは、カーネルモード[リフレクター](overview-of-the-umdf.md)です。

場合によっては、ファイルハンドルベースの i/o ターゲット (ファイルやネットワークソケットなど) に i/o 要求を送信する必要があります。 したがって、フレームワークはファイルハンドルベースの i/o ターゲットオブジェクトも提供します。

既定の i/o ターゲットとファイルハンドルベースの i/o ターゲットはどちらも、*ローカル i/o ターゲット*と呼ばれます。これは、UMDF ベースのドライバーがこれらのターゲットを使用して、ドライバースタックがサポートしているデバイスに i/o 要求を送信するためです。

<a href="" id="remote-i-o-targets-------"></a>**リモート I/o ターゲット**   
場合によっては、ドライバーから別のドライバースタックに i/o 要求を送信する必要があります。 したがって、このフレームワークには、ローカル i/o ターゲットを除くすべての i/o ターゲットで構成される*リモート i/o ターゲット*も用意されています。

リモート i/o ターゲットは、ドライバースタックがサポートしていないデバイス、そのデバイス上のファイル、またはそのデバイスの[デバイスインターフェイス](using-device-interfaces-in-umdf-drivers.md)である可能性があります。

次のセクションでは、一般的な i/o ターゲットを初期化して使用する方法について説明します。

-   [UMDF での一般的な i/o ターゲットの初期化](initializing-a-general-i-o-target-in-umdf.md)
-   [UMDF での一般的な i/o ターゲットへの i/o 要求の送信](sending-i-o-requests-to-a-general-i-o-target-in-umdf.md)
-   [UMDF での一般的な i/o ターゲットの状態の制御](controlling-a-general-i-o-target-s-state-in-umdf.md)
-   [UMDF での一般的な i/o ターゲットに関する情報の取得](obtaining-information-about-a-general-i-o-target-in-umdf.md)

 

 





