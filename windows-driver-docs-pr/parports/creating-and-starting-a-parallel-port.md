---
title: パラレル ポートの作成と開始
description: パラレル ポートの作成と開始
ms.assetid: 75c82353-6490-47e9-9278-ec0981af9ae9
keywords:
- パラレル ポート、WDK を作成します。
- 以降、WDK のパラレル ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fe045b0297f967ee4d0bbd42133a770282fc9f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377544"
---
# <a name="creating-and-starting-a-parallel-port"></a>パラレル ポートの作成と開始





プラグ アンド プレイ マネージャーでは、パラレル ポート用のシステムによって提供される関数のドライバーのプラグ アンド プレイのサポートを使用して作成し、開始関数のデバイス オブジェクト (*FDO*) パラレル ポートを表します。

パラレル ポート関数ドライバーは、次を行います。

-   名前付き FDO を作成します。

    パラレル ポート、デバイス名の形式は"\\デバイス\\ParallelPortx"x は、ポート番号の整数値。 パラレル ポート関数ドライバー PortName エントリの値を使用して (REG\_SZ) 並列ポートでポート番号を特定するためのプラグ アンド プレイのレジストリ キーの下。 PortName がある形式"LPTn"、n は、ポートの数、し、"ParallePortx"で x に設定される (n-1) の値に注意してください。 たとえば、"ParallelPort0"は、"LPT1"に関連付けられます。 PortName が正しい形式を持たない場合、デバイス オブジェクトは作成されません。

    "ParallelPortx"デバイス名とは限りませんことに注意してください。 使用をお勧め[ **IoRegisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification) GUID の到着を通知する\_並列\_デバイスのデバイスのインターフェイス。

-   登録し、GUID をできるように\_並列\_パラレル ポートのデバイスのインターフェイス

-   プラグ アンド プレイ マネージャーによって送信されたリソースを検証します。

-   パラレル ポートに接続されている 1284.3 デバイスを初期化します

    パラレル ポート機能のドライバーでは、デイジー チェーンのデバイスの数をカウントし、各デバイスにデイジー チェーン ID を割り当てます。 Microsoft Windows 2000 では、ドライバーは、0 から 3 に Id を割り当てます。 Windows XP では、ドライバーは、0 または 1 の ID を割り当てます。 以降では、パラレル ポートに物理的に最も近いデバイスの昇順でデバイスにデバイス Id が割り当てられます。

-   WDM プロバイダーを FDO と関連付けられている WMI データのブロックとコールバックを登録します。

    パラレル ポート機能のドライバーでは、パラレル ポートの割り当てし、解放の回数を記録します。

-   パラレル ポート ハードウェアでサポートされている通信モードを決定します。

    ハードウェアは以上である必要があります IEEE 1284 と互換性のあります。 ハードウェアがバイト、EPP、ECP モードをサポートしているかどうか、パラレル ポート関数ドライバーを確認します。 EPP がマシンの小さなサブセットでのみサポートされていることに注意してください。

-   パラレル ポートの作業キュー (法 FIFO) を作成します。

    各並列のポートは、独自の作業キューを持っています。 パラレル ポート関数ドライバー キューはのみを割り当てるし、デバイスの要求を選択します。 パラレル ポート関数ドライバー、新しい割り当ての要求または select の要求を受信するときに、ポートは既に割り当てられている場合、要求をキューします。

 

 




