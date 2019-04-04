---
title: セキュリティで保護して、仮想アドレスの所有権を解放します。
description: セキュリティで保護して、仮想アドレスの所有権を解放します。
ms.assetid: e7b31c8d-fed4-43e2-bcd2-295e3e17719e
keywords:
- プロキシ ドライバー WDK San、仮想アドレス
- SAN プロキシ ドライバー WDK、仮想アドレス
- WDK の San の仮想アドレス
- WDK 仮想アドレスの所有権
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29837bb65680db471bf4d16d18a5ff6e25b036e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537845"
---
# <a name="securing-and-releasing-ownership-of-virtual-addresses"></a>セキュリティで保護して、仮想アドレスの所有権を解放します。





プロキシ ドライバーの SAN サービス プロバイダーはこれらのバッファーにキャッシュされるたびに、プロキシ ドライバーはユーザー モードのバッファーの仮想アドレスの所有権を保護する必要があります。 バッファー キャッシュの詳細については、[登録されているメモリのキャッシュ](caching-registered-memory.md)を参照してください。 プロキシ ドライバーは、ユーザー モード バッファーの所有権をセキュリティで保護、アプリケーションがオペレーティング システムに戻したり、バッファーが解放された場合に Windows Sockets を切り替える、オペレーティング システムに通知するためです。 バッファーのセキュリティで保護された所有権は、プロキシ ドライバーを呼び出す必要があります、 [ **MmSecureVirtualMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff556374)関数。 この呼び出しでは、プロキシ ドライバーは、バッファーとバッファーのバイト単位のサイズの開始アドレスへのポインターを渡します。

変更するのには、キャッシュされたバッファーの仮想物理マッピングがスケジュールされている場合、に、スイッチに通知し、SAN サービス プロバイダーの呼び出し[ **WSPMemoryRegistrationCacheCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff566299)関数SAN NIC からバッファーの登録を削除し、バッファー SAN からサービス プロバイダーのキャッシュします。 SAN サービス プロバイダーのプロキシ ドライバーでは、さらに、呼び出す必要があります、 [ **MmUnsecureVirtualMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff556395)バッファーの所有権を解放する関数。 この呼び出しでプロキシ ドライバーは以前から返されたバッファーにハンドルを渡す、 **MmSecureVirtualMemory**呼び出します。

**注**  を呼び出すことによって保護されたユーザー モード バッファーへのアクセスを試行するドライバー **MmSecureVirtualMemory**オペレーティング システムにも低下する可能性があります。 そのため、プロキシのドライバーが、そのようなユーザー モード バッファーにアクセスする必要がありますも使用し、**試用/を除く**バッファーにアクセスするコードの周りのメカニズムです。 詳細については**試用/を除く**、Visual C のドキュメントを参照してください。

 

SAN サービス プロバイダーは、セキュリティで保護し、バッファーの所有権を解放するには、プロキシ ドライバーを I/O コントロール (IOCTL) 要求を送信できます。 詳細については、[SAN サービス プロバイダーの実装の Ioctl](implementing-ioctls-for-a-san-service-provider.md)を参照してください。

 

 





