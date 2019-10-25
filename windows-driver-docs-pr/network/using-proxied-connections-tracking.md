---
title: プロキシ接続追跡の使用
description: プロキシ接続追跡の使用
ms.assetid: 20A737D7-043D-4D05-A15D-85595E48521B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92ef88b7c31d0aca84041f5eab8191ebbcfcbce9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842975"
---
# <a name="using-proxied-connections-tracking"></a>プロキシ接続追跡の使用


プロキシ接続の追跡は、Windows 8 以降のバージョンの Windows でサポートされています。

この WFP 機能により、接続の最初のリダイレクトから宛先へのリダイレクト "レコード" の追跡が容易になります。 また、WFP は、コールアウトドライバーが接続をリダイレクトできるようにします。

### <a name="proxied-connections-tracking"></a>プロキシ接続の追跡

複数のプロキシが存在する (たとえば、さまざまな Isv によって開発された) 場合、一方のパーティが最終的な送信先と通信するために使用する接続は、2番目のパーティによってリダイレクトされます。また、元のパーティによって新しい接続が再びリダイレクトされる可能性があります。 接続の追跡がないと、元の接続は無限プロキシループでスタックして最終的な宛先に達しない可能性があります。

接続追跡をサポートするためのデータフィールド識別子への追加には、次のものがあります。

<a href="" id="fwps-field-xxx-ale-original-app-id"></a>FWPS\_フィールド\_Xxx\_ALE\_元の\_アプリ\_ID  
プロキシ接続用の元のアプリケーションの完全なパス。 アプリケーションがプロキシ化されていない場合、このパスは、xxx\_ALE\_アプリの\_ID と同じになります。

<a href="" id="fwps-field-xxx-package-id"></a>FWPS\_フィールド\_Xxx\_パッケージ\_ID  
パッケージ識別子は、関連付けられている AppContainer プロセスを識別するセキュリティ識別子 (SID) です。 SID 構造の詳細については、Microsoft Windows SDK のドキュメントで SID 構造の説明を参照してください。

### <a name="redirecting-connections"></a>リダイレクト (接続を)

コールアウトドライバーは、 [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)関数を呼び出して、TCP 接続をリダイレクトするために使用できるハンドルを作成します。

ここでは、次のトピックについて説明します。

リダイレクトハンドルの使用

リダイレクト状態のクエリ

### <a name="using-a-redirection-handle"></a>リダイレクトハンドルの使用

ALE 接続リダイレクトの吹き出しでローカルプロセスに接続をリダイレクトする前に、FwpsRedirectHandleCreate0 関数を使用してリダイレクトハンドルを取得し、そのハンドルを[**Fwps\_connect\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)構造体に配置する必要があります。 このコールアウトによって、ALE 接続リダイレクトレイヤーの Classid の構造が変更されます。

FWPS\_CONNECT\_REQUEST0 構造体には、リダイレクト用に次のメンバーが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>localRedirectHandle</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0" data-raw-source="[&lt;strong&gt;FwpsRedirectHandleCreate0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)"><strong>FwpsRedirectHandleCreate0</strong></a>関数を呼び出すことによってコールアウトドライバーによって作成されたリダイレクトハンドル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>localRedirectContext</strong></p></td>
<td align="left"><p>このコールアウトドライバーが、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>Exallocatepoolwithtag</strong></a>関数を呼び出すことによって割り当てた、コールアウトドライバーのコンテキスト領域。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>localRedirectContextSize</strong></p></td>
<td align="left"><p>コールアウトによって指定されたコンテキスト領域のサイズ (バイト単位)。</p></td>
</tr>
</tbody>
</table>

 

コールアウトドライバーがリダイレクトハンドルの使用を終了したら、 [**FwpsRedirectHandleDestroy0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0)関数を呼び出してハンドルを破棄する必要があります。

### <a name="querying-the-redirect-state"></a>リダイレクト状態のクエリ

コールアウトドライバーは、接続のリダイレクト状態を取得するために[**FwpsQueryConnectionRedirectState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)関数を呼び出します。 [**Fwps\_CONNECTION\_REDIRECT\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_connection_redirect_state_)列挙体は、 **FwpsQueryConnectionRedirectState0**関数への呼び出しの戻り値の型です。

リダイレクトの状態が FWPS の場合\_接続\_\_リダイレクトされていない場合は、ALE\_CONNECT\_REDIRECT コールアウトは、接続のプロキシに進むことができます。

リダイレクトの状態が FWPS\_接続\_\_リダイレクトされている場合は、"\_" によってリダイレクトされます。そのためには、ALE\_接続\_リダイレクト 吹き出しで、"許可/\_アクション\_続行\_アクション\_を返す必要があります。

リダイレクトの状態が FWPS の場合、接続\_リダイレクトされた\_他の\_によってリダイレクトされた場合、\_他のインスペクターの結果を信頼していない場合、ALE\_CONNECT\_REDIRECT コールアウトが接続のプロキシに進む可能性があります。

リダイレクトの状態が FWPS\_接続\_以前に自己\_\_\_リダイレクトされている場合、他のインスペクターの結果が許容できない場合でも、ALE\_CONNECT\_REDIRECT コールアウトはリダイレクトを実行しないようにする必要があります。 この場合、接続を許可またはブロックする必要があります (ALE\_AUTH\_CONNECT レイヤー)。

 

 





