---
Description: Netmon とも呼ばれます、Microsoft ネットワーク モニターを使用して USB ETW イベントのトレースを表示することができます。
title: Netmon で USB の ETW トレースの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75f450f6d9ce74275554cd812f0c2f184fffe16f
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717014"
---
# <a name="overview-of-usb-etw-traces-in-netmon"></a>Netmon で USB の ETW トレースの概要


Netmon とも呼ばれます、Microsoft ネットワーク モニターを使用して USB ETW イベントのトレースを表示することができます。 ネットワーク モニターでは、トレースを自動的に解析しません。 USB ETW パーサーが必要です。 USB ETW パーサーはテキスト ファイル、ネットワーク モニター パーサーの言語 (NPL) で記述された USB ETW イベントのトレースの構造を記述します。 また、パーサーは、USB に固有の列とフィルターを定義します。 これらのパーサーは、Netmon USB ETW トレースを分析するための最適なツールを作成します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="how-to-install-netmon-and-the-netmon-usb-parser.md" data-raw-source="[How to install Netmon and USB ETW Parsers](how-to-install-netmon-and-the-netmon-usb-parser.md)">Netmon と USB ETW パーサーをインストールする方法</a></p></td>
<td><p>このトピックでは、パーサー Netmon と USB ETW に関するインストール情報を示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-examining-a-trace-file-by-using-netmon.md" data-raw-source="[How to view a USB ETW trace in Netmon](how-to-examining-a-trace-file-by-using-netmon.md)">Netmon で USB の ETW トレースを表示する方法</a></p></td>
<td><p>このトピックでは、例にイベント トレースの方法は Netmon を使用してファイル。 について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="best-practices--debugging-usb-device-problems.md" data-raw-source="[Debugging USB device issues by using ETW events](best-practices--debugging-usb-device-problems.md)">ETW イベントを使用して USB デバイスの問題のデバッグ</a></p></td>
<td><p>このトピックでは、ETW イベントを使用して USB デバイスに関する問題をデバッグするためのヒントを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md" data-raw-source="[Case Study: Troubleshooting an unknown USB device by using ETW and Netmon](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)">ケース スタディ:ETW と Netmon を使用して不明な USB デバイスのトラブルシューティング</a></p></td>
<td><p>このトピックでは、USB ETW と Netmon を使用して、Windows で認識されない USB デバイスをトラブルシューティングする方法の例を示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  



