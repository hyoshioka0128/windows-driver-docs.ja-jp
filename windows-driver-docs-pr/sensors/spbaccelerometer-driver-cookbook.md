---
title: SpbAccelerometer ドライバー クックブック
description: SpbAccelerometer ドライバー クックブック
ms.assetid: 3E7875E1-0810-4698-A5E1-7A4C6C366967
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acfe2ad3fbaf7a32d05485e33b6a05b0a419a8bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324822"
---
# <a name="spbaccelerometer-driver-cookbook"></a>SpbAccelerometer ドライバー クックブック


## <a name="get-started"></a>はじめに


このガイドでは、Windows 8.1 およびそれ以前のオペレーティング システム (SpbAccelerometer サンプル ドライバー) 用に開発したサンプル ドライバーの使用を開始する方法を示します。

>[!NOTE]
> Windows 10 および以降のオペレーティング システム用センサー ドライバーのサンプルを評価するため、次を参照してください。[センサー サンプル ドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors)します。 開発および Windows 10 および以降のオペレーティング システム用センサー ドライバーをビルドする方法については、次を参照してください。[作成および配置には、ユニバーサル センサー ドライバー](write-and-deploy-your-universal-sensor-driver.md)します。

 

によって、サメ Cove ボード上で Windows をインストールするようになります。 加速度計を構成し、サメ Cove 掲示板にアタッチします。 次に、Microsoft Visual Studio Express と Windows Driver Kit (WDK) にインストールします。 次に、サンプル ドライバーをインストールします。 これらのタスクが完了すると、ドライバーのサンプルを探索を開始できます。

サメ Cove ボードの詳細については、次を参照してください。 [SharksCove.org](https://go.microsoft.com/fwlink/p/?linkid=403167)します。

### <a name="required-hardware"></a>必要なハードウェア

開始する前に、次のハードウェアを確認してください。

-   電源コードとアダプターが付属する Sharks Cove ボード
-   [ADXL345](https://go.microsoft.com/fwlink/p/?linkid=401463)加速度計/ブレーク アウト ボード
-   USB ハブ
-   USB キーボード
-   USB マウス
-   USB ネットワーク アダプター
-   モニターおよび HDMI ケーブル (場合によってはアダプターも必要)

### <a name="document-conventions"></a>ドキュメントの表記規則

セクションでは、ドライバーのサンプルを記述するには、各セクションの見出しの後に簡単なテーブルがわかります。

![ドキュメントの表記規則](images/document-conventions.png)

これらのテーブルでは、ソースのモジュールとそのセクションで説明したクラスを特定します。 モジュールを開くし、Visual Studio での対応するコードを表示するには、この情報を使用します。

 

 




