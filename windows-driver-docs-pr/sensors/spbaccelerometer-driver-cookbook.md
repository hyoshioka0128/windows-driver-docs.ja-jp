---
title: SpbAccelerometer driver クックブック
description: SpbAccelerometer driver クックブック
ms.assetid: 3E7875E1-0810-4698-A5E1-7A4C6C366967
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f8535839075b5a044505ed95fab17cde7ae94fe
ms.sourcegitcommit: 19ba939a139e8ad62b0086c30b2fe772a2320663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72681932"
---
# <a name="spbaccelerometer-driver-cookbook"></a>SpbAccelerometer driver クックブック


## <a name="get-started"></a>、


このガイドでは、Windows 8.1 以前のオペレーティングシステム (SpbAccelerometer サンプルドライバー) 用に開発されたサンプルの使用を開始する方法について説明します。

>[!NOTE]
> Windows 10 以降のオペレーティングシステムのセンサードライバーのサンプルを評価するには、「[センサーのサンプルドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors)」を参照してください。 Windows 10 以降のオペレーティングシステム用のセンサードライバーを開発して構築する方法の詳細については、「[ユニバーサルセンサードライバーの書き込みと展開](write-and-deploy-your-universal-sensor-driver.md)」を参照してください。

 

まず、サメ Cove board に Windows をインストールします。 加速度計を構成し、サメ Cove board にアタッチします。 次に、Microsoft Visual Studio Express と Windows Driver Kit (WDK) をインストールします。 次に、サンプルドライバーをインストールします。 これらのタスクが完了したら、サンプルドライバーの調査を開始できます。

### <a name="required-hardware"></a>必要なハードウェア

作業を開始する前に、次のハードウェアがあることを確認してください。

-   電源コードとアダプターが付属する Sharks Cove ボード
-   [ADXL345](https://go.microsoft.com/fwlink/p/?linkid=401463)加速度計/ブレイクアウトボード
-   USB ハブ
-   USB キーボード
-   USB マウス
-   USB ネットワーク アダプター
-   モニターおよび HDMI ケーブル (場合によってはアダプターも必要)

### <a name="document-conventions"></a>ドキュメントの表記規則

サンプルドライバーについて説明しているセクションでは、各セクション見出しの後に短いテーブルが表示されます。

![ドキュメントの表記規則](images/document-conventions.png)

これらのテーブルは、そのセクションで説明されているソースモジュールとクラスを識別します。 Visual Studio でモジュールを開き、対応するコードを表示するには、この情報を使用します。

 

 




