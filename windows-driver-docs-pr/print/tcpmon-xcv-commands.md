---
title: TCPMON Xcv コマンド
description: TCPMON Xcv コマンド
ms.assetid: 89aebc89-d81e-4d86-942e-d13b16c55fb3
keywords:
- 印刷モニター WDK、TCPMON Xcv
- transceive (Xcv) コマンド WDK 印刷
- Xcv コマンドの WDK 印刷
- TCPMON Xcv コマンドの WDK 印刷
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
ms.openlocfilehash: 4a965b72820bc68fe94081d6c57b713de4fc56e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838786"
---
# <a name="tcpmon-xcv-commands"></a>TCPMON Xcv コマンド





このセクションでは、標準の TCP/IP ポートモニター (TCPMON) と通信するときに、 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))または[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)関数の呼び出しで指定できるコマンドについて説明します。 各コマンドは、これらの関数の呼び出しで、 *Pszdataname*文字列によって指定されます。 一部のコマンドでは、入力バッファーまたは出力バッファーのいずれかまたは両方が必要です。 これらの関数の*Pinputdata*パラメーターと*poutputdata*パラメーターは、これらのバッファーのアドレスを保持します。

次の各コマンドの説明に表示される表は、コマンドで使用される**XcvData**パラメーターと**XcvDataPort**パラメーターを示しています。 *Hxcv*パラメーター (両方の関数に共通) は表示されないことに注意してください。また、 **XcvData**関数の*pdwStatus*パラメーターも含まれていません。

### <a name="addport-command"></a>AddPort コマンド

**Addport**コマンドは、標準の tcp/ip ポートを追加します。これは、LPR ポートまたは RAW tcp/ip ポートのいずれかになります。

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
<td><p>L "AddPort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1)"><strong>PORT_DATA_1</strong></a>構造体のアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p>DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

ポートを追加できる場合、 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))は\_エラーを返しません。 通常のエラーコードに加えて、 **XcvData**は、サーバー上にポートを作成するための十分な特権がユーザーにない場合、エラー\_アクセス\_拒否を返します。 このコマンドでは、サーバー\_アクセス\_管理特権が必要です。 *Pinputdata*パラメーターが**NULL**の場合、関数は無効な\_データ\_エラーを返します。 *Pinputdata*--&gt;*dwversion*が1と等しくない場合、関数は無効な\_レベル\_エラーを返します。

### <a name="configport-command"></a>ConfigPort コマンド

**Configport**コマンドは、既存の標準 tcp/ip ポートモニターのポートを構成します。

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
<td><p>L "ConfigPort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1)"><strong>PORT_DATA_1</strong></a>構造体のアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p>DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

ポートを構成できる場合、 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))は\_エラーを返しません。 通常のエラーコードに加えて、 **XcvData**は、呼び出し元に要求を実行するための十分な特権がない場合に、アクセス\_拒否\_エラーを返します。 このコマンドでは、サーバー\_アクセス\_管理特権が必要です。 *Pinputdata*パラメーターが**NULL**の場合、または*cbinputdata*の値が required よりも小さい場合、関数は無効な\_データ\_エラーを返します。 *Pinputdata*--&gt;*dwversion*が1と等しくない場合、関数は無効な\_レベル\_エラーを返します。

### <a name="deleteport-command"></a>DeletePort コマンド

**Deleteport**コマンドは、標準の tcp/ip ポートモニタからポートを削除します。

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
<td><p>L "DeletePort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_delete_port_data_1" data-raw-source="[&lt;strong&gt;DELETE_PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_delete_port_data_1)"><strong>DELETE_PORT_DATA_1</strong></a>構造体のアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(DELETE_PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p>DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

ポートが正常に削除された場合、 **XcvData**は NO\_エラーを返します。 通常のエラーコードに加えて、 **XcvData**は、呼び出し元がサーバーに対して十分な権限を持っていない場合に、アクセス\_拒否\_エラーを返します。 このコマンドでは、サーバー\_アクセス\_管理特権が必要です。 *Pinputdata*パラメーターが**NULL**の場合、または*cbinputdata*パラメーターが required より小さい場合、関数は無効な\_データ\_エラーを返します。 *Pinputdata*--&gt;*dwversion*が1と等しくない場合、関数は無効な\_レベル\_エラーを返します。

### <a name="getconfiginfo-command"></a>GetConfigInfo コマンド

**Getconfiginfo**コマンドは、特定のポートの構成情報を取得します。 この場合、Xcv データハンドルは、ポートを識別できるように、特定の標準 TCP/IP ポートモニターポートをポイントする必要があります。

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
<td><p>L "GetConfigInfo"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_config_info_data_1" data-raw-source="[&lt;strong&gt;CONFIG_INFO_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_config_info_data_1)"><strong>CONFIG_INFO_DATA_1</strong></a>構造体のアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(CONFIG_INFO_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1)"><strong>PORT_DATA_1</strong></a>構造体のアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p><em>Poutputdata</em>が指すバッファーに必要なバイト数を含む DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

ポートの構成情報を取得できる場合、 **XcvData**は\_エラーを返しません。 *Pinputdata*が**NULL**の場合、または*cbinputdata*が required よりも小さい場合、関数は無効な\_データ\_エラーを返します。 *Pinputdata*--&gt;*dwversion*が1と等しくない場合、関数は無効な\_レベル\_エラーを返します。 *Cboutputdata*が必須値より小さい場合、この関数は*pcboutputneeded*が**NULL**である場合にエラー\_無効な\_パラメーターを返し、 *pcboutputneeded が必要*なときに\_バッファーが不足していると、エラー\_**NULL**。

### <a name="hostaddress-command"></a>HostAddress コマンド

**Hostaddress**コマンドは、プリンターのホスト名を取得します。

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
<td><p>L "HostAddress"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>プリンターのホスト名を含む文字列を受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><em>Poutputdata</em>が指すバッファーのサイズ</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p><em>Poutputdata</em>が指すバッファーに必要なバイト数を含む DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

プリンターのホスト名を取得できる場合、 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))は\_エラーを返しません。 *Cboutputdata*が必須値より小さい場合、この関数は*pcboutputneeded*が**NULL**である場合にエラー\_無効な\_パラメーターを返し、 *pcboutputneeded が必要*なときに\_バッファーが不足していると、エラー\_**NULL**。 *Poutputdata*が**NULL**の場合、この関数はエラー\_無効な\_パラメーターを返します。

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
<td><p>L "IPAddress"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>プリンターの IP アドレスを含む文字列を受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><em>Poutputdata</em>が指すバッファーのサイズ</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p><em>Poutputdata</em>が指すバッファーに必要なバイト数を含む DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

