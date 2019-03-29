---
title: Tracelog Enumguid の表示
description: Tracelog Enumguid の表示
ms.assetid: 9bb93238-98f7-4422-8434-b4dc105ec008
keywords:
- Tracelog WDK、プロバイダー
- プロバイダーの WDK ソフトウェア トレース
- WDK、プロバイダーのトレース
- -enumguid コマンド
- enumguid コマンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e94a41767a6fe440f0db0f45e1f47108d2f4d112
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581568"
---
# <a name="tracelog-enumguid-display"></a>Tracelog Enumguid の表示

送信するとき、 **tracelog enumguid**コマンド、トレース ログを実行していているトレース プロバイダーの一覧が表示されます。[登録](registered-provider.md)を Event Tracing for Windows (ETW)。 表示が非常に便利ですが、多くの場合、誤って解釈されます。

### <a name="span-idwhichprovidersappearinthedisplayspanspan-idwhichprovidersappearinthedisplayspanwhich-providers-appear-in-the-display"></a><span id="which_providers_appear_in_the_display_"></span><span id="WHICH_PROVIDERS_APPEAR_IN_THE_DISPLAY_"></span>プロバイダーは、表示で表示されますか。

Tracelog enumguid 表示は、トレース セッションを有効にできるプロバイダーの一部を示しますが、完全な一覧ではありません。 実行しているし、ETW に登録されているトレース プロバイダーのみが含まれています。

表示では、次のプロバイダーは含まれません。

実行されていないため、通常は、システムで使用できますが、登録されていないプロバイダーをトレースします。

トレース プロバイダーのトレース セッションを有効になっているが、現在実行中ではないです。 (これらは多くの場合と呼ばれる*あらかじめ有効になっている*または*に事前登録された*プロバイダー)。これには、実行されている継続的に、Dll が読み込まれ、必要に応じて、アンロードなどのプロバイダーが含まれます。

システム セッションとのプロバイダーのプロバイダーを含む、Windows に組み込まれているプロバイダー、[グローバル ロガー トレース セッション](global-logger-trace-session.md)と[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

### <a name="span-idthelogmanqueryprovidersdisplayspanspan-idthelogmanqueryprovidersdisplayspanthe-logman-query-providers-display"></a><span id="the_logman_query_providers_display"></span><span id="THE_LOGMAN_QUERY_PROVIDERS_DISPLAY"></span>Logman クエリ プロバイダーを表示します。

Tracelog enumguid 表示は、Logman のクエリ プロバイダーの表示とは大きく異なります (**logman クエリ プロバイダー**)、多くの場合は、表示、混乱します。

Logman (logman.exe) は、トレース イベントとパフォーマンス カウンターのトレース コント ローラーです。 Windows XP および Windows の以降のバージョンに含まれています。

Logman プロバイダーのクエリ (**logman クエリ プロバイダー**) wmi 管理オブジェクト フォーマット (MOF) ファイルを登録したプロバイダーの一覧を表示します。 Logman 表示では WMI にも登録した場合を除き、ソフトウェア トレースのインストルメント化されているプロバイダーは含まれません。

開発者がときどきそのプロバイダーを見つけられるようにする場合は、プロバイダー、Logman 表示するために、MOF ファイルを登録します。 残念ながら、Logman クエリ プロバイダーの表示も Tracelog enumguid 表示は、システム上のすべてのトレース プロバイダーの完全なリストです。 Logman の詳細については、ヘルプとサポート センターで"Logman"を参照してください。

### <a name="span-idelementsoftheenumguiddisplayspanspan-idelementsoftheenumguiddisplayspanelements-of-the-enumguid-display"></a><span id="elements_of_the_enumguid_display"></span><span id="ELEMENTS_OF_THE_ENUMGUID_DISPLAY"></span>Enumguid 表示の要素

Tracelog enumguid 表示内のテーブルには、次の列が含まれています。

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
<td align="left"><p><strong>guid</strong></p></td>
<td align="left"><p><a href="control-guid.md" data-raw-source="[control GUID](control-guid.md)">コントロール GUID</a>トレース プロバイダーの</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Enabled</strong></p></td>
<td align="left"><p>プロバイダーが現在有効になっているかどうかを示しています (<strong>TRUE</strong>) またはの登録が有効になっていません (<strong>FALSE</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LoggerId</strong></p></td>
<td align="left"><p>トレース セッションを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>レベル</strong></p></td>
<td align="left"><p>現在、プロバイダー設定されているレベル。 プロバイダーが有効になっている場合にのみ有効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>フラグ</strong></p></td>
<td align="left"><p>プロバイダーの現在、フラグを設定します。 プロバイダーが有効になっている場合にのみ有効です。</p></td>
</tr>
</tbody>
</table>

 
Enumguid 表示が、対応するエントリに表示されるかどうかは、プロバイダーの登録が有効になっていない、**有効**列が**FALSE**します。

プロバイダーがある場合は有効になっているが、現在実行されていないが、そのため、登録されていない には表示されません enumguid 表示にします。

### <a name="span-idsampleenumguiddisplayspanspan-idsampleenumguiddisplayspansample-enumguid-display"></a><span id="sample_enumguid_display"></span><span id="SAMPLE_ENUMGUID_DISPLAY"></span>サンプル Enumguid の表示

次の enumguid 表示は、Windows Server 2003 を実行しているコンピューターからコピーされました。 登録され、実行中のプロバイダーの一覧が表示されます。 トレースでは、1 つのプロバイダー、Tracedrv サンプル ドライバーは有効です。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)、ソフトウェア トレースのように設計されたドライバーのサンプルが記載されて、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

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
