---
title: プリント プロセッサの概要
description: プリント プロセッサの概要
ms.assetid: a34d8daa-b000-4501-8799-5f38cdf38ba4
keywords:
- プリント プロセッサ WDK、プリント プロセッサについて
- WDK のプリント プロセッサのカスタマイズ
- プリント プロセッサ WDK、データ型
- WDK のデータ型のプリント プロセッサ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82e49973eabfd92f91ecffb3b564911b13d788b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537669"
---
# <a name="introduction-to-print-processors"></a>プリント プロセッサの概要





プリント プロセッサは、印刷ジョブの変換、データを送信できる形式にスプールの責任者はユーザー モード Dll、*印刷モニター*します。 担当も一時停止、再開、および印刷ジョブをキャンセルするアプリケーション要求を処理します。

印刷ジョブのスプールされたデータは、操作のスプール ファイルに含まれます。 プリント プロセッサは、ファイルを読み取り、データ ストリームに対する変換操作を実行し、スプーラーに変換されたデータを書き込みます。 次に、スプーラーは印刷適切なモニターにデータ ストリームを送信します。

Microsoft Windows 2000 以降では、次の表に、プリント プロセッサが含まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>プリント プロセッサ</th>
<th>入力データ型</th>
<th>出力のデータ型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Localspl.dll *</p></td>
<td><p>EMF</p>
<p>生</p>
<p>テキスト</p></td>
<td><p>生</p></td>
</tr>
<tr class="even">
<td><p>Sfmpsprt.dll</p></td>
<td><p>PSCRIPT1</p></td>
<td><p>生</p></td>
</tr>
</tbody>
</table>

 

\* Windows 2000 以降、Localmon.dll には Winprint.dll が含まれます Localspl.dll で。

データ型については、次のトピックを参照してください。

[EMF データ型](emf-data-type.md)

[生のデータ型](raw-data-type.md)

[テキストのデータ型](text-data-type.md)

[PSCRIPT1 データ型](pscript1-data-type.md)

Windows 2000 またはそれ以降のオペレーティング システムのバージョンによってサポートされていないデータ型をサポートするためにカスタマイズしたプリント プロセッサを作成することができます。 行うことができますもカスタマイズしたプリント プロセッサ、サポートされているデータ型の 1 つ以上をサポートするため、指定したプリント プロセッサによって提供される機能を変更することができます。

プリント プロセッサに関連付けられているプリンター ドライバー、ドライバーのインストール中に、同じデータ型をサポートしている複数のプリント プロセッサが共存できるようにします。 詳細については、[プリント プロセッサをインストールする](installing-a-print-processor.md)を参照してください。

**注**  プリント プロセッサをコンパイルするときに Unicode フラグを設定します\#UNICODE を定義します。 プリント プロセッサ コードでは、たとえば LPWSTR、型のワイドのみの文字列を使用する必要があります。

 

 

 




