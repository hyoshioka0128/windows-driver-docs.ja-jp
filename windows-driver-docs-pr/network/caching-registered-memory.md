---
title: 登録済みメモリのキャッシュ
description: 登録済みメモリのキャッシュ
ms.assetid: e1040f6a-6e65-462a-a79a-5d05d36787b0
keywords:
- SAN 接続のセットアップ WDK、登録されたメモリのキャッシュ
- RDMA バッファーキャッシュ WDK San
- RDMA バッファーのキャッシュ WDK San
- 登録済みメモリ WDK San
- ローカルアクセス登録済みメモリキャッシュ WDK San
- リモートアクセス登録済みメモリキャッシュ WDK San
- メモリ WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c225e40ae2176d0530563767ecd7816fce7a3d00
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835269"
---
# <a name="caching-registered-memory"></a>登録済みメモリのキャッシュ





SAN サービスプロバイダーは、ローカルまたはリモートのアクセスに対して公開されている RDMA バッファーをキャッシュして、パフォーマンスを向上させることができます。

### <a name="caching-rdma-buffers-exposed-for-local-access"></a>ローカルアクセス用に公開された RDMA バッファーのキャッシュ

Windows ソケットスイッチは、アプリケーションに代わって SAN サービスプロバイダーの[**WSPRegisterMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566311(v=vs.85)) extension 関数を呼び出して、 [**WSPRdmaWrite**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))拡張機能関数の呼び出しで、ローカルの受信 RDMA バッファーとして機能するすべてのデータバッファーを[**WSPRdmaRead**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85)) extension 関数またはローカル RDMA ソースのいずれかとして登録します。 この登録プロセスの一環として、SAN サービスプロバイダーはこれらのバッファーを物理メモリの領域にロックダウンし、SAN NIC に登録する必要があります。 これらの操作はどちらもリソースを集中的に消費します。 そのため、SAN サービスプロバイダーはキャッシュを使用して、これらの登録のオーバーヘッドを軽減する必要があります。 SAN サービスプロバイダーがキャッシュを使用する場合、データ転送のためにバッファーを再利用するアプリケーションのパフォーマンスが向上します。

SAN サービスプロバイダーは、次の一覧に示すように、ローカルアクセス用に公開されている RDMA バッファーをキャッシュおよび解放する必要があります。

1.  スイッチが[**WSPDeregisterMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566279(v=vs.85)) extension 関数を呼び出してバッファーを解放すると、san サービスプロバイダーは、バッファーを san NIC に登録し、物理メモリの領域にロックダウンする必要があります。 また、次のリスト項目で説明されているように、その後の RDMA 操作でバッファーが再度使用される場合に備えて、登録されたバッファーのキャッシュにバッファーを追加する必要があります。

2.  SAN サービスプロバイダーは、仮想アドレスに基づいてメモリ登録をキャッシュします。 SAN サービスプロバイダーがバッファーの登録をキャッシュする場合、SAN サービスプロバイダーのプロキシドライバーは、 [**Mmsecurevirtualmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory)関数を呼び出して、バッファーが解放されたときにオペレーティングシステムによってスイッチに通知されるようにします (たとえば、アプリケーションが**VirtualFree**関数を呼び出して仮想アドレス範囲をオペレーティングシステムに解放する場合など)。

3.  その後、スイッチが**WSPRegisterMemory**を呼び出してバッファーを登録すると、SAN サービスプロバイダーはそのキャッシュを確認して、バッファーが既に登録されているかどうかを確認する必要があります。 SAN サービスプロバイダーがキャッシュ内のバッファーを検出した場合、SAN サービスプロバイダーは、それ以上の登録操作を実行することはできません。

4.  その後、登録されたバッファーの仮想から物理へのマッピングが変更される前に、スイッチは各 SAN サービスプロバイダーの[**WSPMemoryRegistrationCacheCallback**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))拡張機能を呼び出します。 さらに、各 SAN サービスプロバイダーのプロキシドライバーは、 [**Mmunsecurevirtualmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmunsecurevirtualmemory)関数を呼び出して、バッファーの所有権を解放する必要があります。 さらに、各 SAN サービスプロバイダーは、そのキャッシュからバッファーを削除する必要があり、SAN NIC からバッファー登録を削除する必要があります。

