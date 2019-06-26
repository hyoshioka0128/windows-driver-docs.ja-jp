---
title: プロキシ接続追跡の使用
description: プロキシ接続追跡の使用
ms.assetid: 20A737D7-043D-4D05-A15D-85595E48521B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44e8ffbd0db09d54b0de82578b20f84718c14291
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371774"
---
# <a name="using-proxied-connections-tracking"></a>プロキシ接続追跡の使用


追跡プロキシの接続は、Windows 8 および Windows の以降のバージョンでサポートされます。

この WFP 機能には、最終的な宛先に接続する接続のリダイレクトに基づく初期リダイレクト「レコード」の追跡が容易になります。 WFP は、コールアウト ドライバーの接続をリダイレクトすることもできます。

### <a name="proxied-connections-tracking"></a>追跡プロキシの接続

(たとえば、さまざまな Isv が開発した) 複数のプロキシの存在は最終送付先との通信に 1 つのパーティで使用する接続が 2 番目のパーティ; してリダイレクトする順番新しい接続が元のパーティによってリダイレクトされる可能性がもう一度です。 プロキシの無限ループでスタックしている、取得と、元の接続追跡接続を行わず、最終的な宛先は到達で可能性があることはありません。

接続の追跡をサポートするためにデータ フィールドの識別子に追加されたものは次のとおりです。

<a href="" id="fwps-field-xxx-ale-original-app-id"></a>FWPS\_フィールド\_Xxx\_ALE\_元\_アプリ\_ID  
プロキシ接続には、元のアプリケーションの完全パス。 このパスは xxx と同じ場合は、アプリケーションはプロキシ処理されていない、\_ALE\_アプリ\_id。

<a href="" id="fwps-field-xxx-package-id"></a>FWPS\_フィールド\_Xxx\_パッケージ\_ID  
パッケージ識別子は、関連付けられた AppContainer プロセスを識別するセキュリティ識別子 (SID) です。 SID 構造体の詳細については、Microsoft Windows sdk で SID 構造体の説明を参照してください。

### <a name="redirecting-connections"></a>接続をリダイレクトします。

コールアウト ドライバーは呼び出し、 [ **FwpsRedirectHandleCreate0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0) TCP 接続をリダイレクトするために使用できるハンドルを作成する関数。

ここでは、次のトピックについて説明します。

リダイレクトのハンドルを使用してください。

リダイレクト状態のクエリを実行します。

### <a name="using-a-redirection-handle"></a>リダイレクトのハンドルを使用してください。

リダイレクト コールアウトは、ローカルのプロセスに接続をリダイレクトできますエール接続前に、FwpsRedirectHandleCreate0 関数を使用したリダイレクト ハンドルを取得し、ハンドルを配置する必要があります、 [ **FWPS\_CONNECT\_REQUEST0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-_fwps_connect_request0)構造体。 引き出し線は、ALE connect レイヤーをリダイレクトするための classifyFn で構造を変更します。

FWPS\_CONNECT\_REQUEST0 構造体にはリダイレクトは、次のメンバーが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>localRedirectHandle</strong></p></td>
<td align="left"><p>コールアウト ドライバーを呼び出すことによって作成されるリダイレクト ハンドル、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0" data-raw-source="[&lt;strong&gt;FwpsRedirectHandleCreate0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)"> <strong>FwpsRedirectHandleCreate0</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>localRedirectContext</strong></p></td>
<td align="left"><p>コールアウト ドライバーを呼び出すことによって割り当てられているコールアウト ドライバーのコンテキスト領域、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)"> <strong>exallocatepoolwithtag に</strong></a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>localRedirectContextSize</strong></p></td>
<td align="left"><p>引き出し線のバイト単位のサイズは、コンテキストの領域を指定します。</p></td>
</tr>
</tbody>
</table>

 

コールアウト ドライバーが完了したら、リダイレクトのハンドルを使用して、呼び出す必要があります、 [ **FwpsRedirectHandleDestroy0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0)ハンドルを破棄する関数。

### <a name="querying-the-redirect-state"></a>リダイレクト状態のクエリを実行します。

コールアウト ドライバーは呼び出し、 [ **FwpsQueryConnectionRedirectState0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)接続のリダイレクトの状態を取得します。 [ **FWPS\_接続\_リダイレクト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_connection_redirect_state_)列挙型への呼び出しの戻り値の型は、 **FwpsQueryConnectionRedirectState0**関数。

リダイレクト状態が FWPS 場合\_接続\_いない\_REDIRECTED、ALE\_CONNECT\_リダイレクト吹き出しに進んでプロキシ接続します。

リダイレクト状態が FWPS 場合\_接続\_REDIRECTED\_BY\_SELF、ALE\_CONNECT\_リダイレクト コールアウトは、FWP を返す必要があります\_アクション\_許可/FWP\_アクション\_続行します。

リダイレクト状態が FWPS 場合\_接続\_REDIRECTED\_BY\_他 ALE\_CONNECT\_リダイレクト コールアウトでしたに進みますプロキシ接続が信頼していない場合、その他検査の結果。

リダイレクト状態が FWPS 場合\_接続\_以前\_REDIRECTED\_BY\_SELF、ALE\_CONNECT\_リダイレクト コールアウトはリダイレクトを実行する必要がありますいない場合でもその他のインスペクターの結果は入力できません。 必要がありますか、許可または接続をブロック、ここでは、(ALE で\_AUTH\_CONNECT レイヤー)。

 

 





