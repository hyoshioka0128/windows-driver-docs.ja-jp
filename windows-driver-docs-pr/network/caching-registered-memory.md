---
title: 登録済みメモリのキャッシュ
description: 登録済みメモリのキャッシュ
ms.assetid: e1040f6a-6e65-462a-a79a-5d05d36787b0
keywords:
- SAN 接続のセットアップ WDK、登録されているメモリのキャッシュ
- RDMA のバッファー キャッシュ WDK San
- キャッシュ バッファーを RDMA WDK San
- 登録されているメモリ WDK San
- ローカルのアクセスには、WDK の San のキャッシュ メモリが登録されています。
- リモート アクセスには、WDK の San のキャッシュ メモリが登録されています。
- WDK の San のメモリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f15e5ffdbc9593ae680d504b751d8887d63475c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386353"
---
# <a name="caching-registered-memory"></a>登録済みメモリのキャッシュ





SAN サービス プロバイダーは、パフォーマンスを向上させるために、ローカルまたはリモートのアクセスに対して公開されている RDMA バッファーをキャッシュできます。

### <a name="caching-rdma-buffers-exposed-for-local-access"></a>ローカル アクセス用に公開されている RDMA バッファーをキャッシュ

Windows Sockets スイッチ呼び出し SAN サービス プロバイダーの[ **WSPRegisterMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566311(v=vs.85))に代わってローカル受信 RDMA をいずれかとして機能するすべてのデータ バッファーを登録するアプリケーションの拡張関数バッファーへの呼び出しで、 [ **WSPRdmaRead** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85))拡張関数またはローカルの RDMA ソースへの呼び出しで、 [ **WSPRdmaWrite** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))拡張関数。 この登録プロセスの一環として、SAN サービス プロバイダーする必要がありますの物理メモリの領域にこれらのバッファーをロックダウンし、SAN の NIC に登録 これらの操作の両方が、リソースを消費します。 そのため、SAN サービス プロバイダーはキャッシュを使用これらの登録のオーバーヘッドを軽減します。 SAN サービス プロバイダーは、キャッシュを使用している場合は、データ転送のバッファーを再利用するアプリケーションのパフォーマンスが向上します。

SAN サービス プロバイダーは、キャッシュし、次の一覧に示すようにローカル アクセスに対して公開されている RDMA バッファーを解放する必要があります。

1.  スイッチを呼び出すと、 [ **WSPDeregisterMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566279(v=vs.85)) SAN の NIC に登録されの領域にロックダウン バッファーのままにしてください、SAN サービス プロバイダー、バッファーを解放する拡張関数物理メモリです。 SAN サービス プロバイダーがバッファーは、後続の RDMA 操作、および一覧の次の項目」の説明に従って、バッファーを所有しているセキュリティで保護されたでもう一度使用する場合、バッファーを登録済みのバッファー キャッシュに追加もする必要があります。

2.  SAN サービス プロバイダーは、仮想アドレスに基づく登録のメモリをキャッシュします。 SAN サービス プロバイダーは、バッファーの登録にキャッシュ、SAN サービス プロバイダーのプロキシ ドライバーで呼び出す必要があります、 [ **MmSecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmsecurevirtualmemory)関数がその登録済みのバッファーを所有しているのためをセキュリティで保護するにはバッファーが解放された場合、オペレーティング システムは、スイッチを通知します。 (たとえば、アプリケーションを呼び出す場合、 **VirtualFree**オペレーティング システムに戻す仮想アドレス領域を解放する関数)。

3.  その後、スイッチを呼び出すと**WSPRegisterMemory**バッファーを登録するに SAN サービス プロバイダーがバッファーは既に登録されているかどうかを判断するには、そのキャッシュを確認する必要があります。 SAN サービス プロバイダーには、そのキャッシュ内のバッファーが検出されると場合、SAN サービス プロバイダーは以上の登録処理を実行する必要があります。

4.  スイッチに各 SAN サービス プロバイダーの呼び出し前に、後で登録されたバッファーの仮想物理マッピングを変更、 [ **WSPMemoryRegistrationCacheCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))拡張関数。 各 SAN サービス プロバイダーのプロキシ ドライバーでは、さらに、呼び出す必要があります、 [ **MmUnsecureVirtualMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmunsecurevirtualmemory)バッファーの所有権を解放する関数。 各 SAN サービス プロバイダーがさらに、そのキャッシュからバッファーを削除する必要があり。、SAN NIC からバッファーの登録を削除する必要があります。

