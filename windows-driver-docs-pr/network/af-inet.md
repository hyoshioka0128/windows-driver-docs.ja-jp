---
title: AF_INET
description: AF_INET
ms.assetid: 59e12f8d-02eb-413c-bc04-6b9b6e4adde6
ms.date: 08/08/2017
keywords: -AF_INET ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5319fe56d72f314708725bc16952a78e11ada74d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529655"
---
# <a name="afinet"></a>AF\_INET


AF\_INET アドレス ファミリが ipv4 アドレス ファミリ。

### <a name="socket-address-structure"></a>ソケット アドレス構造

IPv4 のトランスポート アドレスを指定した、 [ **SOCKADDR\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff570823)構造体。

### <a name="socket-types"></a>ソケットの種類

IPv4 では、次の種類のソケットをサポートします。

<a href="" id="sock-stream"></a>SOCK\_ストリーム  
信頼性の高い接続指向のバイト ストリーム通信をサポートしています。

<a href="" id="sock-dgram"></a>SOCK\_DGRAM  
信頼性の低いコネクションレスのデータグラム通信をサポートしています。

<a href="" id="sock-raw"></a>SOCK\_RAW  
トランスポート プロトコルへの生のアクセスをサポートしています。

呼び出すときに、WSK アプリケーションはソケットの種類を指定します、 [ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)関数または[ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)関数を作成する、新しいソケット。

### <a name="protocols"></a>プロトコル

次の IPv4 IPPROTO\_*XXX* IPPROTO 列挙体の値をプロトコル WSK ヘッダー ファイルで定義されます。

<a href="" id="ipproto-ip"></a>IPPROTO\_IP  
インターネット プロトコル オプション

<a href="" id="ipproto-icmp"></a>IPPROTO\_ICMP  
インターネット制御メッセージ プロトコル

<a href="" id="ipproto-igmp"></a>IPPROTO\_IGMP  
インターネット グループ管理プロトコル

<a href="" id="ipproto-ggp"></a>IPPROTO\_GGP  
ゲートウェイ プロトコルへのゲートウェイ

<a href="" id="ipproto-ipv4"></a>IPPROTO\_IPV4  
IPv4 のカプセル化

<a href="" id="ipproto-st"></a>IPPROTO\_ST  
Stream プロトコル

<a href="" id="ipproto-tcp"></a>IPPROTO\_TCP  
伝送制御プロトコル

<a href="" id="ipproto-cbt"></a>IPPROTO\_CBT  
Core ベースのツリーのプロトコル

<a href="" id="ipproto-egp"></a>IPPROTO\_EGP  
外部ゲートウェイ プロトコル

<a href="" id="ipproto-igp"></a>IPPROTO\_IGP  
プライベートの内部ゲートウェイ プロトコル

<a href="" id="ipproto-pup"></a>IPPROTO\_PUP  
PARC universal packet プロトコル

<a href="" id="ipproto-udp"></a>IPPROTO\_UDP  
ユーザー データグラム プロトコル

<a href="" id="ipproto-idp"></a>IPPROTO\_IDP  
インターネット データグラム プロトコル

<a href="" id="ipproto-rdp"></a>IPPROTO\_RDP  
信頼性の高いデータ プロトコル

<a href="" id="ipproto-nd"></a>IPPROTO\_ND  
Net disk プロトコル

<a href="" id="ipproto-iclfxbm"></a>IPPROTO\_ICLFXBM  
広域デルファイの監視

<a href="" id="ipproto-pim"></a>IPPROTO\_PIM  
プロトコルの独立したマルチキャスト

<a href="" id="ipproto-pgm"></a>IPPROTO\_PGM  
実用的な一般的なマルチキャスト

<a href="" id="ipproto-l2tp"></a>IPPROTO\_L2TP  
レベル 2 トンネリング プロトコル

<a href="" id="ipproto-sctp"></a>IPPROTO\_SCTP  
Stream 制御伝送プロトコル

<a href="" id="ipproto-raw"></a>IPPROTO\_RAW  
Raw IP パケット

Raw ソケットを使用することは、その他のプロトコルがサポートされています。

WSK アプリケーションを呼び出すときに、プロトコルを指定します、 [ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)関数または[ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)関数を作成します。新しいソケット。

WSK アプリケーションでは、プロトコルも指定します (として、*レベル*パラメーター) 呼び出し時に、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)設定またはトランスポート プロトコルのレベルを取得する関数またはネットワーク プロトコル レベルのソケット オプション。

### <a name="combinations"></a>組み合わせ

IPv4 は、各 WSK の次のようなソケットの種類とプロトコルの組み合わせをサポートしている[ソケット カテゴリ](https://msdn.microsoft.com/library/windows/hardware/ff571093):

基本的なソケット SOCK\_ストリーム + IPPROTO\_TCP SOCK\_DGRAM + IPPROTO\_UDP SOCK\_RAW + IPPROTO\_*Xxx*リッスン ソケットの SOCK\_ストリーム + IPPROTO\_TCP

Datagram Sockets SOCK\_DGRAM + IPPROTO\_UDP SOCK\_RAW + IPPROTO\_*Xxx* Connection-Oriented Sockets SOCK\_STREAM + IPPROTO\_TCP

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




