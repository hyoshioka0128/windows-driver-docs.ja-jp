---
title: Tracelog Enumguid の表示
description: Tracelog Enumguid の表示
ms.assetid: 9bb93238-98f7-4422-8434-b4dc105ec008
keywords:
- Tracelog WDK、providers
- プロバイダー WDK ソフトウェアトレース
- WDK のトレース, プロバイダ
- -enumguid コマンド
- enumguid コマンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36450bb7e1d880260b09d4dfbd312b694cf54fbc
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769698"
---
# <a name="tracelog-enumguid-display"></a>Tracelog Enumguid の表示

**トレースログ-enumguid**コマンドを送信すると、トレースログには、Windows イベントトレーシング (ETW) に[登録](registered-provider.md)されている、実行中のトレースプロバイダーの一覧が表示されます。 表示は非常に便利ですが、誤って解釈されることがよくあります。

### <a name="span-idwhich_providers_appear_in_the_display_spanspan-idwhich_providers_appear_in_the_display_spanwhich-providers-appear-in-the-display"></a><span id="which_providers_appear_in_the_display_"></span><span id="WHICH_PROVIDERS_APPEAR_IN_THE_DISPLAY_"></span>ディスプレイに表示されるプロバイダー

Tracelog enumguid 表示には、トレースセッションに対して有効にできるプロバイダーの一部が一覧表示されますが、完全な一覧ではありません。 これには、を実行していて、ETW に登録されているトレースプロバイダーだけが含まれます。

表示には、次のプロバイダーは含まれていません。

システムで使用できるが、通常は実行されていないために登録されていないトレースプロバイダー。

トレースセッションに対して有効になっているが、現在実行されていないトレースプロバイダー。 (これらは、*事前有効化*または*事前登録*されたプロバイダーと呼ばれることがよくあります)。これには、必要に応じて読み込みおよびアンロードされる Dll など、継続的に実行されないプロバイダーが含まれます。

[グローバルロガートレースセッション](global-logger-trace-session.md)および[NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)用のシステムセッションおよびプロバイダーのプロバイダーを含む、Windows に組み込まれたプロバイダー。

### <a name="span-idthe_logman_query_providers_displayspanspan-idthe_logman_query_providers_displayspanthe-logman-query-providers-display"></a><span id="the_logman_query_providers_display"></span><span id="THE_LOGMAN_QUERY_PROVIDERS_DISPLAY"></span>Logman クエリプロバイダーが表示されます。

Tracelog enumguid の表示は、Logman (**logman クエリプロバイダー**) に表示されるクエリプロバイダーとは大きく異なりますが、表示は混同されることがよくあります。

Logman (logman) は、トレースイベントとパフォーマンスカウンターのトレースコントローラーです。 Windows XP 以降のバージョンの Windows に含まれています。

Logman プロバイダークエリ (**logman クエリプロバイダー**) には、管理オブジェクトフォーマット (MOF) ファイルが WMI に登録されているプロバイダーの一覧が表示されます。 Logman 表示には、WMI にも登録されていない限り、ソフトウェアのトレース用にインストルメント化されたプロバイダーは含まれません。

ユーザーがプロバイダーを検索できるようにする開発者は、プロバイダーが Logman 画面に表示されるように MOF ファイルを登録することが必要になる場合があります。 残念ながら、Logman クエリプロバイダーの表示も Tracelog enumguid の表示も、システム上のすべてのトレースプロバイダーの完全な一覧ではありません。 Logman の詳細については、ヘルプとサポートセンターの「Logman」を参照してください。

### <a name="span-idelements_of_the_enumguid_displayspanspan-idelements_of_the_enumguid_displayspanelements-of-the-enumguid-display"></a><span id="elements_of_the_enumguid_display"></span><span id="ELEMENTS_OF_THE_ENUMGUID_DISPLAY"></span>Enumguid 表示の要素

