---
title: レガシ COM ポートをインストールする
description: レガシ COM ポートをインストールする
ms.assetid: 9cf2a22c-fb4e-4f15-8410-021d2b4f2ce1
keywords:
- 従来の COM ポートの WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aff01e1f79f2e82c1e67795a98e2d71602600b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383516"
---
# <a name="installing-legacy-com-ports"></a>レガシ COM ポートをインストールする

シリアル関数ドライバーは、常として従来のシリアル ポートを構成、 [COM ポート](configuration-of-com-ports.md)します。

シリアルが下にある対応する COM ポートのサブキーを読み取ることによって従来のポートの存在を検出、 **.\\サービス\\シリアル\\パラメーター**キー。 従来の COM ポートをインストールするには、従来の COM ポート サブキーをこのキーの下のデバイスを設定する必要があります。 COM ポートのサブキーが含まれています、[従来の COM ポートのレジストリ設定](registry-settings-for-a-legacy-com-port.md)します。

レガシ ポートが、以前チェックでは検出されない決定シリアルが読み込まれるときに、 **LegacyDiscovered**レガシ ポートのエントリの値。 このエントリの値が存在しないか、ゼロ場合、シリアルは、次のタスクを実行します。

1. 呼び出し[ **IoReportDetectedDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioreportdetecteddevice)プラグ アンド プレイのマネージャーにデバイスを報告します。

2. セット、 **LegacyDiscovered**ポート、ポートが報告されていることを示します 0x00000001 のエントリの値。

3. 物理デバイス オブジェクトのプラグ アンド プレイ デバイスのキーをコピーする COM ポートのサブキーの下のエントリの値の一部 (*PDO*) によって返される**IoReportDetectedDevice**します。

4. シリアル セット、 **PortName**の値に、プラグ アンド プレイ デバイスのキーの下のエントリの値、 **\dosdevices\z**従来の COM ポートのサブキーの下のエントリの値。 シリアル コピーする他のすべてのエントリ値の同じエントリ値の名前を保持します。 詳細についてはどのエントリの値をシリアル コピーでは、Microsoft Windows Driver Kit (WDK) で提供されるシリアル サンプル コードを参照してください。

**IoReportDetectedDevice**呼び出しは、ルート列挙のデバイスとポートをマークします。 後続のシステムの起動時に、プラグ アンド プレイ マネージャでは、その INF ファイルの情報に基づいて、デバイスが自動的に構成されます。

プラグ アンド プレイ マネージャーは、次を作成します。[互換性 Id](https://docs.microsoft.com/windows-hardware/drivers/install/compatible-ids)従来の COM ポート。DETECTEDInternal\\シリアルと検出された\\シリアルです。

