---
title: Microsoft Bluetooth テストプラットフォーム
description: Bluetooth テストプラットフォーム (BTP) の HID テスト。
ms.assetid: b5b039bb-af0f-446f-9657-aa0e137a3437
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 62dd2fbdbbafef0e8e73534c4ef4a1ae33338599
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528928"
---
# <a name="btp-hid-tests"></a>BTP HID テスト #

BTP HID テストでは、ローカルシステムが BR/EDR または LE を介してリモートラジオとペアリングし、HID 機能を検証する機能がテストされます。

## <a name="setting-up"></a>設定 ##

まず、緑色の電源インジケーター、オプションの黄色いテスト LED、および Traduci の3つのオレンジ色の Led がオンになっていることを確認します。 SUT の Bluetooth ラジオの電源が入っていて、適切なラジオが Traduci に正しく接続されていることを確認します。 現時点では、RN42 radio はジューク中に**のみ**接続できます。 Simlarly Bluefruit radio は JC に**のみ**接続できます。 セットアップの詳細については、「 [BTP の設定](testing-BTP-setup.md)」を参照してください。

サポートされているラジオの情報と購入に関する情報は、[サポートされている BTP ハードウェア](testing-BTP-hw.md)で参照できます。

## <a name="running-the-hid-tests"></a>HID テストの実行 ##

BTP パッケージが抽出されたフォルダーに移動します。 通常は `C:\BTP`の下にあります。 パッケージのバージョンの後にあるという名前のフォルダーでは、次のスクリプトが参照されます。 その後、次のいずれかを実行します。

- 管理者特権のコマンドプロンプトから `RunHidTests.bat <radio name>` するか、
- 管理者特権の PowerShell コンソールからの `RunHidTests.ps1 <radio name>`

使用可能なラジオ名パラメーターの情報については、こちらを参照して[ください](testing-BTP-hw.md#supported-radios)。

また、オプションのパラメーター `-VerboseLogs` を末尾に含めて、BTP の内部操作のより詳細な出力を取得することもできます。

テストが開始されると、12ピンアダプターの横にある赤い LED がオンになると、テストからコマンドが送信されます。 この LED は、すべてのテストの終了時にオフになります。 前回のテストが失敗したために次のテストの開始時にオンになっている場合は、その電源を入れて電源を入れ、既知の状態に戻します。 電源サイクルが失敗した場合、ラジオが不明な状態になっているため、テストは失敗します。

## <a name="capturing-logs"></a>ログのキャプチャ ##

Bluetooth ログをキャプチャするには、GitHub の「 [Bus tools For Windows リポジトリ](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md)」に記載されている手順に従います。

## <a name="known-issues"></a>既知の問題 ##

- ストレステスト: LE ラジオを使用して短いループでテストを実行すると、ペアリングまたはペアリング解除が失敗する可能性があります。
