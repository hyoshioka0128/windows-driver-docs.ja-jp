---
title: 仮想アドレスの所有権のセキュリティ保護と解放
description: 仮想アドレスの所有権のセキュリティ保護と解放
ms.assetid: e7b31c8d-fed4-43e2-bcd2-295e3e17719e
keywords:
- プロキシドライバー WDK San、仮想アドレス
- SAN プロキシドライバー WDK、仮想アドレス
- 仮想アドレス WDK San
- WDK 仮想アドレスの所有権
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bf44c3b266cb5f73045768d850d94aeaf5b4ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841994"
---
# <a name="securing-and-releasing-ownership-of-virtual-addresses"></a>仮想アドレスの所有権のセキュリティ保護と解放





プロキシドライバーの SAN サービスプロバイダーがこれらのバッファーをキャッシュするたびに、プロキシドライバーはユーザーモードバッファーの仮想アドレスの所有権をセキュリティで保護する必要があります。 バッファーのキャッシュの詳細については、「[登録済みメモリのキャッシュ](caching-registered-memory.md)」を参照してください。 プロキシドライバーは、ユーザーモードバッファーの所有権をセキュリティで保護します。これにより、オペレーティングシステムは、バッファーがアプリケーションによってオペレーティングシステムに解放された場合に Windows ソケットスイッチに通知します。 バッファーの所有権をセキュリティで保護するには、プロキシドライバーが[**Mmsecurevirtualmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory)関数を呼び出す必要があります。 この呼び出しでは、プロキシドライバーは、バッファーの開始アドレスとバッファーのサイズ (バイト単位) へのポインターを渡します。

キャッシュされたバッファーの仮想から物理へのマッピングが変更されるようにスケジュールされている場合、スイッチには通知され、san NIC からのバッファー登録と SAN サービスプロバイダーのキャッシュからのバッファーを削除するために、SAN サービスプロバイダーの[**WSPMemoryRegistrationCacheCallback**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))関数が呼び出されます。 さらに、SAN サービスプロバイダーのプロキシドライバーは、 [**Mmunsecurevirtualmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmunsecurevirtualmemory)関数を呼び出して、バッファーの所有権を解放する必要があります。 この呼び出しでは、プロキシドライバーは、以前に**Mmsecurevirtualmemory**呼び出しから返されたバッファーにハンドルを渡します。

**Mmsecurevirtualmemory**への呼び出しによってセキュリティで保護されたユーザーモードのバッファーにアクセスしようとするドライバーは、オペレーティングシステムをダウンさせる可能性**が  ます**。 したがって、プロキシドライバーは、このようなユーザーモードバッファーにアクセスするときに、バッファーにアクセスするコードの前後の**try/except**機構も使用する必要があります。 **Try/except**の詳細については、ビジュアルC++ドキュメントを参照してください。

 

SAN サービスプロバイダーは、プロキシドライバーに i/o 制御 (IOCTL) 要求を送信して、バッファーの所有権を保護および解放できます。 詳細については、「 [SAN サービスプロバイダーの ioctl の実装](implementing-ioctls-for-a-san-service-provider.md)」を参照してください。

 

 





