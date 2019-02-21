---
title: システムの明るさの応答をテストします。
author: windows-driver-content
description: このトピックでは、ソリューションをテスト信号として MALT (Microsoft アンビエント光ツール) を使用する方法の手順を提供します。
ms.assetid: f0ba2628-8752-467d-abf6-6447668ac244
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9980569f59ce92741a5cfab9db3bf5bb5b84e3ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549639"
---
# <a name="testing-system-brightness-response"></a>システムの明るさの応答をテストします。

このトピックでは、MALT (Microsoft アンビエント光ツール) ツールを使用してシステムの明るさの応答をテストする方法の手順を提供します。

## <a name="test-requirements"></a>テストの要件

1. **完全に組み立てられた MALT します。**   [「方法」ガイド](testing-MALT-building-a-light-testing-tool.md)MALT をビルドまたは既存のテスト装置 MALT の互換性を確保する方法を説明します。

2. **Windows デバイスが、環境光センサーが搭載されています。** 画面の明るさをテストする MALT (または互換性のある) の設計されています。 テスト (SUT) 対象のシステムには、明るさを調整できる必要があります。 [SensorExplorer](https://aka.ms/sensorexplorerblog) Windows によって認識されるセンサーを判断するために使用できます。

## <a name="sensorexplorer"></a>SensorExplorer

使用[SensorExplorer](https://aka.ms/sensorexplorerblog)を環境光センサーの存在を確認します。

![SensorExplorer](images/sensorexplorer.png)

1. **MALT を SUT の USB ポートに接続し、マイクロ コント ローラーに、Arduino プログラムをアップロードします。** MALT の Arduino プログラムで確認できます[GitHub](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT) (HLK) でも。 マイクロ コント ローラーにアップロードします。 開くことが**Arduino** > **ツール** > **シリアル モニター**、いることを確認し、[マイクロ コント ローラー コマンド](testing-MALT-auto-brightness.md)期待どおりに動作します。 次に、しないようにすることは、COM ポート ビジー状態にするために、シリアル モニターを閉じます。

2. **SUT SensorExplorer をインストールします。** SensorExplorer をからダウンロードできます、 [Microsoft store](https://aka.ms/sensorexplorer)します。 
   
> [!Note] 
> 明るさを手動でテストを実行する場合は、ダウンロードから MALTUtil [GitHub](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT)します。 ツールは、HLK でもあります。
   
3. **背景色と SUT をスリープ状態を構成します。**  構成スクリプト[MALT_SUT_Setup.bat](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Code/Scripts)テスト用にデバイスを正しくセットアップされます。  実行の管理者特権でコマンド プロンプトから``MALT_SUT_Setup.bat``スクリプトの指示に従います。

## <a name="test-areas-to-consider"></a>検討すべき点をテストします。

次に考慮すべきその他のテスト区分の一覧を示します。

* 機能性

    * [明るさの自動調整のテスト](testing-MALT-auto-brightness.md)
    * [手動テストの明るさ](testing-MALT-manual-brightness.md)

* ストレス

    * [システムのシナリオのテスト](testing-MALT-system-scenarios.md)

## <a name="malt-sensor-placement"></a>MALT センサーの配置

![MALT センサーの配置](images/placement.png)

次に MALT センサーの配置に関するヒントの一覧を示します。

* SUT の画面で、見開き側に MALT の画面のセンサーを配置します。
* MALT アンビエント センサーには、光源の方向と SUT の画面から離れたを直面する必要があります。 
* SUT の ALS センサーはブロックしません。  オンボード センサーは、MALT またはその他の障害物によってオクルー ジョンいない必要があります。
* ライトの開口部が上方に接続するように、SUT にライトのエンクロージャを置きます。 最適な結果を画面が並列にライトの開口部と光の開口部に接続する必要があります。
* Light する必要がありますがリークするありません、エンクロージャの下部の内外にします。  センサーが引き続き有効であることを確認する再確認してください。
* 内側またはライト エンクロージャ上のいずれかの光源をマウントします。  光源が明るいエンクロージャ上にマウントされている場合は、エンクロージャを光が見やすくなるように、上の開口部にあるボックスに、パネルを配置する必要があります。
* Light する必要がありますがリークするありませんボックスの上部から。 ボックス内でがまったく表示しない場合があります。


参照してください[このホワイト ペーパー](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update)光センサーとアンビエント ライト応答曲線の統合に関する完全なガイダンスについては Microsoft の。