プリンターの IP アドレスを取得できる場合、 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))は\_エラーを返しません。 *Cboutputdata*が必須値より小さい場合、この関数は*pcboutputneeded*が**NULL**である場合にエラー\_無効な\_パラメーターを返し、 *pcboutputneeded が必要*なときに\_バッファーが不足していると、エラー\_**NULL**。 *Poutputdata*が**NULL**の場合、この関数はエラー\_無効な\_パラメーターを返します。

### <a name="monitorui-command"></a>MonitorUI コマンド

**Monitorui**コマンドは、tcpmon へのインターフェイスを提供するポートモニター UI DLL の名前を取得します。

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
<td><p>L "MonitorUI"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>ポートモニターのユーザーインターフェイス DLL の名前を受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>ポートモニターのユーザーインターフェイス DLL の名前を含む文字列内のバイト数</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p><em>Poutputdata</em>が指すバッファーに必要なバイト数を含む DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))は、ユーザーインターフェイス DLL の名前を取得できる場合に\_エラーを返しません。 通常のエラーコードに加えて、 **XcvData**は、呼び出し元がサーバーに対して十分な権限を持っていない場合に、アクセス\_拒否\_エラーを返します。 このコマンドでは、サーバー\_アクセス\_管理特権が必要です。 *Cboutputdata*が必須値より小さい場合、この関数は*pcboutputneeded*が**NULL**である場合にエラー\_無効な\_パラメーターを返し、 *pcboutputneeded が必要*なときに\_バッファーが不足していると、エラー\_**NULL**。 *Poutputdata*が**NULL**の場合、この関数はエラー\_無効な\_パラメーターを返します。

### <a name="snmpcommunity"></a>SNMPCommunity

**SNMPCommunity**コマンドは、プリンターの簡易ネットワーク管理プロトコル (SNMP) コミュニティ名を取得します。

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
<td><p>L "SNMPCommunity"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>プリンターの SNMP コミュニティを含む文字列を受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><em>Poutputdata</em>パラメーターが指す文字列を格納するために必要なバッファーのサイズ</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p><em>Poutputdata</em>が指すバッファーに必要なバイト数を含む DWORD のアドレス</p></td>
</tr>
</tbody>
</table>

 

[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))は、プリンターの SNMP コミュニティ名を取得できる場合に\_エラーを返しません。 *Cboutputdata*が必須値より小さい場合、この関数は*pcboutputneeded*が**NULL**である場合にエラー\_無効な\_パラメーターを返し、 *pcboutputneeded が必要*なときに\_バッファーが不足していると、エラー\_**NULL**。 *Poutputdata*が**NULL**の場合、この関数はエラー\_無効な\_パラメーターを返します。

### <a name="snmpdeviceindex"></a>SNMPDeviceIndex

**SNMPDeviceIndex**コマンドは、プリンタの簡易ネットワーク管理プロトコル (SNMP) デバイスインデックスを取得します。

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
<td><p>L "SNMPDeviceIndex"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>デバイスインデックスを受け取るバッファーのアドレス</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p><strong>Sizeof</strong>(dword) を含む dword のアドレス</p></td>
</tr>
</tbody>
</table>

 

[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))は、プリンターの SNMP デバイスインデックスを取得できる場合に\_エラーを返しません。 *Cboutputdata*が必須値より小さい場合、この関数は*pcboutputneeded*が**NULL**である場合にエラー\_無効な\_パラメーターを返し、 *pcboutputneeded が必要*なときに\_バッファーが不足していると、エラー\_**NULL**。 *Poutputdata*が**NULL**の場合、この関数はエラー\_無効な\_パラメーターを返します。

### <a name="snmpenabled"></a>SNMPEnabled

**SNMPEnabled**コマンドは、現在のデバイスに対して簡易ネットワーク管理プロトコル (SNMP) が有効になっているかどうかを判断します。

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
<td><p>L "SNMPEnabled"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>空白</strong></p></td>
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
<td><p><em>pcbOutputNeeded 必要です</em></p></td>
<td><p><strong>Sizeof</strong>(dword) を含む dword のアドレス</p></td>
</tr>
</tbody>
</table>

 

SNMP がデバイスに対して有効になっている場合、 **XcvData**は NO\_エラーを返します。 *Cboutputdata*が必須値より小さい場合、この関数は*pcboutputneeded*が**NULL**である場合にエラー\_無効な\_パラメーターを返し、 *pcboutputneeded が必要*なときに\_バッファーが不足していると、エラー\_**NULL**。 *Poutputdata*が**NULL**の場合、この関数はエラー\_無効な\_パラメーターを返します。

 

 




