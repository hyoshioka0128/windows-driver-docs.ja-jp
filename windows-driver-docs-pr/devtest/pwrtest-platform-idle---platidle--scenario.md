---
title: PwrTest のプラットフォーム アイドル シナリオ
description: PwrTest プラットフォームのアイドル状態のシナリオ (/platidle) をポーリングし、コンピューターでサポートされている場合、プラットフォームのアイドル状態の遷移の数をログインしようとしています。
ms.assetid: 71A3AB26-AAC5-46DB-99A3-6693D5AF5AC9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c2a477c5a1ff8ad446ac8bdee6aeaa9238345b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360096"
---
# <a name="pwrtest-platform-idle-scenario"></a>PwrTest のプラットフォーム アイドル シナリオ


PwrTest プラットフォームのアイドル状態のシナリオ (**/platidle**) をポーリングし、コンピューターでサポートされている場合、プラットフォームのアイドル状態の遷移の数をログインしようとしています。

このシナリオは、コンピューターを使用中に発生するプラットフォームのアイドル状態の遷移を追跡するために役立ちます。 このシナリオは、システムは、(電源ボタンを使用して手動で入力された) 場合、アイドル状態の詳細なプラットフォームが入る場合は診断にも役立ちます。

**/Platidle**シナリオでは、コンピューターのサポートがある必要があります、*常に常時接続されている*(AoAc) 電源機能。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /platidle  [/t:n] [/i:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

<span id="_i_n"></span><span id="_I_N"></span>**/i:**<em>n</em>  
ポーリング間隔を秒単位でプラットフォームのアイドル状態の統計情報の収集を指定します (既定値の*n*は 5 秒です)。

**使用例**

```
pwrtest /platidle /t:60
```

```
pwrtest /platidle
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PlatIdle> 
    <PlatformIdleStats StateCount="X" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX">
        <State Index="X" SuccessCount="X" FailureCount="X" CancelCount="X"/>
    </PlatformIdleStats>
  </PlatIdle>
</PwrTestLog> 
```

次の表では、ログ ファイルに表示される XML 要素について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要素</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>&lt;PlatIdle&gt;</strong></td>
<td align="left"><p>すべてのプラットフォームのアイドル状態統計情報が含まれています。 1 つしかない<strong>&lt;PlatIdle&gt;</strong> PwrTest ログ ファイル内の要素</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PlatformIdleStats&gt;</strong></td>
<td align="left"><p>アイドル状態の統計情報ブロックのプラットフォームです。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