5.  ローカル SAN ソケットとリモートピア間の接続が切断される前に、SAN サービスプロバイダーがキャッシュされたバッファーを解放する必要があります。

**注**  、オペレーティングシステムのクラッシュを防ぐために、 **Mmsecurevirtualmemory**への呼び出しによってセキュリティで保護されたユーザーモードのバッファーにアクセスするコードについては、プロキシドライバーが**try/except**機構を使用する必要があることに注意してください。 プロキシドライバーがバッファーをセキュリティで保護する方法と解放する方法の詳細については、「[仮想アドレスの所有権の保護と解放](securing-and-releasing-ownership-of-virtual-addresses.md)」を参照してください。 **Try/except**の詳細については、ビジュアルC++ドキュメントを参照してください。 **VirtualFree**の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

### <a name="caching-rdma-buffers-exposed-for-remote-access"></a>リモートアクセス用に公開されている RDMA バッファーのキャッシュ

Windows ソケットスイッチは、SAN サービスプロバイダーの[**WSPRegisterRdmaMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566313(v=vs.85)) extension 関数を呼び出して、リモート**WSPRdmaWrite**呼び出しのリモート rdma ターゲットまたはリモート**WSPRdmaRead**呼び出しのリモート rdma ソースとして機能するすべてのデータバッファーを登録します。 つまり、スイッチは、リモートピアによるアクセスのためにこれらのバッファーを公開します。 これらのバッファーからのデータ転送が完了すると、スイッチは SAN サービスプロバイダーの[**WSPDeregisterRdmaMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566281(v=vs.85)) extension 関数を呼び出してこれらのバッファーを解放し、リモートピアからアクセスできなくなります。

SAN サービスプロバイダーは、次の一覧に示すように、リモートアクセス用に公開されている RDMA バッファーをキャッシュする必要があります。

1.  スイッチが**WSPDeregisterRdmaMemory**を呼び出してバッファーを解放すると、san サービスプロバイダーはバッファーを物理メモリにロックしたままにして、san NIC に登録する必要があります。 また、その後の RDMA 操作でバッファーが再度使用される場合に備えて、登録済みのバッファーのキャッシュにもバッファーを追加する必要があります。 ただし、SAN サービスプロバイダーは、リモートピアがバッファーにアクセスできなくなるように、適切な操作を行う必要があります。
    **注**  san NIC からバッファー登録を削除する san サービスプロバイダーがバッファーにアクセスできない場合は、san サービスプロバイダーがこの処理を行う必要があります。 ただし、SAN サービスプロバイダーはバッファーを物理メモリ領域にロックしたままにしておく必要があります。 このシナリオでは最適なパフォーマンスは得られませんが、キャッシュを使用するよりも優れています。

     

2.  リモートアクセス用に公開されている RDMA バッファーをキャッシュするには、SAN サービスプロバイダーとそのプロキシドライバーは、前の一覧で説明したように、ローカルアクセス用に公開されている RDMA バッファーのキャッシュ技法を使用する必要があります。

3.  その後、スイッチが**WSPRegisterRdmaMemory**を呼び出してバッファーを登録すると、SAN サービスプロバイダーはそのキャッシュを確認して、バッファーが既に登録されているかどうかを確認する必要があります。 SAN サービスプロバイダーがキャッシュ内のバッファーを検出した場合、SAN サービスプロバイダーは単にリモートアクセス用のバッファーを公開する必要があります。これ以上の登録操作は必要ありません。 ただし、バッファー登録が SAN NIC から既に削除されている場合、SAN サービスプロバイダーはバッファーを再度登録する必要があります。

4.  リモートアクセス用に公開されている RDMA バッファーを解放するには、SAN サービスプロバイダーとそのプロキシドライバーで、前の一覧に記載されている手法を使用する必要があります。

 

 





