---
Description: ハブのテストの目的では、デバイスからのトラフィック パターンの完全なセットを生成します。 テストすることができます、アップ ストリームの SuperMUTT パックを追加することでシナリオを切断します。
title: USB ハブの MUTT デバイスでのテスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82b49279ac5dc285c25870f0cae5c6c040d1cf99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363909"
---
# <a name="usb-hub-testing-with-mutt-devices"></a>USB ハブの MUTT デバイスでのテスト


ハブのテストの目的では、デバイスからのトラフィック パターンの完全なセットを生成します。 テストすることができます、アップ ストリームの SuperMUTT パックを追加することでシナリオを切断します。

## <a name="hub-testing-prerequisites"></a>ハブのテストの前提条件


管理者特権のコマンド プロンプトで MUTT テスト コマンドを実行する前に、次の要件を満たしていることを確認します。

-   テスト システムには、Windows 8 の最新バージョンを実行する必要があります。
-   設定して、MUTT デバイスを構成し、ファームウェアをインストールします。 詳細については、次を参照してください。 [MUTT テスト ツールを実行するテスト システムを準備する方法](mutt-testing-options.md)します。

## <a name="recommended-hub-tests"></a>テストのハブをお勧めします。


-   USB 場合電気をテストします。 すべてのテストは、プロトコルと状態の重点を置いています。 参照してください[USB の場合はコンプライアンス プログラム](https://www.usb.org/compliance)電気的なテストの詳細についてはします。
-   MUTT デバイス MUTT ソフトウェア パッケージに含まれている MUTT ストレスおよび転送テストは、USB コント ローラーの推奨構成で接続されています。 **RunTest.bat**ストレスおよび転送の両方のテストを実行します。 参照してください[ストレスを実行し、MUTT デバイスのパフォーマンス テストを転送する方法](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)します。
-   デバイスの基本的なテストです。 詳細については、次を参照してください。 [MUTT デバイス用の Visual Studio で devfund テストを実行する方法](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)します。
-   Windows ハードウェア認定キットをコント ローラーをテストします。 詳細については、次を参照してください。 [USB-IF 証明検証テスト (コント ローラー)](https://go.microsoft.com/fwlink/p/?linkid=316509)します。
-   セクションで、Windows テスト ガイダンス ドキュメントで見つかった、ホスト コント ローラーの手動テスト_ケース。

## <a name="recommended-topologies-for-hub-testing-with-mutt-devices"></a>MUTT デバイスでのテスト ハブの推奨されるトポロジ


-   使用可能な各ダウン ストリームのポートには、MUTT デバイスをアタッチします。
-   使用可能なポートの半分に SuperMUTTs をアタッチします。 残りのポートには、MUTT デバイスをアタッチします。
-   テスト ハブの SuperMutt パックをアップ ストリームのアタッチし、次の図に示すように、下流のポートが SuperMUTT および MUTT デバイスの数が等しいが。

    ![テストの接続と切断](images/fig14-topology-connect-disconnect.png)

## <a name="related-topics"></a>関連トピック
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



