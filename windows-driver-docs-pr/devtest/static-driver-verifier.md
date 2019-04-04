---
title: 静的ドライバー検証ツール
description: 静的ドライバー検証ツール
ms.assetid: 74feeb16-387c-4796-987a-aff3fb79b556
keywords:
- ドライバー WDK、Static Driver Verifier の確認
- ドライバーの検証 WDK、Static Driver Verifier
- Static Driver Verifier WDK
- StaticDV WDK
- SDV WDK
- WDK の SDV のパス
- WDK のコンパイル時の静的検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1c7d189c43fa9d21405ba2ce72d8a13137ea69f
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464212"
---
# <a name="static-driver-verifier"></a>静的ドライバー検証ツール


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>目的</strong></p>
<p>Static Driver Verifier ("StaticDV"または"SDV"とも呼ばれます) は、Windows カーネル モード ドライバーのソース コードを体系的に分析する静的検証ツールです。 SDV は、欠陥およびドライバー設計の問題を検出できるコンパイル時ツールです。 一連のインターフェイスの規則とオペレーティング システムのモデルに基づいて、SDV は、Windows オペレーティング システムのカーネルのドライバーが正しく対話するかどうかを決定します。</p>
<p></p>
 
<p><strong>インストール</strong></p>
<p>Static Driver Verifier はの一部、 <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk">Windows Driver Kit (WDK)</a>両方完全 WDK エクスペリエンスでは、スタンドアロンのエンタープライズ WDK でし。  さらに、 <a href="https://www.microsoft.com/en-us/download/details.aspx?id=40784">for Visual Studio 2013 の Visual C 再頒布可能パッケージ</a>と<a href="https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads">for Visual Studio 2017 の Visual C 再頒布可能パッケージ</a>SDV を実行するために必要な。  
<p></p>バージョンの SDV は、WDK for Windows 10、1809 以前のバージョンで使用できる、 <a href="https://my.visualstudio.com/Downloads?pid=1452">for Visual Studio 2012 の Visual C 再頒布可能パッケージ</a>2017 パッケージではなくインストールする必要があります。
<p></p>
 
</div>
<p><strong>Visual Studio の統合</strong></p>
<p>Static Driver Verifier は、Visual Studio に統合されます。 Visual Studio ドライバーのプロジェクトでは、静的分析を実行できます。 起動、構成、およびから Static Driver Verifier の制御、<strong>ドライバー</strong> Visual Studio のメニュー。</p>
<p><strong>Static Driver Verifier のドキュメント</strong></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/develop/static-driver-verifier-known-issues">Static Driver Verifier の既知の問題</a>
<p>Static Driver Verifier の最新の既知の問題を一覧表示します。</p>
<a href="using-static-driver-verifier-to-find-defects-in-drivers.md" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](using-static-driver-verifier-to-find-defects-in-drivers.md)">Static Driver Verifier を使用してドライバーで障害が検出するには</a>
<p>Visual Studio 環境でドライバー コードの分析を開始する必要がありますがわかります。</p>
<a href="-static-driver-verifier-commands--msbuild-.md" data-raw-source="[Static Driver Verifier commands (MSBuild)](-static-driver-verifier-commands--msbuild-.md)">Static Driver Verifier のコマンド (MSBuild)</a>
<p>Visual Studio コマンド プロンプト ウィンドウでの SDV の実行に使用する MSBuild コマンドが表示されます。</p>
<a href="introducing-static-driver-verifier.md" data-raw-source="[Introducing Static Driver Verifier](introducing-static-driver-verifier.md)">Static Driver Verifier の概要</a>
<p>静的分析ツールの概要を示します。</p>
<a href="using-static-driver-verifier.md" data-raw-source="[Using Static Driver Verifier](using-static-driver-verifier.md)">Static Driver Verifier を使用します。</a>
<p>使用して、静的分析ツールの構成についてを説明します。</p>
<a href="static-driver-verifier-report.md" data-raw-source="[Static Driver Verifier Report](static-driver-verifier-report.md)">Static Driver Verifier のレポート</a>
<p>静的コード分析の詳細なトレースを表示するビューアーについて説明します。</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff552840" data-raw-source="[Static Driver Verifier Rules](https://msdn.microsoft.com/library/windows/hardware/ff552840)">Static Driver Verifier の規則</a>
<p>ルールは、ドライバー モデルと、オペレーティング システムのカーネル インターフェイスの適切な相互作用するための要件を定義します。</p>
<a href="static-driver-verifier-reference.md" data-raw-source="[Static Driver Verifier Reference](static-driver-verifier-reference.md)">Static Driver Verifier の参照</a>
<p>関数のロールの種類、SDV 構成ファイル、エラー、および警告メッセージに関する参照情報を提供します。</p></td>
<td align="left"><p><em>静的分析は、最大で 6 つの要因によって欠陥を減らすことができます!</em></p>
<p>— ため Jones、ソフトウェアの生産性グループ</p>
<p><strong>Windows ドライバー コードのバグの検索</strong></p>
<p>マイクロソフトは、wdk サンプル ドライバーをテストして、Microsoft Windows オペレーティング システムに含まれるカーネル モード ドライバーをテストする SDV を使用します。 Windows 8 のリリースでは、前に、マイクロソフトは、127 の重大なバグの修正を見つけてに SDV を使用します。</p>
<p>SDV は DDI 準拠規則の特定のドライバー モデルを使用して、適切なドライバーの動作を確認できます。 たとえば、SDV を確認できるドライバー。</p>
<ul>
<li><p>適切な IRQL で関数を呼び出す</p></li>
<li><p>取得し、正しい順序でロックを解放します。</p></li>
<li><p>不適切に使用される I/O 要求パケット (IRP) を処理する関数</p></li>
</ul>
<p>SDV は、すべての可能なドライバーのコード パスを検証します。 徹底的なテストにも可能性があるないあいまいなパスで重大なエラーを見つけるために設計されています。</p>
<p><strong>リソース</strong></p>
<p>SDV を検証するドライバーの詳細については、<a href="supported-drivers.md" data-raw-source="[Supported Drivers](supported-drivers.md)">ドライバーのサポートされている</a>を参照してください。</p>
<p>詳細および Static Driver Verifier の使用に関するヒントについては、、<a href="https://go.microsoft.com/fwlink/p/?linkid=154232" data-raw-source="[Static Driver Tools blog](https://go.microsoft.com/fwlink/p/?linkid=154232)">ドライバーの静的ツールのブログ</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 

