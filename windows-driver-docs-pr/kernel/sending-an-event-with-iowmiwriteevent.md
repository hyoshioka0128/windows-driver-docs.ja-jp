---
title: IoWMIWriteEvent イベントでのイベントの送信
description: IoWMIWriteEvent イベントでのイベントの送信
ms.assetid: 77c1041a-340c-4c59-a30a-e946adf60a95
keywords:
- WMI WDK カーネル、イベント追跡
- イベント WDK WMI
- WDK WMI のトレース
- WMI イベントの送信
- イベントブロック WDK WMI
- 通知 WDK WMI
- IoWMIWriteEvent
- 動的インスタンス名 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91a3be7e12a573646a8e038f57cc02fd1b1bf8c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836363"
---
# <a name="sending-an-event-with-iowmiwriteevent"></a>IoWMIWriteEvent イベントでのイベントの送信





ドライバーは、 [**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)を呼び出して任意のイベントを送信できます。 イベントは、単一の項目、単一のインスタンス、またはデータブロックのすべてのインスタンスで構成され、動的なインスタンス名を使用できます。

WMI によって割り当てられ、部分的に初期化されるクエリまたは変更要求で渡される**wnode\_* xxx*** 構造とは異なり、ドライバーは、 **wnode\_* xxx*** 構造体のすべてのメンバーを割り当て、初期化する必要があります。場合.

ドライバーは、WMI によって IRP\_送信された後にのみイベントを送信する必要があります。この場合、イベントを有効にするための[ **\_イベント要求\_有効**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)にします。 次に、イベントのトリガー条件が発生すると、ドライバーは次のようになります。

1. 非ページプールからバッファーを割り当てて、イベントに必要な**Wnode\_* XXX*** 構造を格納します。これには、変数データの領域 (存在する場合) が含まれます。

   イベントによっては、ドライバーは[**wnode\_単一の\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)、 [**wnode\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)、またはイベントの[**すべての\_データ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)の wnode を割り当てます。 **Wnode\_* XXX*** と変数データのサイズは、レジストリ定義の制限である1k を超えることはできません。

2. Wnodeheader を含む**Wnode\_* XXX*** 構造体のすべてのメンバーを初期化**します。 Flags**:

   - このドライバーは、構造体がイベントであることを示すために、 **Wnode\_フラグ\_イベント\_項目**フラグを設定します。

   - ドライバーは、 **Wnode\_* XXX*** 構造体の種類を示すために、次のいずれかのフラグを設定します。

     **WNODE\_フラグ\_すべての\_データ**

     **WNODE\_フラグ\_単一\_インスタンス**

     **WNODE\_フラグ\_単一の\_項目**

   - ドライバーは、ブロックで静的または動的なインスタンス名が使用されているかどうかを示すために、次のフラグを設定またはクリアします。

     **WNODE\_フラグ\_静的\_インスタンス\_名**

     **WNODE\_フラグ\_PDO\_インスタンス\_名**

   - ドライバーは、イベントに応じて追加のフラグを設定することがあります。

3. **Wnode\_* XXX*** へのポインターを、PWNODE\_イベント\_項目にキャストします。

4. ポインターを使用して**IoWMIWriteEvent**を呼び出します。

   **IoWMIWriteEvent**が正常に完了した場合、WMI はイベントに対してドライバーで割り当てられたメモリを解放します。

[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)が返された後、ドライバーは、イベントのトリガー条件の監視を再開し、トリガーの条件が発生するたびにイベントを送信します。これにより、\_WMI は、\_のイベント要求を[ **\_無効**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)にします。そのイベントを無効にします。

イベントのサイズがレジストリで定義されている最大値 1K (推奨されません) を超える場合、ドライバーは[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference) **IoWmiWriteEvent**を呼び出す必要があります。これは、イベントの GUID、サイズ、およびインスタンスインデックス (静的インスタンス名の場合) または名前 (動的インスタンス名の場合)。 WMI は、 **Wnode\_イベント\_リファレンス**の情報を使用して、イベントのクエリを実行します。

ドライバーは、動的なインスタンス名を使用せず、WMI ライブラリルーチン[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)を呼び出すことによって1つのインスタンスで構成されるイベントを送信できます。 **WmiFireEvent**呼び出しに対して、 **wnode\_* XXX*** 構造体を割り当てて初期化する必要はありません。 WMI は、 [**Wnode\_1 つの\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)にドライバーのイベントデータをパッケージ化し、データコンシューマーに配信します。 **WmiFireEvent**を使用してイベントを送信する方法の詳細については、「 [WmiFireEvent を使用](sending-an-event-with-wmifireevent.md)したイベントの送信」を参照してください。

 

 




