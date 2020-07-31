---
title: Microsoft Bluetooth テストプラットフォーム-ペアリング
description: Bluetooth テストプラットフォーム (BTP) のペアリングテスト。
ms.assetid: 19caf4db-9303-47d1-be12-5ff4b2710bc8
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: e3154e5373763e9ee8c4e537affeb56b0672ebe0
ms.sourcegitcommit: 7a7ce6070ed16673108cc64c33b3ddb894453cfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87412515"
---
# <a name="btp-pairing-tests"></a>BTP ペアリングテスト

BTP ペアリングテストでは、ローカルシステムが BR/EDR または LE を介してリモートラジオとのペアリングを組み合わせることができるかどうかをテストします。

## <a name="setting-up-for-testing"></a>設定 (テスト用に)

まず、緑色の電源インジケーター、オプションの黄色いテスト LED、および Traduci の3つのオレンジ色の Led がオンになっていることを確認します。 SUT の Bluetooth ラジオの電源が入っていて、適切なラジオが Traduci に正しく接続されていることを確認します。 現時点では、RN42 無線は、ジューク中に**のみ**接続できます。 Simlarly Bluefruit radio は JC に**のみ**接続できます。 セットアップの詳細については、「 [BTP の設定](testing-BTP-setup.md)」を参照してください。

サポートされているラジオの情報および購入情報については、「 [BTP サポートされているハードウェア](testing-BTP-hw.md)」を参照してください。

## <a name="running-the-pairing-tests"></a>ペアリングテストの実行

BTP パッケージが抽出されたフォルダーに移動します。 通常はになり `C:\BTP` ます。 パッケージのバージョンの後にあるという名前のフォルダーでは、次のスクリプトが参照されます。 その後で、いずれかを実行します。

- `RunPairingTests.bat <radio name>`管理者特権でのコマンドプロンプトまたは
- `RunPairingTests.ps1 <radio name>`管理者特権の PowerShell コンソールから

使用可能なラジオ名パラメーターの情報については[、「BTP の設定](testing-BTP-hw.md#supported-radios)」を参照してください。

また、オプションのパラメーターを末尾に含めて、 `-VerboseLogs` BTP の内部操作の詳細な出力を取得することもできます。

テストが開始されると、12ピンアダプターの横にある赤い LED がオンになると、テストからコマンドが送信されます。 この LED は、すべてのテストの終了時にオフになります。 前回のテストが失敗したために次のテストの開始時にオンになっている場合は、その電源を入れて電源を入れ、既知の状態に戻します。 電源サイクルが失敗した場合、ラジオが不明な状態になっているため、テストは失敗します。

## <a name="capturing-logs"></a>ログのキャプチャ

Bluetooth ログをキャプチャするには、GitHub の「 [Bus tools For Windows リポジトリ](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md)」に記載されている手順に従います。

## <a name="known-issues"></a>既知の問題

- ストレステスト: LE ラジオを使用して短いループでテストを実行すると、ペアリングまたはペアリング解除が失敗する可能性があります。
