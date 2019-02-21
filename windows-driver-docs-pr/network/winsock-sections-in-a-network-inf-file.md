---
title: Winsock のセクションでは、ネットワークの INF ファイル
description: Winsock のセクションでは、ネットワークの INF ファイル
ms.assetid: 179a8570-287b-446e-8b56-a9f23071e84d
keywords:
- Winsock のセクションでは、ある INF ファイル WDK ネットワーク
- ネットワーク INF ファイル、WDK Winsock セクション
- Winsock のセクションでは WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 820316b0c64c15ebc100e5f5c67b323619cc2c0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536236"
---
# <a name="winsock-sections-in-a-network-inf-file"></a>Winsock のセクションでは、ネットワークの INF ファイル




用の INF ファイルを**NetTrans** Winsock インターフェイスを提供するコンポーネントは、この Winsock の依存関係を指定する必要があります。 このような INF ファイルを含める必要があります、 *Winsock インストール*セクション。 Winsockinstall セクションを作成するには追加します。Winsock の拡張機能、 *DDInstall*プロトコルのセクション名。 たとえば場合、 *DDInstall*セクションのプロトコルの名前は**Ipx**、 *Winsock インストール*セクションは、そのプロトコルが名前の Ipx.Winsock を指定する必要があります。

> [!NOTE] 
> Windows 8 以降、Winsock の依存関係は非推奨とされました。


A *Winsock インストール*セクションを含める必要があります、 **AddSock**ディレクティブ。 **AddSock**ディレクティブ指定ベンダーという名前のセクションに、コンポーネントの追加する値を含む**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\*TransportDriverName*\\Params\\Winsock**キー。

によって参照されているベンダーの名前付きセクション、 **AddSock**ディレクティブは、次の必要な値を含める必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">［値の名前］</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>TransportService</p></td>
<td align="left"><p>プロトコルのサービス名を指定する REG_SZ 値を返します。 これと同じである必要があります、 <strong>Ndi\Service</strong>プロトコルの値。 詳細については、次を参照してください。 <a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Adding Service-Related Values to the Ndi Key](adding-service-related-values-to-the-ndi-key.md)">Ndi キーに値を Adding Service-Related</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HelperDllName</p></td>
<td align="left"><p>Windows Sockets ヘルパー (WSH) プロトコルの DLL へのパスを指定する REG_EXPAND_SZ 値。 詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566260" data-raw-source="[WSH DLL Function Summary](https://msdn.microsoft.com/library/windows/hardware/ff566260)">WSH DLL 関数の概要</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxSockAddrLength</p></td>
<td align="left"><p>WSH DLL の最大の有効な SOCKADDR サイズをバイト単位で指定する REG_DWORD 値</p></td>
</tr>
<tr class="even">
<td align="left"><p>MinSockAddrLength</p></td>
<td align="left"><p>WSH DLL の (バイト単位) の最小有効の SOCKADDR サイズを指定する REG_DWORD 値</p></td>
</tr>
</tbody>
</table>

 

省略可能な場合**ProviderId**次の値が指定することも必要がありますの名前空間のプロバイダーを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">［値の名前］</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ProviderId</p></td>
<td align="left"><p>グローバル一意識別子 (GUID) 名前空間のプロバイダーを識別するを指定するための REG_SZ 値。 GUID は、名前空間のプロバイダーへの後続のすべての参照をキーとして使用されます。 Uuidgen.exe ユーティリティを実行して GUID を取得します。 このユーティリティの詳細については、Microsoft Windows SDK を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LibraryPath</p></td>
<td align="left"><p>REG_EXPAND_SZ の値で、名前空間プロバイダーの DLL への完全パスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DisplayString</p></td>
<td align="left"><p>ユーザー インターフェイスの名前空間のプロバイダーの表示名を指定する、ローカライズ可能な文字列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SupportedNameSpace</p></td>
<td align="left"><p>名前空間のプロバイダーでサポートされている名前空間を指定する REG_DWORD 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>名前空間のプロバイダーのバージョン番号を指定する省略可能な REG_DWORD 値。 この値が指定されていない場合は、既定値 (1) が、バージョン番号に使用されます。</p></td>
</tr>
</tbody>
</table>

 

次の名前空間の値は、SupportedNameSpace に割り当てることができます、Winsock2.h で定義されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名前空間</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NS_ALL</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_SAP</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_NDS</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_PEER_BROWSE</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_TCPIP_LOCAL</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_TCPIP_HOSTS</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_DNS</p></td>
<td align="left"><p>12</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_NETBT</p></td>
<td align="left"><p>13</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_WINS</p></td>
<td align="left"><p>14</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_NBP</p></td>
<td align="left"><p>20</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_MS</p></td>
<td align="left"><p>30</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_STDA</p></td>
<td align="left"><p>31</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_CAIRO</p></td>
<td align="left"><p>32</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_X500</p></td>
<td align="left"><p>40</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_NIS</p></td>
<td align="left"><p>41</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_WRQ</p></td>
<td align="left"><p>50</p></td>
</tr>
</tbody>
</table>

 

名前空間のプロバイダーの詳細については、Windows SDK のドキュメントを参照してください。

次の例では、Winsock のセクションでは IPX プロトコルを示します。

```INF
[Ipx.Winsock]
AddSock = Install.IpxWinsock
 
[Install.IpxWinsock]
TransportService = nwlinkipx
HelperDllName = "%%SystemRoot%%\System32\wshisn.dll"
MaxSockAddrLength = 0x10
MinSockAddrLength = 0xe
ProviderId = "GUID"
LibraryPath = "%SystemRoot%\\System32\\nwprovau.dll"
DisplayString = %NwlnkIpx_Desc%
SupportedNameSpace = 1
Version = 2
```

プロトコルの Winsock の依存関係を削除など、INF ファイル、 *Winsock 削除*セクション。 作成する、 *Winsock 削除*セクションを追加します。Winsock の拡張機能、*削除*プロトコルのセクション名。 たとえば場合、*削除*セクションのプロトコルは Ipx.Remove、名前は、 *Winsock 削除*セクション プロトコルにより、Ipx.Remove.Winsock 指定する必要があります。

*Winsock 削除*セクションが含まれています、 **DelSock** INF ライターという名前のセクションで示すディレクティブ。 INF ライターという名前のセクションでは、削除するトランスポート サービスを指定する必要があります。 場合、 **ProviderId**以前に登録されたプロトコル、ベンダーの名前付きセクションを指定する必要がありますも、 **ProviderId**を削除します。

IPX プロトコル Winsock 依存関係を削除する 2 つのセクションで、次の例です。

```INF
[Ipx.Remove.Winsock]
DelSock = Remove.IpxWinsock
 
[Remove.IpxWinsock]
TransportService = nwlinkipx
ProviderId = "GUID"
```

 

 





