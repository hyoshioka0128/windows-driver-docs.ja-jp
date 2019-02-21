---
title: MSI X を動的に構成します。
description: MSI X を動的に構成します。
ms.assetid: 53051239-e00f-41e8-b95d-9618693e696d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 564c18d512d23ab7372d7ab089e570b47ea7658a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530702"
---
# <a name="dynamically-configuring-msi-x"></a>MSI X を動的に構成します。


Windows Vista Service Pack 1 (SP1)、Windows Server 2008、および以降のオペレーティング システムは、MSI X 割り込みメッセージのプロパティを動的に変更をサポートします。 (PCI 3.0 の仕様には、MSI X が定義されている)。GUID を公開、PCI バス ドライバー\_MSIX\_テーブル\_CONFIG\_バス ハードウェア割り込みの表の設定を変更する PCI デバイス用のドライバーを許可するインターフェイス。

ドライバー インターフェイスを使用して送信することによって、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687) 、バス ドライバーへの要求、 *InterfaceType*パラメーターの GUID と等しく\_MSIX\_テーブル\_CONFIG\_インターフェイス。 バス ドライバーへのポインターを提供する、 [ **PCI\_MSIX\_テーブル\_CONFIG\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff558787)構造体は、次の 3 つのルーチンへのポインターを提供します。割り込みテーブルを変更するには。

-   [*SetTableEntry* ](https://msdn.microsoft.com/library/windows/hardware/gg604857)ハードウェア テーブル エントリにメッセージ ID を割り当てます。

-   [*MaskTableEntry* ](https://msdn.microsoft.com/library/windows/hardware/gg604852)ハードウェア テーブル エントリに対応する割り込みをマスクします。

-   [*UnmaskTableEntry* ](https://msdn.microsoft.com/library/windows/hardware/gg604859)ハードウェア テーブル エントリに対応する割り込みに対してマスクを解除します。

既定では、割り込みテーブルが最初のエントリがある 0 のメッセージ ID を持つように構成されている、2 番目のエントリが 1 つは、メッセージ ID となどです。 テーブル エントリの数は、メッセージの数を超えている場合、その他のテーブルの各エントリにはメッセージ ID 0 が割り当てられます。 (メッセージ ID は、割り込みのエントリのインデックス、 **MessageInfo**のメンバー、 [ **IO\_割り込み\_メッセージ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550576)ドライバーのメッセージ シグナル割り込みを記述する構造体。 [ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)ルーチンは、この構造体へのポインターを提供します)。

 

 




