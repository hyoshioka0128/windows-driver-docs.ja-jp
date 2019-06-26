---
title: HDAUDIO_BUS_INTERFACE DDI オブジェクトの取得
description: HDAUDIO_BUS_INTERFACE DDI オブジェクトの取得
ms.assetid: 78667254-62a6-41fe-af36-43dbdea63aa8
keywords:
- HDAUDIO_BUS_INTERFACE 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564ce09947de9b937ef48c5827b18d0542001fe3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363198"
---
# <a name="obtaining-an-hdaudiobusinterface-ddi-object"></a>取得、HDAUDIO\_BUS\_インターフェイス DDI オブジェクト


次の表は入力パラメーターの値に、関数のドライバーを書き込みます、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IOCTL、を取得するには[**HDAUDIO\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造と、この構造体を定義する HD オーディオ DDI のバージョンのコンテキスト オブジェクト。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONST GUID *<em>InterfaceType</em></p></td>
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>サイズ</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p>ポインター <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"> <strong>HDAUDIO_BUS_INTERFACE</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

Function ドライバーの記憶域の割り当て、 [ **HDAUDIO\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造し、IOCTL でこの構造体へのポインターが含まれています。 前の表へのポインター、 **HDAUDIO\_BUS\_インターフェイス**構造が型にキャスト**PINTERFACE**、型の構造体へのポインターである[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)します。 名前と型の最初の 5 つのメンバーの**HDAUDIO\_BUS\_インターフェイス**の 5 つのメンバーに合わせて**インターフェイス**します。 **HDAUDIO\_BUS\_インターフェイス**DDI ルーチンへの関数ポインターであるその他のメンバーが含まれています。 関数ドライバーからの IOCTL の受信に応答してでは、HD オーディオ バス ドライバー、全体で塗りつぶします**HDAUDIO\_BUS\_インターフェイス**構造体。

次の表は、値の最初の 5 つのメンバーに、HD オーディオ バス ドライバーを記述、 [ **HDAUDIO\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>USHORT<strong>サイズ</strong></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>バージョン</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>コンテキスト</strong></p></td>
<td align="left"><p>コンテキストについては、最初の呼び出しのパラメーターとして各 DDI ルーチンに渡す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>コンテキスト オブジェクトの参照カウントをインクリメントするルーチンへのポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>ルーチンへのポインターをコンテキスト オブジェクトの参照カウントをデクリメント</p></td>
</tr>
</tbody>
</table>

 

上記の表に、**コンテキスト**ベースライン HD オーディオ DDI IOCTL からクライアントを取得するは、特定のインスタンスに固有の情報が含まれるコンテキスト オブジェクトへのポインターします。 クライアント機能のドライバーが常に指定する必要があります DDI でこれらのルーチンを呼び出す場合、**コンテキスト**最初の呼び出しのパラメーターとしてのポインターの値。 コンテキスト情報は、クライアントに対して非透過的です。 HD オーディオ バス ドライバーでは、各クライアントのさまざまなコンテキスト オブジェクトを作成します。 クライアントが呼び出すことによって、コンテキスト オブジェクトを解放するコンテキスト オブジェクトが必要でなくなったときに、 **InterfaceDereference**ルーチンは、前の表に示すようにします。 クライアントが呼び出すことによってオブジェクトへの他の参照を作成できます、必要な場合、 **InterfaceReference**ルーチンが、クライアントが不要になった要求して、これらの参照を解放します。

 

 




