---
title: MSI-X を動的に構成する
description: MSI-X を動的に構成する
ms.assetid: 53051239-e00f-41e8-b95d-9618693e696d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 77224c97a6b63e4e890d59cf2205ea177561bad6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838711"
---
# <a name="dynamically-configuring-msi-x"></a>MSI-X を動的に構成する


Windows Vista Service Pack 1 (SP1)、Windows Server 2008、およびそれ以降のオペレーティングシステムでは、MSI-X 割り込みメッセージのプロパティの動的な変更がサポートされています。 (PCI 3.0 仕様では、MSI-X が定義されています)。PCI バスドライバーは\_MSIX\_TABLE\_CONFIG\_インターフェイスインターフェイスの GUID を公開し、PCI デバイスのドライバーがバスハードウェア割り込みテーブルの設定を変更できるようにします。

ドライバーは、 [**IRP\_\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求をバスドライバーに送信することによってインターフェイスを使用します。このとき、 *InterfaceType*パラメーターは\_GUID と同じであり、MSIX\_テーブル\_CONFIG\_インターフェイスに等しくなります。 バスドライバーは、 [**PCI\_MSIX\_テーブル\_CONFIG\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pci_msix_table_config_interface)構造へのポインターを提供します。これにより、割り込みテーブルを変更する3つのルーチンへのポインターが提供されます。

-   [*Settableentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pci_msix_set_entry)は、ハードウェアテーブルエントリにメッセージ ID を割り当てます。

-   [*Masktableentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pci_msix_maskunmask_entry)は、ハードウェアテーブルエントリに対応する割り込みをマスクします。

-   [*Unmasktableentry*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/gg604859(v=vs.85))は、ハードウェアテーブルエントリに対応する割り込みをマスク解除します。

既定では、割り込みテーブルは、最初のエントリがメッセージ ID ゼロ、2番目のエントリがメッセージ ID 1 などを持つように構成されます。 テーブルエントリの数がメッセージ数を超える場合は、追加の各テーブルエントリにメッセージ ID 0 が割り当てられます。 (メッセージ ID は、ドライバーのメッセージシグナル割り込みを記述する[**IO\_interrupt\_message\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_interrupt_message_info)構造体の**messageinfo**メンバーの割り込みのエントリのインデックスです。 [**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)ルーチンは、この構造体へのポインターを提供します)。

 

 




