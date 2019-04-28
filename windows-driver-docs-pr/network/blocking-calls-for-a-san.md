---
title: SAN の呼び出しのブロック
description: SAN の呼び出しのブロック
ms.assetid: 93be861c-4cf1-48ea-ac69-a4a171ca9052
keywords:
- WDK の San のブロッキング呼び出し
- Windows ソケットはブロッキング呼び出し WDK を直接します。
- SAN のブロッキング呼び出し WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a851f2ae874a2a016add304376805e15c1a0a82d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367684"
---
# <a name="blocking-calls-for-a-san"></a>SAN の呼び出しのブロック





Windows ソケットは、呼び出しをブロックしているハンドルを切り替えてなどのキャンセルは内部的にまたは TCP/IP サービスのプロバイダーに転送します。 スイッチが呼び出すことはありません、 **WSPCancelBlockingCall**進行中のブロックの要求をキャンセルする SAN サービス プロバイダーの関数。 そのため、SAN サービス プロバイダーは、実装する必要はありません、 **WSPCancelBlockingCall**関数。

スイッチは、次の方法で、次の要求をブロックしていると対応する取り消しを処理します。

-   ブロッキング モードで特定の宛先アドレスに SAN のソケットを接続するアプリケーションを要求するときにスイッチはブロッキングを受け取ります**WSPConnect**呼び出します。 スイッチを適切なの SAN サービス プロバイダーの非ブロッキング モードで接続要求を転送する[ **WSPConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff566275)関数。 SAN サービス プロバイダーの場合は、スイッチは、何らかの理由により、この接続要求を取り消す必要があります、呼び出す[ **WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273)関数。 SAN サービス プロバイダーは、接続要求を中止し、ソケットのリソースを解放する必要があります速やかにします。

-   スイッチは、SAN のソケットでのデータ転送操作を実行するアプリケーションによって開始されたブロックの要求を受信するときに適切な SAN サービス プロバイダーにオーバー ラップの (非ブロッキング) 方法でデータの転送要求を転送します。 スイッチは、同期 (ブロック) を受け取る場合など、 **WSPSend**呼び出し、適切なの SAN サービス プロバイダーの呼び出し[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)オーバー ラップの (関数非ブロッキング) 方法です。 後でアプリケーションがデータ転送操作をキャンセルし、アプリケーションのバッファーのスイッチを制御する場合、スイッチは、障害状態で、アプリケーションの要求を完了します。 アプリケーションのバッファーが未処理の RDMA 操作に関係している場合は、操作を完了するスイッチが待機します。 スイッチが適切なの SAN サービス プロバイダーを呼び出して RDMA の転送を完了するには長すぎる場合は、 **WSPCloseSocket**欠如完了、中止になる方法で接続を閉じます。

**注**  保持されている接続に依存するアプリケーションでは、ブロッキング呼び出しをキャンセルした場合ことはできません。 のみ、 **WSPCloseSocket**呼び出しがブロックしている要求のキャンセル後ソケットで成功することが保証されます。 詳細については、Microsoft Windows SDK の Windows Sockets SPI ドキュメントを参照してください。

 

 

 