Tracelog enumguid 表示の表には、次の列が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列見出し</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Guid</strong></p></td>
<td align="left"><p>トレースプロバイダーの<a href="control-guid.md" data-raw-source="[control GUID](control-guid.md)">コントロール GUID</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Enabled</strong></p></td>
<td align="left"><p>プロバイダーが現在有効になっている (<strong>TRUE</strong>) か、登録されているが有効になっていない (<strong>FALSE</strong>) かを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LoggerId</strong></p></td>
<td align="left"><p>トレースセッションを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Level</strong></p></td>
<td align="left"><p>プロバイダーに対して現在設定されているレベル。 プロバイダーが有効になっている場合にのみ有効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>フラグ</strong></p></td>
<td align="left"><p>プロバイダーに対して現在設定されているフラグ。 プロバイダーが有効になっている場合にのみ有効です。</p></td>
</tr>
</tbody>
</table>

 
プロバイダーが登録されていても有効になっていない場合は、enumguid 画面に表示されますが、[**有効**] 列のエントリは [ **FALSE**] になります。

プロバイダーが有効になっていても、まだ実行されていないため、登録されていない場合は、enumguid 表示に表示されません。

### <a name="span-idsample_enumguid_displayspanspan-idsample_enumguid_displayspansample-enumguid-display"></a><span id="sample_enumguid_display"></span><span id="SAMPLE_ENUMGUID_DISPLAY"></span>Enumguid 表示のサンプル

次の enumguid 表示は、Windows Server 2003 を実行しているコンピューターからコピーされました。 表示には、登録されて実行されているプロバイダーが一覧表示されます。 追跡のために、Tracedrv サンプルドライバーの1つのプロバイダーが有効になっています。 ソフトウェアトレース用に設計された[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)は、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

```
c:\Tracelog>tracelog -enumguid
##     Guid                     Enabled  LoggerId Level Flags
------------------------------------------------------------
1046d4b1-fce5-48bc-8def-fd33196af19a     FALSE  0    0    0
196e57d9-49c0-4b3b-ac3a-a8a93ada1938     FALSE  0    0    0
4a8aaa94-cfc4-46a7-8e4e-17bc45608f0a     FALSE  0    0    0
1540ff4c-3fd7-4bba-9938-1d1bf31573a7     FALSE  0    0    0
1fbecc45-c060-4e7c-8a0e-0dbd6116181b     FALSE  0    0    0
f12b1984-4c42-11d3-ab7b-00c04f68fcdc     FALSE  0    0    0
94a984ef-f525-4bf1-be3c-ef374056a592     FALSE  0    0    0
3121cf5d-c5e6-4f37-be86-57083590c333     FALSE  0    0    0
f498b9f5-9e67-446a-b9b8-1442ffaef434     FALSE  0    0    0
e1f65b93-f32a-4ed6-aa72-b039e28f1574     FALSE  0    0    0
dd5ef90a-6398-47a4-ad34-4dcecdef795f     FALSE  0    0    0
e80aa9fe-913d-4ede-af58-73e332dcac8d     FALSE  0    0    0
1b1d4ff4-f27b-4c99-8bd7-da8f1a74051a     FALSE  0    0    0
f33959b4-dbec-11d2-895b-00c04f79ab69     FALSE  0    0    0
cc85922f-db41-11d2-9244-006008269001     FALSE  0    0    0
c92cf544-91b3-4dc0-8e11-c580339a0bf8     FALSE  0    0    0
bba3add2-c229-4cdb-ae2b-57eb6966b0c4     FALSE  0    0    0
8fc7e81a-f733-42e0-9708-cfdae07ed969     FALSE  0    0    0
cddc01e2-fdce-479a-b8ee-3c87053fb55e     FALSE  0    0    0
fc4b0d39-e8be-4a83-a32f-c0c7c4f61ee4     FALSE  0    0    0
fc570986-5967-4641-a6f9-05291bce66c5     FALSE  0    0    0
39a7b5e0-be85-47fc-b9f5-593a659abac1     FALSE  0    0    0
dab01d4d-2d48-477d-b1c3-daad0ce6f06b     FALSE  0    0    0
bca7bd7f-b0bf-4051-99f4-03cfe79664c1     FALSE  0    0    0
d58c126f-b309-11d1-969e-0000f875a5bc      TRUE  2    0    0
d58c126e-b309-11d1-969e-0000f875a5bc     FALSE  0    0    0
58db8e03-0537-45cb-b29b-597f6cbebbfe     FALSE  0    0    0
58db8e03-0537-45cb-b29b-597f6cbebbfd     FALSE  0    0    0
688a5248-f348-4576-86cf-3521c7094614     FALSE  0    0    0
27246e9d-b4df-4f20-b969-736fa49ff6ff    FALSE  0    0    0
```
