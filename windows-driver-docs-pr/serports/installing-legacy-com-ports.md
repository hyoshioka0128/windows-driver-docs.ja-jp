---
title: レガシ COM ポートをインストールする
description: レガシ COM ポートをインストールする
ms.assetid: 9cf2a22c-fb4e-4f15-8410-021d2b4f2ce1
keywords:
- レガシ COM ポート WDK シリアルデバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4e01c1b32e488d678e3e2b4bb29f3ca2bed9ea3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842442"
---
# <a name="installing-legacy-com-ports"></a>レガシ COM ポートをインストールする

シリアル関数ドライバーは、常に、レガシシリアルポートを[COM ポート](configuration-of-com-ports.md)として構成します。

シリアルは、 **..\\Services\\シリアル\\Parameters**キーの下にある対応する COM ポートサブキーを読み取って、レガシポートの存在を検出します。 レガシ COM ポートをインストールするには、このキーでデバイスのレガシ COM ポートサブキーを設定する必要があります。 COM ポートのサブキーには、[レガシ com ポートのレジストリ設定](registry-settings-for-a-legacy-com-port.md)が含まれています。

シリアルが読み込まれるときに、レガシポートの**LegacyDiscovered**エントリ値をチェックすることで、以前に検出されなかったレガシポートを特定します。 このエントリ値が存在しない場合、または0の場合、Serial は次のタスクを実行します。

1. [**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)を呼び出して、デバイスをプラグアンドプレイマネージャーに報告します。

2. ポートの**LegacyDiscovered** entry 値を0x00000001 に設定します。これは、ポートが報告されたことを示します。

3. COM ポートサブキーの下にあるエントリ値の一部を、 **IoReportDetectedDevice**によって返される物理デバイスオブジェクト (*PDO*) のプラグアンドプレイデバイスキーにコピーします。

4. シリアルは、プラグアンドプレイデバイスキーの下の**PortName**エントリ値を、レガシ COM ポートサブキーの下にある**dosdevices**エントリ値に設定します。 シリアルコピーを行う他のすべてのエントリ値については、同じエントリ値の名前が保持されます。 シリアルコピーするエントリ値の詳細については、Microsoft Windows Driver Kit (WDK) に用意されているシリアルサンプルコードを参照してください。

**IoReportDetectedDevice**呼び出しは、ポートをルートで列挙されたデバイスとしてマークします。 その後のシステムブート時に、プラグアンドプレイ manager は INF ファイルの情報に基づいてデバイスを自動的に構成します。

プラグアンドプレイ manager は、レガシ COM ポートに対して[互換性のある id](https://docs.microsoft.com/windows-hardware/drivers/install/compatible-ids)として、DETECTEDInternal\\serial、および検出された\\シリアルを作成します。

