---
title: PwrTest
description: 電源管理テストツール (PwrTest) は、開発者、テスト担当者、およびシステムインテグレーターがシステムから電源管理情報を行使して記録できるようにするテストツールです。
ms.assetid: 8c242d61-6c5b-44d9-84d1-f78ef9a56a6d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61078d41b80e86f6476b0304749eba52c40162b0
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769408"
---
# <a name="pwrtest"></a>PwrTest


電源管理テストツール (PwrTest) は、開発者、テスト担当者、およびシステムインテグレーターがシステムから電源管理情報を行使して記録できるようにするテストツールです。 PwrTest を使用すると、スリープを自動化し、遷移を再開して、一定期間内にシステムからのプロセッサ電源管理とバッテリ情報を記録することができます。

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
<td align="left"><p>PwrTest .exe は、Microsoft Windows Driver Kit (WDK) に含まれています。 WDK の入手方法については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Driver Kit Downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows Driver Kit のダウンロード</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrunning_pwrtestspanspan-idrunning_pwrtestspanspan-idrunning_pwrtestspanrunning-pwrtest"></a><span id="Running_PwrTest"></span><span id="running_pwrtest"></span><span id="RUNNING_PWRTEST"></span>PwrTest の実行


PwrTest (PwrTest .exe) は、堅牢なログ記録とコマンドラインインターフェイスを備えています。 PwrTest は、Microsoft Windows Test Technologies (WTL) と XML ファイル形式の両方に情報を記録できます。

PwrTest 機能はシナリオに分割されます。 これらのシナリオの詳細については、「 [Pwrtest のシナリオ](pwrtest-scenarios.md)」を参照してください。

**Pwrtest を実行するには**

1.  すべての PwrTest シナリオを使用できるようにするには、まず、Visual Studio と WDK を使用してテスト用のテストコンピューターをプロビジョニングする必要があります。 詳細については、「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (wdk 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」または「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (wdk 8)](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))」を参照してください。

    一部のシナリオでは、Windows Driver テストフレームワーク (WDTF) の一部である電源ボタンドライバーが必要です。 WDTF (および付属の電源ボタンドライバー) は、Visual Studio と WDK を使用してテスト用にシステムをプロビジョニングするときに自動的にインストールされます。

2.  PwrTest .exe は、WDK と共にインストールされます。 テストコンピューターで Pwrtest を実行するには、WDK がインストールされているコンピューターから PwrTest .exe をコピーする必要があります。

    Pwrtest .exe は、windows Driver Kit Tools ディレクトリにあります (たとえば、C: \\ Program Files (x86) \\ windows kit \\ * &lt; version &gt; * \\ Tools \\ * &lt; platform &gt; * \\ pwrtest .exe)。

3.  プロビジョニングしたテストコンピューターで、昇格したアクセス許可 ([**管理者として実行**]) を使用してコマンドプロンプトウィンドウを開き、PwrTest .exe をコピーしたディレクトリに移動します。

    **例**

    ```
    pwrtest /? 
    ```

    ```
    pwrtest /battery /c:4 /i:1000
    ```

    詳細については、「 [Pwrtest 構文](pwrtest-syntax.md)」と「 [Pwrtest のシナリオ](pwrtest-scenarios.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest の構文](pwrtest-syntax.md)

[PwrTest のログ ファイル](pwrtest-log-file.md)

[PwrTest のシナリオ](pwrtest-scenarios.md)

[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)

[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (WDK 8)](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))

 

 






