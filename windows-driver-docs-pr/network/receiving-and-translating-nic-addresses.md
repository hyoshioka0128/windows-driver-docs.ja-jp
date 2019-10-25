---
title: NIC アドレスの受信と変換
description: NIC アドレスの受信と変換
ms.assetid: c7171a4d-cc77-427e-8d23-8811f650e543
keywords:
- Windows Sockets Direct WDK、SAN 使用率の初期化
- SAN 使用率を初期化しています
- NIC アドレス変換 WDK San
- NIC アドレスの WDK San の変換
- San 用の NIC アドレスの受信
- WDK San に対処する
- 削除-アドレス通知 WDK San
- アドレス通知の追加の WDK San
- 通知 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fa50a5651316083068a4ceee6668c187e4c534b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844853"
---
# <a name="receiving-and-translating-nic-addresses"></a>NIC アドレスの受信と変換





Windows ソケットスイッチは、SAN サービスプロバイダーおよび SAN Nic とやり取りするときに、IP アドレスを含む[Wsk アドレスファミリ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))を常に使用します。 スイッチで、SAN のネイティブアドレスファミリが使用されていません。 そのため、SAN サービスプロバイダーは、関連付けられているプロキシドライバーを使用して、Nic に割り当てられている IP アドレスの一覧を取得する必要があります。 SAN サービスプロバイダーは、プロキシドライバーと対話するときに、これらの IP アドレスを使用します。 プロキシドライバーは、IP アドレスとネイティブアドレスの間で変換される必要があります。

初期化中に、プロキシドライバーは通常、アドレス変更通知のために Transport Driver Interface (TDI) に登録されます。 TCP/IP を含むすべてのプラグアンドプレイ (PnP) 対応トランスポートは、このような通知に登録されているクライアントに対して、TDI 経由でアドレス変更通知を提供します。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

### <a name="registering-for-address-change-notification"></a>アドレス変更通知の登録

初期化中に、プロキシドライバーは[**TdiRegisterPnPHandlers**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565062(v=vs.85))関数を呼び出して、アドレス変更通知を登録します。 この呼び出しでは、プロキシドライバーは、TDI\_クライアント\_インターフェイス\_INFO 構造体の**AddAddressHandlerV2**メンバーと**DelAddressHandlerV2**メンバーでアドレスの追加と削除を行うためのコールバック関数へのポインターを渡します。 これらの通知を受信するためにプロキシドライバーが登録した後、TDI は、アドレス指定コールバックを使用して現在アクティブなすべてのネットワークアドレスを即座に示します。

TDI は、次のパラメーターをプロキシドライバーの追加または削除のコールバック関数に渡します。

<a href="" id="address"></a>*先*  
NIC に割り当てられているか、NIC から削除されたネットワークアドレスを記述する TA\_アドレス構造体へのポインター。 TCP/IP の場合、このポインターは実際には TA\_アドレス\_IP 構造へのポインターです。

<a href="" id="devicename"></a>*DeviceName*  
アドレスが関連付けられているトランスポートから NIC へのバインドを識別する Unicode 文字列へのポインター。 TCP/IP の場合、Unicode 文字列の形式は次のようになります。

\\デバイス\\Tcpip\_{NIC-GUID}

ここで、NIC はネットワーク構成サブシステムによって NIC に割り当てられたグローバル一意識別子です。

前の構造体の定義は、tdi ヘッダーファイルで定義されています。 前述の登録およびコールバック関数は、tdikrnl ヘッダーファイルで定義されています。 これらのヘッダーファイルは、Microsoft Windows Driver Development Kit (DDK) および Windows Driver Kit (WDK) で使用できます。 Tdi の PnP 通知の詳細については、tdi[クライアントコールバック](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565081(v=vs.85))と[tdi クライアントイベントおよび PnP 通知ハンドラー](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565082(v=vs.85))に含まれています。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

### <a name="maintaining-a-list-of-ip-addresses"></a>IP アドレスの一覧の管理

SAN サービスプロバイダーのプロキシドライバーは、アドレスの追加と削除の通知を使用して、各 NIC に割り当てられた IP アドレスの一覧を管理下に保持します。 プロキシドライバーは、この一覧を使用して、SAN NIC に割り当てられた1つ以上の IP アドレスを TCP/IP トランスポートとネイティブ SAN アドレスに変換します。 また、プロキシドライバーはデバイス制御ルーチンを提供する必要があります。これにより、スイッチがクエリ制御コードクエリ\_SIO\_アドレス\_リストを作成するたびに、NIC に割り当てられた IP アドレスの一覧が Windows ソケットスイッチで使用可能になります。 プロキシドライバーの**Driverentry**ルーチンは、このデバイス制御ルーチンのエントリポイントを指定する必要があります。

Windows ソケットスイッチでは、各 SAN NIC に割り当てられているすべての IP アドレスの一覧が保持されます。 この包括リストの IP アドレスを取得するには、スイッチは各 SAN サービスプロバイダーの[**WSPIoctl**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))関数を呼び出し、SIO\_ADDRESS\_LIST\_クエリ制御コードを渡します。 各 SAN サービスプロバイダーは、関連付けられているプロキシドライバーに対して、その SAN Nic に割り当てられている IP アドレスの個々のリストを照会します。 スイッチにアドレスの変更が通知された後、各 SAN サービスプロバイダーに対して、個々のリストの更新を照会します。

 

 





