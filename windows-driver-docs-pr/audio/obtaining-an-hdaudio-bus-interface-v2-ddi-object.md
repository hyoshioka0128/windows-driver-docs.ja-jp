---
title: HDAUDIO_BUS_INTERFACE_V2 DDI オブジェクトの取得
description: HDAUDIO_BUS_INTERFACE_V2 DDI オブジェクトの取得
ms.assetid: 3aad8c7a-8c89-499a-bfe8-e3facdffcd15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ca6d6d20b01f243fe7b2bf084de0dca98a5edd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363188"
---
# <a name="obtaining-an-hdaudiobusinterfacev2-ddi-object"></a>取得、HDAUDIO\_BUS\_インターフェイス\_V2 DDI オブジェクト


次の表は入力パラメーターの値に、関数のドライバーを書き込みます、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IOCTL、を取得するには[**HDAUDIO\_BUS\_インターフェイス\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造と、この構造体を定義する HD オーディオ DDI のバージョンのコンテキスト オブジェクト。

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
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_V2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>サイズ</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p>ポインター <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"> <strong>HDAUDIO_BUS_INTERFACE_V2</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

Function ドライバーの記憶域の割り当て、 [ **HDAUDIO\_BUS\_インターフェイス\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造し、IOCTL でこの構造体へのポインターが含まれています。 前の表へのポインター、 **HDAUDIO\_BUS\_インターフェイス\_V2**構造が型にキャスト**PINTERFACE**型の構造体へのポインターであります。[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)します。 名前と型の最初の 5 つのメンバーの**HDAUDIO\_BUS\_インターフェイス\_V2**の 5 つのメンバーに合わせて**インターフェイス**します。 **HDAUDIO\_BUS\_インターフェイス\_V2** DDI ルーチンへの関数ポインターであるその他のメンバーが含まれています。 HD オーディオ バス ドライバーの設定関数ドライバーからの IOCTL の受信に対する応答として、 **HDAUDIO\_BUS\_インターフェイス\_V2**構造体。

次の表は、値の最初の 5 つのメンバーに、HD オーディオ バス ドライバーを記述、 [ **HDAUDIO\_BUS\_インターフェイス\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造体。

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
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>バージョン</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>コンテキスト</strong></p></td>
<td align="left"><p>すべて DDI ルーチンへの呼び出しの最初のパラメーターとして渡す必要があるコンテキスト情報。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>コンテキスト オブジェクトの参照カウントをインクリメントするルーチンへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>ルーチンへのポインターをコンテキスト オブジェクトの参照カウントをデクリメントします。</p></td>
</tr>
</tbody>
</table>

 

前の表に、**コンテキスト**HD オーディオ DDI 基準計画の特定のインスタンスに固有の情報が含まれるコンテキスト オブジェクトへのポインターします。 クライアントは、IOCTL から HD オーディオ DDI この基準を取得します。 常に指定する必要があります、クライアント機能のドライバーでは、DDI でルーチンのいずれかを呼び出し、ときに、**コンテキスト**最初の呼び出しのパラメーターとしてメンバーの値。 コンテキスト情報は、クライアントに対して非透過的です。 HD オーディオ バス ドライバーでは、各クライアントのさまざまなコンテキスト オブジェクトを作成します。 クライアントが呼び出すことによって、コンテキスト オブジェクトを解放するコンテキスト オブジェクトが必要でなくなったときに、 **InterfaceDereference**ルーチンは、前の表に示すようにします。 クライアントが呼び出すことによってオブジェクトへの他の参照を作成できますが必要な場合、 **InterfaceDereference**ルーチンが、クライアントが不要になった要求して、これらの参照を解放します。

 

 




