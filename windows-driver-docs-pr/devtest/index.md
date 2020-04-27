---
title: ドライバー開発ツール
description: ドライバー開発ツール
ms.assetid: 1d384d73-d1d2-445f-8077-40eed1f99a8c
keywords:
- ツール WDK
- ドライバー開発ツール WDK
- WsdCodeGen ツール WDK
- ツール WDK , ドライバーの開発
- Web Services for Devices WDK WIA , ツール
ms.date: 06/28/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: b8cd56c60d940b3f24ed2fef37cbbd850e7e18f2
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "68473384"
---
# <a name="driver-development-tools"></a>ドライバー開発ツール


## <span id="ddk_driver_development_tools_tools"></span><span id="DDK_DRIVER_DEVELOPMENT_TOOLS_TOOLS"></span>


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>目的</strong></p>
<p>Windows Driver Kit (WDK) は、ドライバーの開発、分析、ビルド、インストール、テストに使用できる一連のツールを提供します。 WDK には、開発プロセスでのドライバー コードのエラーの検出、分析、修正のために設計された強力な検証ツールが含まれています。 これらのツールの多くは、開発プロセスのかなり初期に使用でき、非常に重要な役割を果たし、時間と労力を大幅に節約します。</p>
<p><strong>概要</strong></p>
<p>Windows Driver Kit (WDK) は Microsoft Visual Studio 2015 と完全に統合されています。 WDK は、Visual Studio プロジェクトをビルドする場合と同じコンパイラとビルド ツールを使うようになりました。 コード分析と検証のツールを簡単に構成し、Visual Studio 開発環境から起動できるようになったため、開発サイクルの初期にドライバー ソースの問題を見つけて修正することができます。</p>
<p>WDK は、リモート テスト システム上でドライバーを自動的にビルド、展開、テストするために使用できる、高度なドライバー テスト フレームワークと、デバイスの基本的なテストを提供します。 WDK は、ドライバーのテストとデバッグをこれまでより便利で効率的にするツールを提供しています。</p>
<p><strong>ドライバー開発ツールのドキュメント</strong></p>
<p>このセクションでは、開発時に役立つツールと手法について説明します。</p>
<p><a href="tools-for-inf-files.md" data-raw-source="[Tools for INF Files](tools-for-inf-files.md)">INF ファイル用ツール</a></p>
<p><a href="boot-options-for-driver-testing-and-debugging.md" data-raw-source="[Tools for Changing Boot Options for Driver Testing and Debugging](boot-options-for-driver-testing-and-debugging.md)">ドライバーのテストとデバッグ用のブート オプション変更ツール</a></p>
<p><a href="tools-for-testing-drivers.md" data-raw-source="[Tools for Testing Drivers](tools-for-testing-drivers.md)">ドライバーのテスト用ツール</a></p>
<p><a href="tools-for-verifying-drivers.md" data-raw-source="[Tools for Verifying Drivers](tools-for-verifying-drivers.md)">ドライバーの検証用ツール</a></p>
<p><a href="tools-for-software-tracing.md" data-raw-source="[Tools for Software Tracing](tools-for-software-tracing.md)">ソフトウェア トレース用ツール</a></p>
<p><a href="additional-driver-tools.md" data-raw-source="[Additional Driver Tools](additional-driver-tools.md)">その他のドライバー ツール</a></p>
<td align="left"><p><strong>リソース</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Getting Started with Universal Windows Drivers](https://docs.microsoft.com/windows-hardware/drivers)">ユニバーサル Windows ドライバーの概要</a></p>
<p>ユニバーサル Windows ドライバーを使うと、組み込みシステムからタブレットやデスクトップ PC まで、複数の種類のデバイスで動作する 1 つのドライバーを作成できます。 ハードウェア開発者は、フォーム ファクターが違っても、既存のコンポーネントとデバイス ドライバーを使用することができます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Converting WDK 8.1 Projects to WDK 10](https://docs.microsoft.com/windows-hardware/drivers)">WDK 8.1 プロジェクトから WDK 10 への変換</a></p>
<p>WDK 8 や Windows Driver Kit (WDK) 8.1 を使って作成したプロジェクトやソリューションを、Windows Driver Kit (WDK) 10 と Visual Studio 2015 で動作するように変換できます。 プロジェクトやソリューションを開く前に、ProjectUpgradeTool を実行してください。 ProjectUpgradeTool はプロジェクトとソリューションを変換し、WDK for Windows 10 を使って構築できるようにします。</p>
<p></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Validating Universal Windows drivers](https://docs.microsoft.com/windows-hardware/drivers)">ユニバーサル Windows ドライバーの検証</a></p>
<p>ApiValidator.exe ツールを使うと、ドライバーから呼び出される API が、ユニバーサル Windows ドライバーにとって有効であるかどうかを確認できます。 ユニバーサル Windows ドライバーにとって有効な API セットの外部にある API をドライバーが呼び出すと、エラーが返されます。 このツールは、WDK for Windows 10 の一部です。</p>
<a href="wdk-and-visual-studio-build-environment.md" data-raw-source="[WDK and Visual Studio build environment](wdk-and-visual-studio-build-environment.md)">WDK と Visual Studio のビルド環境</a>
<p>ドライバー開発者向けの WDK と Visual Studio ビルド環境の使用に関する詳細情報とヒントは以下で確認できます。</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Developing, Testing, and Deploying Drivers](https://docs.microsoft.com/windows-hardware/drivers)">ドライバーの開発、テスト、および展開</a>
<p>Visual Studio 開発環境でのドライバーの構築、検証ツールの使用、テストに特化した情報を確認できます。</p></td>
</tr>
</tbody>
</table>

 

 

 





