---
title: 従来の COM ポートをインストールします。
description: 従来の COM ポートをインストールします。
ms.assetid: 9cf2a22c-fb4e-4f15-8410-021d2b4f2ce1
keywords:
- 従来の COM ポートの WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffec5a3b5ba2e6b683702d13dbec7b96afe533e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532031"
---
# <a name="installing-legacy-com-ports"></a>従来の COM ポートをインストールします。





シリアル関数ドライバーは、常として従来のシリアル ポートを構成、 [COM ポート](configuration-of-com-ports.md)します。

シリアルが下にある対応する COM ポートのサブキーを読み取ることによって従来のポートの存在を検出、 **.\\サービス\\シリアル\\パラメーター**キー。 従来の COM ポートをインストールするには、従来の COM ポート サブキーをこのキーの下のデバイスを設定する必要があります。 COM ポートのサブキーが含まれています、[従来の COM ポートのレジストリ設定](registry-settings-for-a-legacy-com-port.md)します。

レガシ ポートが、以前チェックでは検出されない決定シリアルが読み込まれるときに、 **LegacyDiscovered**レガシ ポートのエントリの値。 このエントリの値が存在しないか、ゼロ場合、シリアルは、次のタスクを実行します。

1.  呼び出し[ **IoReportDetectedDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549597)プラグ アンド プレイのマネージャーにデバイスを報告します。

2.  セット、 **LegacyDiscovered**ポート、ポートが報告されていることを示します 0x00000001 のエントリの値。

3.  物理デバイス オブジェクトのプラグ アンド プレイ デバイスのキーをコピーする COM ポートのサブキーの下のエントリの値の一部 (*PDO*) によって返される**IoReportDetectedDevice**します。

4.  シリアル セット、 **PortName**の値に、プラグ アンド プレイ デバイスのキーの下のエントリの値、 **\dosdevices\z**従来の COM ポートのサブキーの下のエントリの値。 シリアル コピーする他のすべてのエントリ値の同じエントリ値の名前を保持します。 詳細についてはどのエントリの値をシリアル コピーでは、Microsoft Windows Driver Kit (WDK) で提供されるシリアル サンプル コードを参照してください。

**IoReportDetectedDevice**呼び出しは、ルート列挙のデバイスとポートをマークします。 後続のシステムの起動時に、プラグ アンド プレイ マネージャでは、その INF ファイルの情報に基づいて、デバイスが自動的に構成されます。

プラグ アンド プレイ マネージャーは、次を作成します。[互換性 Id](https://msdn.microsoft.com/library/windows/hardware/ff539950)従来の COM ポート。DETECTEDInternal\\シリアルと検出された\\シリアルです。

 

 




