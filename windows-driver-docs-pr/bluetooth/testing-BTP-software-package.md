---
title: Microsoft Bluetooth テストプラットフォーム
description: Bluetooth テストプラットフォーム (BTP) ソフトウェアパッケージ。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: c7bac36d57a2e95636a126da771ac49a62c6b5e2
ms.sourcegitcommit: cf3440d9d3ebe3d10d77063092d24be8c94573ba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82654856"
---
# <a name="the-btp-software-package"></a>BTP ソフトウェアパッケージ #

BTP ソフトウェアパッケージには、Bluetooth シナリオのテストに使用するツールがいくつか含まれています。

## <a name="download-the-btp-software-package"></a>BTP ソフトウェアパッケージのダウンロード ##

Bluetooth テストプラットフォーム (BTP) ソフトウェアパッケージには、Bluetooth 対応の周辺機器とシステムの Windows Bluetooth スタックとの相互運用性をテストするためのツールが含まれています。 付属のドキュメントでは、ハードウェアを構成する方法の概要と、最適なテストカバレッジのためのトポロジを提案します。 テストを実行し、Bluetooth Windows スタックからトレースイベントを収集する手順について説明します。

[Bluetooth テストプラットフォームソフトウェアパッケージのダウンロード![](images/download.png)](//download.microsoft.com/download/e/e/e/eeed3cd5-bdbd-47db-9b8e-ca9d2df2cd29/BluetoothTestPlatformPack-1.3.1.msi) Bluetooth テストプラットフォームソフトウェアパッケージをダウンロードします。

## <a name="version-updates"></a>バージョンの更新 ##

| Version | [変更点] |
| --- | --- |
| 1.3.1 | <ul><li>A2DP と HFP を行使できるオーディオテストが追加されました。</li><li>Traduci の FPGA によってオーディオボリュームの検証とエラー検出が追加されました。</li><li>テスト名を短く、ユーザーフレンドリ名に変更しました。</li><li>テストの信頼性に対するいくつかの修正と改善。</li><ul> |
| 1.2.1 | <ul><li>BTP をプライベートプレビューからパブリックに移行しています。</li><li>遅延コマンドを実行する Traduci の新機能を示す実験的な SleepTests を追加しました。</li><li>テストの信頼性に対するいくつかの修正と改善。</li><ul> |

## <a name="tools-in-the-package"></a>パッケージ内のツール ##

### <a name="architecture-independent-files"></a>アーキテクチャに依存しないファイル ###

| テストツール | 説明 | ファイル名 |
| --- | --- | --- |
| ConfigureMachineForBtp | <ul><li>CMD スクリプトと PowerShell スクリプトとして提供されます。</li><li>BTP テストを実行するためのテストコンピューターを構成します。</li><li>新しいコンピューターまたは OS のインストールで最初のテストを実行する前に実行することを意図しています。</li> | ConfigureMachineForBtp<br>ConfigureMachineForBtp |
| RunPairingTests | <ul><li>CMD スクリプトと PowerShell スクリプトとして提供されます。</li><li>Bluetooth ペアリングテストを実行します。</li><li>指定されている場合は、カスタム引数をサポートします。</li></ul> | RunPairingTests<br>RunPairingTests |
| RunHIDTests | <ul><li>CMD スクリプトと PowerShell スクリプトとして提供されます。</li><li>Bluetooth HID テストを実行します。</li><li>指定されている場合は、カスタム引数をサポートします。</li></ul> | RunHIDTests<br>RunHIDTests. ps1 |
| RunTaefTest | <ul><li>テスト dll 名とテストパラメーターを指定して、TAEF テストを実行するための PowerShell ヘルパースクリプト。</li></ul> | RunTeafTests. ps1 |
| RunAudioTests | <ul><li>CMD スクリプトと PowerShell スクリプトとして提供されます。</li><li>エラー検出やオーディオボリューム検証などのオーディオテストを実行します。</li><li>指定されている場合はカスタム引数をサポートします</li></ul> | RunAudioTests<br>RunAudioTests. ps1 |

### <a name="architecture-dependent-binaries"></a>アーキテクチャに依存するバイナリ ###

この表に示されているファイルは、X86、AMD64、および ARM64 アーキテクチャで使用できます。 インストーラーによって、アーキテクチャごとに1つのインスタンスが抽出されます。

| テストツール | 説明 | ファイル名 |
| --- | --- | --- |
| HidTests | <ul><li>Bluetooth HID テストのバイナリをテストします。</li><li>TAEF または提供されたスクリプトを使用して実行できます。</li></ul> | TaefHidTests .dll |
| HidInputObserver | <ul><li>HID テストをサポートするために必要なバイナリ。</li></ul> | HidInputObserver のようになります。 |
| LocalRadioAdapter | <ul><li>ローカル Windows Bluetooth ラジオを使用するテストをサポートするために必要なバイナリ。</li></ul> | LocalRadioAdapter のようになります。 |
| TraduciInputOutput | <ul><li>Traduci を使用するテストをサポートするために必要なバイナリ。</li></ul> | TraduciInputOutput のようになります。 |
| PairingTests | <ul><li>Bluetooth ペアリングテストのバイナリをテストします。</li><li>TAEF または提供されたスクリプトを使用して実行できます。</li></ul> | TaefPairingTests |
| SleepTests | <ul><li>Bluetooth スリープテストの実験用テストバイナリ。</li><li>TAEF を使用して実行できます。</li><li> <b>注:</b>これは現在完全にはサポートされていません。</li></ul> | TaefSleepTests |
| AudioTests | <ul><li>Bluetooth オーディオテストのバイナリをテストします。</li><li>TAEF を使用して実行できます。</li></ul> | TaefAudioTests .dll |
| TraduciCmd | <ul><li>デバッグコマンドを含む Traduci の状態を照会および変更するためのコマンドラインツール。</li><li>Traduci ハードウェアのファームウェア更新に使用されます。</li></ul> | TraduciCmd |
