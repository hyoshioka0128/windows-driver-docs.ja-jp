---
title: PwrTest
description: 電源管理テスト ツール (PwrTest) は、テストのツールを実行し、システムの電源管理情報を記録するには、開発者、テスター、およびシステム インテグレーターです。
ms.assetid: 8c242d61-6c5b-44d9-84d1-f78ef9a56a6d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 097114a7782c79d216a3a2adfb0506ad28f267ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553697"
---
# <a name="pwrtest"></a>PwrTest


電源管理テスト ツール (PwrTest) は、テストのツールを実行し、システムの電源管理情報を記録するには、開発者、テスター、およびシステム インテグレーターです。 PwrTest スリープを自動化し、再開の切り替えとプロセッサ電源管理、およびバッテリに関する情報を記録、システム期間に使用できます。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PwrTest はどこでダウンロードできますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PwrTest.exe には、Microsoft Windows Driver Kit (WDK) が含まれています。 WDK の取得方法の詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Driver Kit Downloads]( https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows Driver Kit のダウンロード</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrunningpwrtestspanspan-idrunningpwrtestspanspan-idrunningpwrtestspanrunning-pwrtest"></a><span id="Running_PwrTest"></span><span id="running_pwrtest"></span><span id="RUNNING_PWRTEST"></span>PwrTest を実行しています。


PwrTest (PwrTest.exe) は、堅牢なログ記録とコマンド ライン インターフェイスに機能します。 PwrTest は、Microsoft Windows テスト テクノロジ (WTL) と XML の両方のファイル形式のログ情報のことができます。

PwrTest 機能は、シナリオに分割されます。 これらのシナリオについては、次を参照してください。 [PwrTest シナリオ](pwrtest-scenarios.md)します。

**Pwrtest を実行するには**

1.  PwrTest のすべてのシナリオを使用できるようにするには、まず Visual Studio と WDK を使用してテストするためのテスト コンピューターをプロビジョニングする必要があります。 詳細については、次を参照してください。[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)、または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)します。

    一部のシナリオでは、Windows ドライバー テスト フレームワーク (WDTF) の一部である電源ボタン ドライバーが必要です。 WDTF (および、同梱の電源ボタン ドライバー) は、Visual Studio と WDK を使用してテストするためのシステムをプロビジョニングするときに自動的にインストールします。

2.  PwrTest.exe は WDK と共にインストールされます。 Pwrtest をテスト コンピューターで実行するには、WDK をインストールしたコンピューターから PwrTest.exe をコピーする必要があります。

    Windows ドライバー キットのツール ディレクトリで PwrTest.exe を見つけることができます (たとえば、c:\\Program Files (x86)\\Windows キット\\*&lt;バージョン&gt;* \\ツール\\*&lt;プラットフォーム&gt;*\\PwrTest.exe)。

3.  プロビジョニングした、テスト コンピューターには、管理者特権を持つコマンド プロンプト ウィンドウを開きます (**管理者として実行**) PwrTest.exe をコピーしたディレクトリに移動します。

    **例**

    ```
    pwrtest /? 
    ```

    ```
    pwrtest /battery /c:4 /i:1000
    ```

    詳細については、次を参照してください。 [PwrTest 構文](pwrtest-syntax.md)と[PwrTest シナリオ](pwrtest-scenarios.md)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

[PwrTest ログ ファイル](pwrtest-log-file.md)

[PwrTest シナリオ](pwrtest-scenarios.md)

[ドライバーの展開と (WDK 8.1) をテスト用にプロビジョニングします。](https://msdn.microsoft.com/library/windows/hardware/dn745909)

[ドライバーの展開と (WDK 8) のテスト用にプロビジョニングします。](https://msdn.microsoft.com/library/windows/hardware/hh698272)

 

 






