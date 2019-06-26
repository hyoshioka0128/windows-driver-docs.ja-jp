---
title: NIC アドレスの受信と変換
description: NIC アドレスの受信と変換
ms.assetid: c7171a4d-cc77-427e-8d23-8811f650e543
keywords:
- SAN 使用率を初期化しています。 Windows Sockets 直接 WDK
- SAN 使用率の初期化
- NIC アドレス翻訳 WDK San
- NIC アドレス WDK San の変換
- NIC の受信に対処の San
- WDK の San のアドレス
- アドレスの削除通知 WDK San
- アドレスの追加通知 WDK San
- WDK の San の通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eecfd5a8d7decc35e3d75ba08ea521708c9c7d6a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368472"
---
# <a name="receiving-and-translating-nic-addresses"></a>NIC アドレスの受信と変換





Windows Sockets 切り替える使用では常に、 [WSK アドレス ファミリ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))、SAN サービス プロバイダーと SAN Nic とやり取りするとき、IP アドレスを格納します。 スイッチは、SAN のネイティブのアドレス ファミリを使用しません。 そのため、SAN サービス プロバイダーは、その Nic に割り当てられた IP アドレスの一覧を取得するのに、関連付けられているプロキシ ドライバーを使用する必要があります。 SAN サービス プロバイダーは、そのプロキシ ドライバーと対話するときに、これらの IP アドレスを使用します。 プロキシ ドライバーは、IP アドレスとネイティブのアドレスの間で変換する必要があります。

初期化中に、プロキシ ドライバーは通常のアドレス変更通知トランスポート ドライバー Interface (TDI) を登録します。 すべてプラグ アンド プレイ (PnP) に注意してくださいを含めた、トランスポート TCP/IP は、このような通知に登録しているクライアントに TDI を通じてアドレス変更通知を指定します。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)または[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)代わりにします。

 

### <a name="registering-for-address-change-notification"></a>アドレス変更通知を登録します。

初期化中に、プロキシ ドライバーを呼び出し、 [ **TdiRegisterPnPHandlers** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565062(v=vs.85))変更通知を関数のアドレスを登録します。 この呼び出しでプロキシ ドライバーはアドレスの追加や削除でコールバック関数へのポインターを渡します、 **AddAddressHandlerV2**と**DelAddressHandlerV2** 、TDI のメンバー\_クライアント\_インターフェイス\_情報構造体。 プロキシ ドライバーは、これらの通知を受信するレジスタ後、TDI はすぐに追加アドレス コールバックを使用してすべての現在アクティブなネットワーク アドレスを示します。

TDI はプロキシ ドライバーの追加アドレスまたはアドレスの削除のコールバック関数に次のパラメーターに渡します。

<a href="" id="address"></a>*アドレス*  
TA へのポインター\_ネットワーク アドレスを示すアドレス構造に割り当てられているか、NIC から削除 TCP/IP の場合、このポインターは実際には、TA を指すポインターは\_アドレス\_IP 構造体。

<a href="" id="devicename"></a>*デバイス名*  
アドレスが関連付けられている NIC-トランスポートのバインドを識別する Unicode 文字列へのポインター。 TCP/IP が発生した場合、Unicode 文字列は、次の形式があります。

\\デバイス\\Tcpip\_{NIC GUID}

NIC-GUID は、ネットワーク構成のサブシステムによって NIC に割り当てられたグローバル一意識別子です。

上記の構造体の定義は、tdi.h ヘッダー ファイルで定義されます。 上記の登録とコールバック関数は、tdikrnl.h ヘッダー ファイルで定義されます。 これらのヘッダー ファイルは、Microsoft Windows ドライバー開発キット (DDK) と Windows Driver Kit (WDK) で使用できます。 TDI PnP 通知に関する詳細情報が記載されて[TDI クライアント コールバック](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565081(v=vs.85))と[TDI クライアント イベントと PnP 通知ハンドラー](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565082(v=vs.85))します。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)または[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)代わりにします。

 

### <a name="maintaining-a-list-of-ip-addresses"></a>IP アドレスの一覧を管理します。

SAN サービス プロバイダーのプロキシ ドライバーでは、追加アドレスとアドレスの削除の通知を使用して、その管理下にある各 NIC に割り当てられた IP アドレスの一覧を管理します。 プロキシ ドライバーでは、このリストを使用して、TCP/IP トランスポートによって SAN NIC に割り当てられた IP アドレスとネイティブの SAN アドレスの 1 つまたは複数の間で変換します。 プロキシ ドライバーは、スイッチ、スイッチにより、SIO たびに、Windows ソケットを使用可能な NIC に割り当てられた IP アドレスの一覧は、デバイス制御ルーチンも指定する必要があります\_アドレス\_一覧\_クエリの制御コードクエリ。 プロキシ ドライバーの**DriverEntry**ルーチンは、このデバイス制御ルーチンのエントリ ポイントを指定する必要があります。

Windows Sockets スイッチは、各 SAN NIC に割り当てられているすべての IP アドレスのリストを保持します。 この包括的な一覧については、IP アドレスを取得するスイッチが SAN サービス プロバイダーの各を呼び出す[ **WSPIoctl** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))関数を SIO\_アドレス\_一覧\_制御コードをクエリします。 各 SAN サービス プロバイダーは、さらに、その SAN Nic に割り当てられた IP アドレスの個々 の一覧については、関連付けられているプロキシ ドライバーを照会します。 スイッチは、アドレスの変更の通知は、後にもう一度、各個々 のリストの更新プログラムの各 SAN サービス プロバイダーを照会します。

 

 





