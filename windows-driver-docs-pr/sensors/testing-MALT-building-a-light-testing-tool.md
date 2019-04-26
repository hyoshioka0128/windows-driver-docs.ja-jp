---
title: テスト ツール (MALT) 光の構築
author: windows-driver-content
description: このトピックでは、ソリューションをテスト信号として MALT (Microsoft アンビエント光ツール) を使用する方法の手順を提供します。
ms.assetid: d045b771-b536-457c-897b-ecb6517bf0a8
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 81f5d4866cc3244a94a1094ec8fb5a01b21471f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345181"
---
# <a name="building-a-light-testing-tool-malt"></a>テスト ツール (MALT) 光の構築

このトピックを使用して (および必要に応じてビルド) する方法の手順と要件をテストして画面の明るさを調整するツール。 MALT (**M**備えて**A**mbient **L**右**T**ool) 参照提供されます。 

テスト ソリューションにアイデアや概念を活用するため、これらの手順を使用してください。 パブリッシュされた、HLK および他の場所でテストをさらに活用するためのマイクロ コント ローラー API が発行されます。 お客様のフィードバックは、このガイドの機能向上に役立ちます。

![malt デバイス](images/MALT.png)

## <a name="prerequsites"></a>前提条件

このガイドでは、プログラミングでは、はんだ付け、基本的な知識を電子機器にあることを前提します。

## <a name="components"></a>コンポーネント

次のコンポーネント必要があります。

* [マイクロ コント ローラー](https://www.arduino.cc/en/Main/arduinoBoardMega)
* [十分な範囲の光の光源を調整した/スペクトル](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/)
* [光の光源の電源装置](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/#tab/PowerSupplies/subtab/powersupply)
* [アナログ コンバーター (DAC)](https://www.microchip.com/wwwproducts/en/MCP4821)
* 2[アンビエント光センサー (TI OPT3001 ex 以上)](https://www.ti.com/product/OPT3001)
* 2[センサーの色](https://www.digikey.com/product-detail/en/ams/TCS34727FN/TCS34727FNCT-ND/3737677)
* [ライトのエンクロージャ](#light-enclosure)

## <a name="instructions"></a>手順

### <a name="step-1---assemble-light-enclosure"></a>手順 1 - ライトをアセンブル エンクロージャ

(SUT) のテスト対象システムに公開されるライトを制御するには、正確なテストにキーです。 エンクロージャは、使用されている、ライトのパネルと SUT に一致する必要があります。 これは、制御可能な光源の一番上に、下にある SUT 用の領域を絞り、ボックスで構成されます。

![ライトのエンクロージャ](images/box.png)

ラップトップ用に使用した、エンクロージャが 16"x 16"x12"エンクロージャの上部にある 10 の"10"x aperture で発生しました。  [モデル](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Schematics/enclosure)3D 印刷できます。 

#### <a name="light-enclosure-tips"></a>ライトのエンクロージャのヒント

有効な明るいエンクロージャでは、制御された光源からしない環境でテスト対象のパネル (またはデバイス) のキャストにライトのある無菌ライト環境を提供します。 明るいボックスの例を次に示します。

* [カスタムの 3D 印刷ケース](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Schematics/enclosure)
* [記憶域 Tote](http://www.sterilite.com/SelectProduct.html?id=955&ProductCategory=182&section=1)
* 段ボール箱

エンクロージャは SUT に十分な大きさし、光のフィクスチャを上に配置されるか、エンクロージャ内でマウントされている外部のライトの影響から削除する必要があります。

ライトのフィクスチャが (上部) で、ボックスの外側マウントされている場合は、開口部にフィクスチャ対応し、提供のための十分な光 SUT で光センサーを確認してください。

#### <a name="assembly-tips"></a>アセンブリのヒント

* 接着剤の使用が推奨グルーまたはテープがボックス アセンブリの必要がある場合または[マット黒強力テープ](https://en.wikipedia.org/wiki/Gaffer_tape)します。
* エンクロージャは、エンクロージャが上に配置する作業サーフェイスと揃えることを確認します。 外部のライト漏えいいけません。
* エンクロージャに外部の環境光漏えいがあるかどうかを判断する、MALT (と光のエンクロージャでない SUT) からのセンサーを使用します。
* 光の光源は、開口部が必要な場合は、適切なサイズの穴を使用して、ライトをフォール スルーやライトをリークせず、ボックスの上に置くことができますようにします。

### <a name="step-2---assemble-sensors"></a>手順 2 - アセンブル センサー

2 つの光センサー (画面の明るさを測定して、アンビエントの明るさを測定する) と 2 つの色のセンサー (画面の色を測定する 1 つ)、アンビエント色を測定するもう 1 つ、MALT を使用します。 これらを同時に実現、ワイヤに 1 つの光センサーおよびセンサーの 1 つの色がその他の 2 つのセンサーから離れた場所に接続するようにします。 画面のセンサーが下方向に接続するときに (画面上に座って)、その他のセンサー直面しています上方アンビエント ライトを測定します。

![センサーのリモート テスト マシン群](images/sensor.png)

LED ライト パネルを電源に接続し、DAC に接続します。 マイクロ コント ローラーは、制御の強度は、DAC を使用して実現するために、ライトのパネルに送信された電圧を制御できる必要があります。 ツールの接続がどのように行われた次の概略図を使用します。 詳細については、センサー PCB KiCad プロジェクトを参照できます。

![センサーの概略図](images/SensorPCB.png)


### <a name="step-3---connect-the-microcontroller"></a>手順 3 - マイクロ コント ローラーの接続

マイクロ コント ローラーと、PC にマイクロ コント ローラーには、センサーを接続します。 この記事では、(SUT) のテスト対象のシステムと同じであるテストを制御する PC があります。

次の図は、MALT のさまざまな部分は連結されます。

![ブロック図](images/BlockDiagram.png)

MALT PCB、を通じて PCB センサーへの Arduino ボードと光源を接続するできなくなっています。 詳細については、MALT PCB KiCad プロジェクトを参照できます。

![MALT 概略図](images/MaltPCB.png)

### <a name="step-4--start-testing"></a>手順 4-開始のテスト

参照してください[システム明るさの応答をテスト](testing-MALT-system-brightness-response.md)詳細については、セットアップと同様にアセンブルする MALT を使用します。

#### <a name="test-scenarios-to-cover"></a>テスト シナリオに対応するには

* [明るさの自動調整のテスト](testing-MALT-auto-brightness.md)

* [手動テストの明るさ](testing-MALT-manual-brightness.md)

* [システムのシナリオのテスト](testing-MALT-system-scenarios.md)

ISO または VHD ファイルのデバイス パスの見つけ方については、  
[マイクロコント ローラー コマンド](testing-MALT-microcontroller-commands.md)MALT を使用して、カスタムのテストを作成するための api。