5.  SAN ソケットをローカルとリモート ピア間の接続が閉じられる前に SAN サービス プロバイダーはキャッシュ バッファーをリリースする必要があります。

**注**  プロキシ ドライバーを使用する必要があります、**試用/を除く**メカニズムを呼び出すことによって保護されたユーザー モード バッファーにアクセスするコードの周り**MmSecureVirtualMemory**にオペレーティング システムのクラッシュを防止します。 プロキシのドライバーがセキュリティで保護してバッファーを解放する方法についての詳細については、次を参照してください。[の保護と仮想アドレスの所有権を解放する](securing-and-releasing-ownership-of-virtual-addresses.md)します。 詳細については**試用/を除く**、Visual C のドキュメントを参照してください。 について**VirtualFree**、Microsoft Windows SDK のドキュメントを参照してください。

 

### <a name="caching-rdma-buffers-exposed-for-remote-access"></a>リモート アクセス用に公開されている RDMA バッファーをキャッシュ

Windows Sockets スイッチ呼び出し SAN サービス プロバイダーの[ **WSPRegisterRdmaMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566313(v=vs.85))リモートのリモートのRDMAのターゲットとして機能するすべてのデータバッファーを登録する拡張関数**WSPRdmaWrite**呼び出しまたはリモートでのリモートの RDMA ソース**WSPRdmaRead**呼び出します。 つまり、スイッチは、リモート ピアによってアクセスするため、これらのバッファーを公開します。 スイッチに SAN サービス プロバイダーの呼び出し後、これらのバッファーからのデータ転送が完了したら、 [ **WSPDeregisterRdmaMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566281(v=vs.85))しなくなったようにこれらのバッファーを解放する拡張関数リモート ピアからアクセスできます。

SAN サービス プロバイダーは、次の一覧」の説明に従って、リモート アクセスに対して公開されている RDMA バッファーをキャッシュする必要があります。

1.  スイッチを呼び出すと**WSPDeregisterRdmaMemory** SAN サービス プロバイダーのバッファーを解放する物理メモリでロックされているし、SAN の NIC に登録されているバッファーのままにする必要があります SAN サービス プロバイダーがバッファーは、後続の RDMA 操作でもう一度使用する場合、バッファーを登録済みのバッファー キャッシュに追加もする必要があります。 ただし、SAN サービス プロバイダーでは、リモート ピアが、バッファーを不要になったアクセスできるようにするの適切な処置を実行する必要があります。
    **注**  場合、バッファーのみにできるアクセスできない SAN NIC からバッファーの登録を削除する SAN サービス プロバイダーが、SAN サービス プロバイダー行う必要があります。 ただし、SAN サービス プロバイダーまで物理メモリの領域がロックされているバッファーのままにする必要があります。 このシナリオでは、最適なパフォーマンスを提供しませんよりも、キャッシュなしをお勧めします。

     

2.  リモート アクセス用に公開されている RDMA バッファーをキャッシュするのには、SAN サービス プロバイダーとのローカル アクセスに対して公開されている RDMA バッファーは上記で説明されていると、そのプロキシ ドライバーはキャッシュの手法を使用する必要があります。

3.  その後、スイッチを呼び出すと**WSPRegisterRdmaMemory**バッファーを登録するに SAN サービス プロバイダーがバッファーは既に登録されているかどうかを判断するには、そのキャッシュを確認する必要があります。 SAN サービス プロバイダーには、そのキャッシュ内のバッファーが検出されると、リモート アクセス用のバッファー、SAN サービス プロバイダーを公開する必要があります、これ以上の登録操作は必要ありません。 ただし、バッファーの登録は、SAN NIC から削除された以前場合、SAN サービス プロバイダーがバッファー再登録します。

4.  SAN サービス プロバイダーにリモート アクセス用に公開されている RDMA バッファーを解放して、上記で説明されていると、そのプロキシ ドライバーは、手法を使用する必要があります。

 

 





