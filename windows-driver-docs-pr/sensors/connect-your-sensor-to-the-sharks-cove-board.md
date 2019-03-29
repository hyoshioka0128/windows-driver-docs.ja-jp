---
title: サメ Cove 掲示板にセンサーを接続します。
description: このトピックでは、サメ Cove 掲示板にセンサー テスト ボードを接続する方法のガイダンスを提供します。
ms.assetid: B081F4B6-D15E-4F1A-A5C0-E19DA806EAB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4ecd4204e2841db1d5825018d30b8ba4d2cf633
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581389"
---
# <a name="connect-your-sensor-to-the-sharks-cove-board"></a>サメ Cove 掲示板にセンサーを接続します。


このトピックでは、サメ Cove 掲示板にセンサー テスト ボードを接続する方法のガイダンスを提供します。

ADXL345 加速度計シナリオでは、および必要な変更を行った後は、次の図に示すように、サメ Cove に接続されている、加速度計テスト ボードで最終的なります。

![サメ cove と adxl345 加速度計ボードの接続図。](images/sensor-header.png)

センサーのブレイク アウト ボードとサメ Cove 間の安定性と信頼性の高い接続を実現するためには、次の図のようにブレーク アウト ボードにピン 8 単一行男性ヘッダーをはんだ付けによって開始でした。

![8-pin、単一行の男性ヘッダーを示す adxl345 加速度計のブレイク アウト ボードのイメージです。](images/adxl-header.png)

(下記参照)、8 つの女性、女性にジャンパー ワイヤのリボンを使用して、前の接続図に基づく、サメ Cove にセンサーのブレイク アウト ボードを接続します。

![adxl345 センサー brrakout 掲示板とジャンパー ワイヤの 8 ワイヤ女性、女性をセットします。](images/snsr-n-jumpers.png)

方法の例をいくつか次のとおり ADXL345 データ シート、およびサメ Cove 技術仕様 Rev. 1.0 からの情報は、前の図に示すように、接続方法に到着できました。

**J1C1 PIN4**に接続されている**VDD**と**CS**加速度計ボード。

-   **VDD**デジタル インターフェイスの供給電圧の行であります。 デュアル電圧構成では、加速度計を使用しても電力消費量を低く抑えるためにしました。 次の 4 つの使用可能な電圧からその (**J1C1 PIN1 - PIN4**) 2 つの最小の対象としています。 2.8V は、 **J1C1 PIN3**とで 1.8 v **J1C1 PIN4**します。 デュアル電圧の構成で**VDD**よりも低電圧に接続する必要があります**VS**します。 接続したように**VDD**に**J1C1 PIN4**、1.8 v はサメ Cove の行。
-   **CS**は加速度計の通信モード選択 pin です。 結び付ける必要があります、I2C 通信モードを有効にする**CS**をここでは、高**VDD**、これは隠メ諶青の線で変更[準備、センサー テスト ボード](prepare-your-sensor-test-board.md). 変更すると、どちらも**VDD**と**CS**に加速度計ボードから**J1C1 PIN4**、1.8 v 行。

**J1C1 PIN12**に接続されている**SDO**加速度計ボード。

-   ときに、 **SDO**行が高い場合、加速度計掲示板の 7 ビット I2C アドレスは、読み取り/書き込みビット続けて 0x1D します。 ときに、 **SDO** (つまり、最初に接続する) の行が少ない、加速度計掲示板の I2C アドレスは、読み取り/書き込みビット続けて 0x53 します。 Microsoft SPBAccelerometer サンプルでは、された 0x53 のアドレスが使用されることになりました。 いるため、 **SDO**行がアース ピンに接続されている (**J1C1 PIN12**) サメ Cove にします。

上記箇条書きで説明されている接続の決定を情報に基づいていた、*理論上の操作*セクション (ページ 6) と*シリアル通信*ADXL345 データのセクション (8 ページ)シートです。

技術情報についてはサメ Cove ボードに関する詳細を参照してください。[サメ Cove 概略](https://firmware.intel.com/sites/default/files/Sharks_Cove_Schematic.pdf)します。

サメ Cove をボード センサー テストが正常に接続後する方法のガイダンスについては、次のトピックを読む[作成および配置には、ユニバーサル センサー ドライバー](write-and-deploy-your-universal-sensor-driver.md)します。

 

 




