---
title: TCPMON Xcv コマンド
description: TCPMON Xcv コマンド
ms.assetid: 89aebc89-d81e-4d86-942e-d13b16c55fb3
keywords:
- 印刷モニター WDK、TCPMON Xcv
- WDK の利用 (Xcv) コマンドを印刷します。
- Xcv コマンド WDK を印刷します。
- TCPMON Xcv コマンド WDK を印刷します。
- AddPort
- ConfigPort
- DeletePort
- GetConfigInfo
- HostAddress
- IPAddress
- MonitorUI
- SNMPCommunity
- SNMPDeviceIndex
- SNMPEnabled
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b97c53f437d7fb95d849a71c203347c20a7e2a76
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385963"
---
# <a name="tcpmon-xcv-commands"></a>TCPMON Xcv コマンド





このセクションへの呼び出しで指定できるコマンドがについて説明します、 [ **XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))または[ **XcvDataPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvdataport)関数である場合に標準の TCP/IP ポート モニタ (TCPMON) と通信します。 各コマンドがで指定された、 *pszDataName*これらの関数の呼び出しでの文字列。 特定のコマンドは、入力バッファーまたは出力バッファー、またはその両方が必要です。 *PInputData*と*pOutputData*これらの関数のパラメーターは、これらのバッファーのアドレスを保持します。

コマンド リストを次のそれぞれの説明に表示されるテーブル、 **XcvData**と**XcvDataPort**コマンドで使用されるパラメーター。 なお、 *hXcv* (どちらの関数に共通) パラメーターは、表示されていないは、 **XcvData**関数の*pdwStatus*パラメーター。

### <a name="addport-command"></a>AddPort コマンド

**AddPort**コマンドは、LPR ポートか、生の TCP/IP ポートを標準の TCP/IP ポートを追加します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"AddPort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>アドレスを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_port_data_1)"> <strong>PORT_DATA_1</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) no が返されます\_エラーの場合は、ポートを追加できます。 通常のエラー コードのほか**XcvData**エラーが返されます\_アクセス\_かどうか、ユーザーには、サーバーのポートを作成するのに十分な特権を拒否します。 このコマンドは、サーバーを必要と\_アクセス\_管理特権。 場合、 *pInputData*パラメーターが**NULL**、関数には、エラーが返されます。\_無効な\_データ。 場合*pInputData*--&gt;*dwVersion*が 1 に等しく、関数は、エラーが返されます\_無効な\_レベル。

### <a name="configport-command"></a>ConfigPort コマンド

**ConfigPort**コマンドは、既存の標準的な TCP/IP ポート モニター ポートを構成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"ConfigPort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>アドレスを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_port_data_1)"> <strong>PORT_DATA_1</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) no が返されます\_エラーの場合は、ポートを構成できます。 通常のエラー コードのほか**XcvData**エラーが返されます\_アクセス\_呼び出し元が要求を実行するのに十分な特権を持つかどうかは拒否されました。 このコマンドは、サーバーを必要と\_アクセス\_管理特権。 場合、 *pInputData*パラメーターが**NULL**、値か、 *cbInputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_データ。 場合*pInputData*--&gt;*dwVersion*が 1 に等しく、関数は、エラーが返されます\_無効な\_レベル。

### <a name="deleteport-command"></a>DeletePort コマンド

**DeletePort**コマンドは、標準の TCP/IP ポート モニタからポートを削除します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"DeletePort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>アドレスを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_delete_port_data_1" data-raw-source="[&lt;strong&gt;DELETE_PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_delete_port_data_1)"> <strong>DELETE_PORT_DATA_1</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(DELETE_PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

**XcvData** no が返されます\_エラーの場合は、ポートが正常に削除します。 通常のエラー コードのほか**XcvData**エラーが返されます\_アクセス\_呼び出し元がサーバー上に十分な特権を持つかどうかが拒否されました。 このコマンドは、サーバーを必要と\_アクセス\_管理特権。 場合、 *pInputData*パラメーターが**NULL**、または、 *cbInputData*パラメーターが必要なよりも小さい、関数はエラーを返します\_無効\_データ。 場合*pInputData*--&gt;*dwVersion*が 1 に等しく、関数は、エラーが返されます\_無効な\_レベル。

### <a name="getconfiginfo-command"></a>GetConfigInfo コマンド

**GetConfigInfo**コマンドは、特定のポートの構成情報を取得します。 ここでは、Xcv データ ハンドルは、ポートを識別できるように特定の標準的な TCP/IP ポート モニター ポート をポイントする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"GetConfigInfo"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>アドレスを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_config_info_data_1" data-raw-source="[&lt;strong&gt;CONFIG_INFO_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_config_info_data_1)"> <strong>CONFIG_INFO_DATA_1</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(CONFIG_INFO_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>アドレスを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/tcpxcv/ns-tcpxcv-_port_data_1)"> <strong>PORT_DATA_1</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>バッファーに必要なバイト数を含む DWORD のアドレスが指す<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

**XcvData** no が返されます\_エラーの場合は、ポートの構成情報を取得できます。 場合*pInputData*は**NULL**、場合*cbInputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_データ。 場合*pInputData*--&gt;*dwVersion*が 1 に等しく、関数は、エラーが返されます\_無効な\_レベル。 場合*cbOutputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_パラメーターと*pcbOutputNeeded*は**NULL**とエラー\_不十分\_場合にバッファー *pcbOutputNeeded*以外**NULL**します。

### <a name="hostaddress-command"></a>HostAddress コマンド

**HostAddress**コマンドは、プリンターのホスト名を取得します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"HostAddress"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>プリンターのホスト名を含む文字列を受信するバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>バッファーのサイズが指す<em>pOutputData</em></p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>バッファーに必要なバイト数を含む DWORD のアドレスが指す<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) no が返されます\_エラーの場合は、プリンターのホストの名前を取得することができます。 場合*cbOutputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_パラメーターと*pcbOutputNeeded*は**NULL**とエラー\_不十分\_場合にバッファー *pcbOutputNeeded*以外**NULL**します。 場合*pOutputData*は**NULL**、関数には、エラーが返されます。\_無効な\_パラメーター。

