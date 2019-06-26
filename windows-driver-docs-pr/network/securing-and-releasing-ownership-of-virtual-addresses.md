---
title: 仮想アドレスの所有権のセキュリティ保護と解放
description: 仮想アドレスの所有権のセキュリティ保護と解放
ms.assetid: e7b31c8d-fed4-43e2-bcd2-295e3e17719e
keywords:
- プロキシ ドライバー WDK San、仮想アドレス
- SAN プロキシ ドライバー WDK、仮想アドレス
- WDK の San の仮想アドレス
- WDK 仮想アドレスの所有権
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a3de75034093139cc01b1caa180c150ea2ef4fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382121"
---
# <a name="securing-and-releasing-ownership-of-virtual-addresses"></a>仮想アドレスの所有権のセキュリティ保護と解放





プロキシ ドライバーの SAN サービス プロバイダーはこれらのバッファーにキャッシュされるたびに、プロキシ ドライバーはユーザー モードのバッファーの仮想アドレスの所有権を保護する必要があります。 バッファー キャッシュの詳細については、次を参照してください。[登録されているメモリのキャッシュ](caching-registered-memory.md)します。 プロキシ ドライバーは、ユーザー モード バッファーの所有権をセキュリティで保護、アプリケーションがオペレーティング システムに戻したり、バッファーが解放された場合に Windows Sockets を切り替える、オペレーティング システムに通知するためです。 バッファーのセキュリティで保護された所有権は、プロキシ ドライバーを呼び出す必要があります、 [ **MmSecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmsecurevirtualmemory)関数。 この呼び出しでは、プロキシ ドライバーは、バッファーとバッファーのバイト単位のサイズの開始アドレスへのポインターを渡します。

変更するのには、キャッシュされたバッファーの仮想物理マッピングがスケジュールされている場合、に、スイッチに通知し、SAN サービス プロバイダーの呼び出し[ **WSPMemoryRegistrationCacheCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))関数SAN NIC からバッファーの登録を削除し、バッファー SAN からサービス プロバイダーのキャッシュします。 SAN サービス プロバイダーのプロキシ ドライバーでは、さらに、呼び出す必要があります、 [ **MmUnsecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmunsecurevirtualmemory)バッファーの所有権を解放する関数。 この呼び出しでプロキシ ドライバーは以前から返されたバッファーにハンドルを渡す、 **MmSecureVirtualMemory**呼び出します。

**注**  を呼び出すことによって保護されたユーザー モード バッファーへのアクセスを試行するドライバー **MmSecureVirtualMemory**オペレーティング システムにも低下する可能性があります。 そのため、プロキシのドライバーが、そのようなユーザー モード バッファーにアクセスする必要がありますも使用し、**試用/を除く**バッファーにアクセスするコードの周りのメカニズムです。 詳細については**試用/を除く**、Visual C のドキュメントを参照してください。

 

SAN サービス プロバイダーは、セキュリティで保護し、バッファーの所有権を解放するには、プロキシ ドライバーを I/O コントロール (IOCTL) 要求を送信できます。 詳細については、次を参照してください。 [SAN サービス プロバイダーの実装の Ioctl](implementing-ioctls-for-a-san-service-provider.md)します。

 

 





