---
Description: The goal of hub testing is to generate a complete set of possible traffic patterns from devices. You can test disconnect scenarios by adding an upstream SuperMUTT pack.
title: USB ハブの MUTT デバイスでのテスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a153cc9039ce5787d07348e8d56a5c7f1ac9b0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532914"
---
# <a name="usb-hub-testing-with-mutt-devices"></a>USB ハブの MUTT デバイスでのテスト


ハブのテストの目的では、デバイスからのトラフィック パターンの完全なセットを生成します。 テストすることができます、アップ ストリームの SuperMUTT パックを追加することでシナリオを切断します。

## <a name="hub-testing-prerequisites"></a>ハブのテストの前提条件


管理者特権のコマンド プロンプトで MUTT テスト コマンドを実行する前に、次の要件を満たしていることを確認します。

-   テスト システムには、Windows 8 の最新バージョンを実行する必要があります。
-   設定して、MUTT デバイスを構成し、ファームウェアをインストールします。 詳細については、[MUTT テスト ツールを実行するテスト システムを準備する方法](mutt-testing-options.md)を参照してください。

## <a name="recommended-hub-tests"></a>テストのハブをお勧めします。


-   USB 場合電気をテストします。 すべてのテストは、プロトコルと状態の重点を置いています。 参照してください[USB の場合はコンプライアンス プログラム](http://www.usb.org/developers/compliance/)電気的なテストの詳細についてはします。
-   MUTT デバイス MUTT ソフトウェア パッケージに含まれている MUTT ストレスおよび転送テストは、USB コント ローラーの推奨構成で接続されています。 **RunTest.bat**ストレスおよび転送の両方のテストを実行します。 参照してください[ストレスを実行し、MUTT デバイスのパフォーマンス テストを転送する方法](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)します。
-   デバイスの基本的なテストです。 詳細については、[MUTT デバイス用の Visual Studio で devfund テストを実行する方法](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)を参照してください。
-   Windows ハードウェア認定キットをコント ローラーをテストします。 詳細については、[USB-IF 証明検証テスト (コント ローラー)](https://go.microsoft.com/fwlink/p/?linkid=316509)を参照してください。
-   セクションで、Windows テスト ガイダンス ドキュメントで見つかった、ホスト コント ローラーの手動テスト_ケース。

## <a name="recommended-topologies-for-hub-testing-with-mutt-devices"></a>MUTT デバイスでのテスト ハブの推奨されるトポロジ


-   使用可能な各ダウン ストリームのポートには、MUTT デバイスをアタッチします。
-   使用可能なポートの半分に SuperMUTTs をアタッチします。 残りのポートには、MUTT デバイスをアタッチします。
-   テスト ハブの SuperMutt パックをアップ ストリームのアタッチし、次の図に示すように、下流のポートが SuperMUTT および MUTT デバイスの数が等しいが。

    ![テストの接続と切断](images/fig14-topology-connect-disconnect.png)

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



