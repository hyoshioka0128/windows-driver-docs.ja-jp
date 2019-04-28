---
title: SAN NIC 通知の登録
description: SAN NIC 通知の登録
ms.assetid: 6a630e7c-3b1a-4f4a-b808-f6b4e2315a42
keywords:
- NIC 通知 WDK San
- プロキシ ドライバー WDK San、NIC の通知
- SAN プロキシ ドライバー WDK、NIC の通知
- NIC の通知を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7dbb9f789ec3f390c0f0e639101e3775efc6fcc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373885"
---
# <a name="registering-for-san-nic-notifications"></a>SAN NIC 通知の登録





プロキシ ドライバーがドライバーの管理下にある Nic に割り当てられた IP アドレスの一覧を指定する、関連付けられている SAN サービス プロバイダーから要求を受け取ったときに、ドライバーを決定し、プロバイダーにこの一覧を渡します。

これらの IP アドレスを取得するためにプロキシ ドライバーのアドレス変更通知を受信するトランスポート ドライバー インターフェイス (TDI) で登録する必要があります。 プロキシのドライバーの呼び出し、 [ **TdiRegisterPnPHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff565062)関数。 この呼び出しでこのプロキシ ドライバーがコールバック関数にポインターを渡す、 **AddAddressHandlerV2**と**DelAddressHandlerV2** 、TDI のメンバー\_クライアント\_インターフェイス\_情報構造体のアドレスの追加と削除のコールバック関数を指定します。 後に、 **TdiRegisterPnPHandlers**関数が正常に返された、TDI すぐにことを示しますプロキシ ドライバーでは、現在アクティブなネットワーク アドレスをすべてアドレスと、追加のコールバックを使用します。 表示には、ネットワーク アドレスとこれらのアドレスがバインドされているデバイスの識別子の両方が含まれています。

たびに TDI で呼び出しをアドレスの追加機能を示すためにこれらのコールバック関数のいずれかまたは削除、プロキシ ドライバーには、次のパラメーターが必要です。

<a href="" id="address"></a>*アドレス*  
TA へのポインター\_ネットワーク アドレスを記述するアドレスの構造体またはいずれかに割り当てられている NIC から削除 TCP/IP の場合このポインターは、実際には、TA へのポインター\_アドレス\_IP 構造体。

<a href="" id="devicename"></a>*デバイス名*  
アドレスが関連付けられている NIC-トランスポートのバインドを識別する Unicode 文字列へのポインター。 TCP/IP が発生した場合、Unicode 文字列は、次の形式があります。\\デバイス\\Tcpip\_{NIC の GUID} NIC-GUID は、ネットワーク構成のサブシステムによって NIC に割り当てられたグローバル一意識別子

上記の構造体の定義は、tdi.h ヘッダー ファイルで定義されます。 上記の登録とコールバック関数は、tdikrnl.h ヘッダー ファイルで定義されます。 これらのヘッダー ファイルは、Microsoft Windows ドライバー開発キット (DDK) と Windows Driver Kit (WDK) で使用できます。 TDI プラグ アンド プレイ (PnP) 通知の詳細については、次を参照してください。 [TDI クライアント コールバック](https://msdn.microsoft.com/library/windows/hardware/ff565081)と[TDI クライアント イベントと PnP 通知ハンドラー](https://msdn.microsoft.com/library/windows/hardware/ff565082)します。

システムの起動時に TDI は現在アクティブなすべての IP アドレスを示すために、プロキシ ドライバーのアドレス追加コールバックを呼び出します。 TDI は、TCP/IP トランスポート プロトコル TDI で新しい IP アドレスを登録するときにもこのコールバックを呼び出します。 プロキシのドライバーには IP アドレスの一覧に、プロキシ ドライバーの Nic に割り当てられているアドレスのみが含まれています。 ドライバーのアドレス追加コールバック コントロールすぐに、ドライバーでの NIC が認識されない場合*DeviceName*します。

TDI では、NIC が削除されている TCP/IP トランスポート プロトコルを示します TDI するたびに、プロキシ ドライバーのアドレスの削除コールバックが呼び出されます。 NIC の IP アドレスが、プロキシ ドライバーの Nic のいずれかに所属している場合、プロキシ ドライバーは、リストから IP アドレスを削除します。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://msdn.microsoft.com/library/windows/hardware/ff571067)または[Winsock Kernel](https://msdn.microsoft.com/library/windows/hardware/ff571083)代わりにします。

 

 

 





