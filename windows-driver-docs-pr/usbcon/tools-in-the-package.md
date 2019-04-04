---
Description: The goal of device testing is to test device usage against various hub scenarios and systems power states.
title: USB デバイスの MUTT デバイスでのテスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40160a68101b12e60d5398c333c5c4e587201868
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570129"
---
# <a name="usb-device-testing-with-mutt-devices"></a>USB デバイスの MUTT デバイスでのテスト


デバイスのテストの目標は、さまざまなハブ シナリオに対してもデバイスの使用状況をテストして、システムの電源の状態。 MUTT パックおよび SuperMUTT パック デバイスは、別のハブ間でのシナリオとシステムの電源状態のシナリオの接続/切断するデバイスを公開する方法を提供できます。 それぞれに USB 2.0 と 3.0 のハブ MUTT パックおよび SuperMUTT パックのデバイスにアタッチされている場合は、デバイスをテストします。

## <a name="usb-device-testing-prerequisites"></a>USB デバイス テストの前提条件


管理者特権のコマンド プロンプトで MUTT テスト コマンドを実行する前に、次の要件を満たしていることを確認します。

-   テスト システムには、Windows 8 の最新バージョンを実行する必要があります。
-   設定して、MUTT デバイスを構成し、ファームウェアをインストールします。 詳細については、[MUTT テスト ツールを実行するテスト システムを準備する方法](mutt-testing-options.md)を参照してください。

## <a name="suggested-device-tests"></a>デバイスのテストを提案


-   USB 場合電気をテストします。 すべてのテストは、プロトコルと状態の重点を置いています。 参照してください[USB の場合はコンプライアンス プログラム](http://www.usb.org/developers/compliance/)電気的なテストの詳細についてはします。
-   デバイスの基本的なテストです。 詳細については、[MUTT デバイス用の Visual Studio で devfund テストを実行する方法](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)を参照してください。
-   Windows ハードウェア認定キットをコント ローラーをテストします。 詳細については、[USB-IF 証明検証テスト (コント ローラー)](https://go.microsoft.com/fwlink/p/?linkid=316509)を参照してください。
-   セクションで、Windows テスト ガイダンス ドキュメントで見つかった、ホスト コント ローラーの手動テスト_ケース。

## <a name="topologies-for-testing-usb-devices"></a>USB デバイスをテストするためのトポロジ


テスト対象の USB デバイスの次の構成を検討してください。

-   テスト デバイスは SuperMUTT パックのダウン ストリームです。

    ![デバイスが supermutt パックのダウン ストリーム](images/fig13-topology-downstream-supermuttpack.png)

-   テスト デバイスは、MUTT パックのダウン ストリームです。

    ![デバイスが mutt パックのダウン ストリーム](images/fig14-topology-downstream-muttpack.png)

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



