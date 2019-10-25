---
title: SAN NIC 通知の登録
description: SAN NIC 通知の登録
ms.assetid: 6a630e7c-3b1a-4f4a-b808-f6b4e2315a42
keywords:
- NIC 通知の WDK San
- プロキシドライバー WDK San, NIC 通知
- SAN プロキシドライバー WDK、NIC 通知
- NIC 通知を登録しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8343c698a8589d2a1b34a56b53c07a31575f46a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842072"
---
# <a name="registering-for-san-nic-notifications"></a>SAN NIC 通知の登録





プロキシドライバーは、関連付けられている SAN サービスプロバイダーから要求を受信して、ドライバーの制御下で Nic に割り当てられた IP アドレスの一覧を提供するときに、ドライバーが決定し、この一覧をプロバイダーに渡します。

これらの IP アドレスを取得するには、プロキシドライバーがアドレス変更通知を受信するために Transport Driver Interface (TDI) に登録する必要があります。 プロキシドライバーは、 [**TdiRegisterPnPHandlers**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565062(v=vs.85))関数を呼び出します。 この呼び出しで、このプロキシドライバーは、TDI\_クライアント\_インターフェイス\_INFO 構造体の**AddAddressHandlerV2**メンバーと**DelAddressHandlerV2**メンバーのコールバック関数へのポインターを渡して、のコールバック関数を指定します。アドレスの追加と削除を行います。 **TdiRegisterPnPHandlers**関数が正常に返された後、TDI は、アドレス追加コールバックを使用して、現在アクティブなすべてのネットワークアドレスをプロキシドライバーに対して直ちに示します。 この表示には、これらのアドレスがバインドされているデバイスのネットワークアドレスと識別子の両方が含まれています。

TDI がアドレスの追加または削除を示すためにこれらのコールバック関数のいずれかを呼び出すと、プロキシドライバーは次のパラメーターを必要とします。

<a href="" id="address"></a>*先*  
NIC に割り当てられるか、NIC から削除されるネットワークアドレスを記述する TA\_アドレス構造体へのポインター。 TCP/IP の場合、このポインターは実際には TA\_アドレス\_IP 構造へのポインターです。

<a href="" id="devicename"></a>*DeviceName*  
アドレスが関連付けられているトランスポートから NIC へのバインドを識別する Unicode 文字列へのポインター。 TCP/IP の場合、Unicode 文字列の形式は次のようになります。 \\デバイス\\Tcpip\_{NIC-GUID}。ここで、NIC-GUID はネットワーク構成サブシステムによって NIC に割り当てられたグローバル一意識別子です。

前の構造体の定義は、tdi ヘッダーファイルで定義されています。 前述の登録およびコールバック関数は、tdikrnl ヘッダーファイルで定義されています。 これらのヘッダーファイルは、Microsoft Windows Driver Development Kit (DDK) および Windows Driver Kit (WDK) で使用できます。 TDI プラグアンドプレイ (PnP) 通知の詳細については、「 [Tdi クライアントコールバック](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565081(v=vs.85))と[tdi クライアントイベントおよび pnp 通知ハンドラー](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565082(v=vs.85))」を参照してください。

システムの起動時に、TDI はプロキシドライバーのアドレス追加コールバックを呼び出して、現在アクティブなすべての IP アドレスを示します。 また、TDI は、TCP/IP トランスポートプロトコルが新しい IP アドレスを TDI に登録するたびに、このコールバックを呼び出します。 プロキシドライバーは、プロキシドライバーの Nic に割り当てられているアドレスのみを IP アドレスの一覧に含めます。 ドライバーが*DeviceName*の NIC を認識しない場合、ドライバーのアドレス追加コールバックは、制御を直ちに返す必要があります。

TDI は、NIC が削除されたことを TCP/IP トランスポートプロトコルが示す場合は常に、プロキシドライバーのアドレス削除コールバックを呼び出します。 NIC の IP アドレスがプロキシドライバーの Nic のいずれかに属している場合は、プロキシドライバーによって一覧から IP アドレスが削除されます。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

 

 





