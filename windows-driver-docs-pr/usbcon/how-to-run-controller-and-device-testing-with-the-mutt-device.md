---
Description: The goal of controller testing is to generate a complete set of possible traffic patterns from hubs and devices.
title: USB ホスト コント ローラーの MUTT デバイスでのテスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acb66bf48481da17e45a06d979797a61364c6957
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570538"
---
# <a name="usb-host-controller-testing-with-mutt-devices"></a>USB ホスト コント ローラーの MUTT デバイスでのテスト


コント ローラーのテストの目的では、ハブとデバイスからのトラフィック パターンの完全なセットを生成します。 これにより、コント ローラーと完全にテストするには、そのファームウェアの内部状態ができます。 MUTT デバイスが自動的に可能なプロトコルのさまざまなシナリオを生成する方法を提供することで、テストできます。

## <a name="usb-host-controller-testing-prerequisites"></a>USB ホスト コント ローラーのテスト前提条件


管理者特権のコマンド プロンプトで、MUTT テスト コマンドを実行する前に、次の要件を満たしていることを確認してください。

-   テスト システムには、Windows 8 の最新バージョンを実行する必要があります。
-   設定して、MUTT デバイスを構成し、ファームウェアをインストールします。 詳細については、次を参照してください。 [MUTT テスト ツールを実行するテスト システムを準備する方法](mutt-testing-options.md)します。

## <a name="recommended-usb-host-controller-tests"></a>推奨される USB ホスト コント ローラーのテスト


-   USB 場合電気をテストします。 すべてのテストは、プロトコルと状態の重点を置いています。 参照してください[USB の場合はコンプライアンス プログラム](http://www.usb.org/developers/compliance/)電気的なテストの詳細についてはします。
-   MUTT デバイス MUTT ソフトウェア パッケージに含まれている MUTT ストレスおよび転送テストは、USB コント ローラーの推奨構成で接続されています。 **RunTest.bat**ストレスおよび転送の両方のテストを実行します。 参照してください[ストレスを実行し、MUTT デバイスのパフォーマンス テストを転送する方法](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)します。
-   SuperMUTT パフォーマンスをテストします。 参照してください[スーパー MUTT パフォーマンス テストの実行方法](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md#supermutt-perf)します。
-   デバイスの基本的なテストです。 詳細については、次を参照してください。 [MUTT デバイス用の Visual Studio で devfund テストを実行する方法](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)します。
-   Windows ハードウェア認定キットをコント ローラーをテストします。 詳細については、次を参照してください。 [USB-IF 証明検証テスト (コント ローラー)](https://go.microsoft.com/fwlink/p/?linkid=316509)します。
-   セクションで、Windows テスト ガイダンス ドキュメントで見つかった、ホスト コント ローラーの手動テスト_ケース。

## <a name="topologies-for-usb-host-controller-testing-with-mutt-devices"></a>USB ホスト コント ローラーの MUTT デバイスでのテストのトポロジ


テスト対象の xHCI コント ローラーの次の構成を検討してください。

-   使用可能なすべてのポートには、MUTT デバイスをアタッチします。
-   SuperMUTT および MUTT パック デバイス数が同じが存在するように、使用可能なポートを分割します。 MUTT パックでは、ダウン ストリームの MUTT デバイスをアタッチします。
-   使用可能なポートを半分に SuperMUTTs をアタッチします。 残りのポートに SuperMUTT パック デバイスをアタッチします。 SuperMUTT パックでは、ダウン ストリーム デバイスは SuperMUTT をアタッチします。
-   複雑なトポロジことができます。 たとえば、4 つのポートがあるコント ローラーがあるとします。 次の図は、トポロジの例を示します。

    ![xhci コント ローラーのトポロジの例](images/fig12-xhci-controller-topology.png)

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