### <a name="ipaddress-command"></a>IPAddress コマンド

**IPAddress**コマンドは、プリンターの IP アドレスを取得します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"IPAddress"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>プリンターの IP アドレスを含む文字列を受信するバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>バッファーのサイズが指す<em>pOutputData</em></p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>バッファーに必要なバイト数を含む DWORD のアドレスが指す<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) no が返されます\_エラーの場合は、プリンターの IP アドレスを取得することができます。 場合*cbOutputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_パラメーターと*pcbOutputNeeded*は**NULL**とエラー\_不十分\_場合にバッファー *pcbOutputNeeded*以外**NULL**します。 場合*pOutputData*は**NULL**、関数には、エラーが返されます。\_無効な\_パラメーター。

### <a name="monitorui-command"></a>MonitorUI コマンド

**MonitorUI**コマンド ポート モニター TCPMON にインターフェイスを提供する UI の DLL の名前を取得します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"MonitorUI"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>ポートのモニターのユーザー インターフェイスの DLL の名前を受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>ポートのモニターのユーザー インターフェイスの DLL の名前を含む文字列のバイト数</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>バッファーに必要なバイト数を含む DWORD のアドレスが指す<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) no が返されます\_エラーに、ユーザーの名前を取得することである場合は、DLL をインターフェイスします。 通常のエラー コードのほか**XcvData**エラーが返されます\_アクセス\_呼び出し元がサーバー上に十分な特権を持つかどうかが拒否されました。 このコマンドは、サーバーを必要と\_アクセス\_管理特権。 場合*cbOutputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_パラメーターと*pcbOutputNeeded*は**NULL**とエラー\_不十分\_場合にバッファー *pcbOutputNeeded*以外**NULL**します。 場合*pOutputData*は**NULL**、関数には、エラーが返されます。\_無効な\_パラメーター。

### <a name="snmpcommunity"></a>SNMPCommunity

**SNMPCommunity**コマンドは、プリンターの簡易ネットワーク管理プロトコル (SNMP) のコミュニティ名を取得します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"SNMPCommunity"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>プリンターの SNMP コミュニティを含む文字列を受信するバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>によって示される文字列を格納するために必要なバッファーのサイズ、 <em>pOutputData</em>パラメーター</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>バッファーに必要なバイト数を含む DWORD のアドレスが指す<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) no が返されます\_エラーの場合は、プリンターの SNMP コミュニティ名を取得できます。 場合*cbOutputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_パラメーターと*pcbOutputNeeded*は**NULL**とエラー\_不十分\_場合にバッファー *pcbOutputNeeded*以外**NULL**します。 場合*pOutputData*は**NULL**、関数には、エラーが返されます。\_無効な\_パラメーター。

### <a name="snmpdeviceindex"></a>SNMPDeviceIndex

**SNMPDeviceIndex**コマンドは、プリンターの簡易ネットワーク管理プロトコル (SNMP) デバイスのインデックスを取得します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"SNMPDeviceIndex"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>デバイスのインデックスを受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>アドレスを含む DWORD の<strong>sizeof</strong>(DWORD)</p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) no が返されます\_エラーの場合は、プリンターの SNMP デバイスのインデックスを取得できます。 場合*cbOutputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_パラメーターと*pcbOutputNeeded*は**NULL**とエラー\_不十分\_場合にバッファー *pcbOutputNeeded*以外**NULL**します。 場合*pOutputData*は**NULL**、関数には、エラーが返されます。\_無効な\_パラメーター。

### <a name="snmpenabled"></a>SNMPEnabled

**SNMPEnabled**コマンドは、現在のデバイスの簡易ネットワーク管理プロトコル (SNMP) が有効になっているかどうかを判断します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L"SNMPEnabled"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>DWORD 値を受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>アドレスを含む DWORD の<strong>sizeof</strong>(DWORD)</p></td>
</tr>
</tbody>
</table>

 

**XcvData** no が返されます\_エラー、デバイスの SNMP が有効になっている場合。 場合*cbOutputData*が小さい関数はエラーを返しますよりも、必要に応じて、\_無効な\_パラメーターと*pcbOutputNeeded*は**NULL**とエラー\_不十分\_場合にバッファー *pcbOutputNeeded*以外**NULL**します。 場合*pOutputData*は**NULL**、関数には、エラーが返されます。\_無効な\_パラメーター。

 

 




