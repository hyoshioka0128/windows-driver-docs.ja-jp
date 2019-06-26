---
title: MSI-X の動的な構成
description: MSI-X の動的な構成
ms.assetid: 53051239-e00f-41e8-b95d-9618693e696d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a187a3ae798a3d42cb49668bc1c224ec9feb2fbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384949"
---
# <a name="dynamically-configuring-msi-x"></a>MSI-X の動的な構成


Windows Vista Service Pack 1 (SP1)、Windows Server 2008、および以降のオペレーティング システムは、MSI X 割り込みメッセージのプロパティを動的に変更をサポートします。 (PCI 3.0 の仕様には、MSI X が定義されている)。GUID を公開、PCI バス ドライバー\_MSIX\_テーブル\_CONFIG\_バス ハードウェア割り込みの表の設定を変更する PCI デバイス用のドライバーを許可するインターフェイス。

ドライバー インターフェイスを使用して送信することによって、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) 、バス ドライバーへの要求、 *InterfaceType*パラメーターの GUID と等しく\_MSIX\_テーブル\_CONFIG\_インターフェイス。 バス ドライバーへのポインターを提供する、 [ **PCI\_MSIX\_テーブル\_CONFIG\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pci_msix_table_config_interface)構造体は、次の 3 つのルーチンへのポインターを提供します。割り込みテーブルを変更するには。

-   [*SetTableEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pci_msix_set_entry)ハードウェア テーブル エントリにメッセージ ID を割り当てます。

-   [*MaskTableEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pci_msix_maskunmask_entry)ハードウェア テーブル エントリに対応する割り込みをマスクします。

-   [*UnmaskTableEntry* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/gg604859(v=vs.85))ハードウェア テーブル エントリに対応する割り込みに対してマスクを解除します。

既定では、割り込みテーブルが最初のエントリがある 0 のメッセージ ID を持つように構成されている、2 番目のエントリが 1 つは、メッセージ ID となどです。 テーブル エントリの数は、メッセージの数を超えている場合、その他のテーブルの各エントリにはメッセージ ID 0 が割り当てられます。 (メッセージ ID は、割り込みのエントリのインデックス、 **MessageInfo**のメンバー、 [ **IO\_割り込み\_メッセージ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_interrupt_message_info)ドライバーのメッセージ シグナル割り込みを記述する構造体。 [ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)ルーチンは、この構造体へのポインターを提供します)。

 

 




