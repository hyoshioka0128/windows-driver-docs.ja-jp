---
title: Bluetooth インターフェイスの照会
description: Bluetooth インターフェイスの照会
ms.assetid: 56db29cd-26ab-4262-9b9f-40d46372ffe9
keywords:
- Bluetooth WDK, インターフェイスクエリ
- Bluetooth インターフェイスのクエリ
- インターフェイス WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d988c24da7e532ff37f441dd2a87be21418430a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837541"
---
# <a name="querying-for-bluetooth-interfaces"></a>Bluetooth インターフェイスの照会


Bluetooth ドライバースタックは、プロファイルドライバーが Bluetooth デバイスと対話するために使用できる次のインターフェイスを公開します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インターフェイス</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GUID_BTHDDI_SDP_NODE_INTERFACE</p></td>
<td align="left"><p>プロファイルドライバーのクエリを使用して GUID_BTHDDI_SDP_NODE_INTERFACE、サービス検出プロトコル (SDP) レコードを作成する関数へのポインターを取得します。</p>
<p>このインターフェイスは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_NODE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)"><strong>BTHDDI_SDP_NODE_INTERFACE</strong></a>構造体に対応します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID_BTHDDI_SDP_PARSE_INTERFACE</p></td>
<td align="left"><p>GUID_BTHDDI_SDP_PARSE_INTERFACE のプロファイルドライバークエリを使用して、SDP レコードを解析できるようにする関数へのポインターを取得します。</p>
<p>このインターフェイスは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_PARSE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)"><strong>BTHDDI_SDP_PARSE_INTERFACE</strong></a>構造体に対応します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GUID_BTHDDI_PROFILE_DRIVER_INTERFACE</p></td>
<td align="left"><p>プロファイルドライバーのクエリを使用して、BTHDDI_PROFILE_DRIVER_INTERFACE を作成、割り当て、再利用、および解放するための関数へのポインターを取得します。</p>
<p>このインターフェイスは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_bth_profile_driver_interface" data-raw-source="[&lt;strong&gt;BTH_PROFILE_DRIVER_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_bth_profile_driver_interface)"><strong>BTH_PROFILE_DRIVER_INTERFACE</strong></a>構造体に対応します。</p></td>
</tr>
</tbody>
</table>

 

これらのインターフェイスのいずれかを取得するには、プロファイルドライバーがまず、Irp\_を作成して、 [ **\_インターフェイスの irp\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)を Bluetooth ドライバースタックに送信する必要があります。

次の手順は、これらのインターフェイスのいずれかを取得する一般的なプロセスです。

### <a name="span-idto_query_for_an_interfacespanspan-idto_query_for_an_interfacespanto-query-for-an-interface"></a><span id="to_query_for_an_interface"></span><span id="TO_QUERY_FOR_AN_INTERFACE"></span>インターフェイスを照会するには

1.  IRP を割り当て、初期化します。

2.  インターフェイスのインスタンスを割り当て、初期化します。

3.  インターフェイスを照会するメジャーおよびマイナー関数コードを指定します。

4.  クエリを実行するインターフェイスを指定します。

5.  処理するドライバースタックを IRP に渡します。

次の擬似コードの例では、IRP\_の\_クエリ\_インターフェイスの IRP を設定して、BTHDDI\_PROFILE\_DRIVER\_インターフェイスの\_GUID の Bluetooth ドライバースタックを照会する方法を示します。

**メモ**  読みやすくするために、次の擬似コード例ではエラー処理を示していません。

 

```cpp
#include <bthddi.h>

...

// Define a custom pool tag to identify your profile driver's dynamic memory allocations. You should change this tag to easily identify your driver's allocations from other drivers.
#define PROFILE_DRIVER_POOL_TAG '_htB'

PIRP Irp;
Irp = IoAllocateIrp( DeviceExtension->ParentDeviceObject->StackSize, FALSE );

PBTH_PROFILE_DRIVER_INTERFACE BthInterface; // Define storage for an instance of the BTH_PROFILE_DRIVER_INTERFACE structure
BthInterface = ExAllocatePoolWithTag( NonPagedPool, sizeof( BTH_PROFILE_DRIVER_INTERFACE ), PROFILE_DRIVER_POOL_TAG );

// Zero the memory associated with the structure
RtlZeroMemory( BthInterface, sizeof( BTH_PROFILE_DRIVER_INTERFACE ) );

// Set up the next IRP stack location
PIO_STACK_LOCATION NextIrpStack;
NextIrpStack = IoGetNextIrpStackLocation( Irp );
NextIrpStack->MajorFunction = IRP_MJ_PNP;
NextIrpStack->MinorFunction = IRP_MN_QUERY_INTERFACE;
NextIrpStack->Parameters.QueryInterface.InterfaceType = (LPGUID) &GUID_BTHDDI_PROFILE_DRIVER_INTERFACE;
NextIrpStack->Parameters.QueryInterface.Size = sizeof( BTH_PROFILE_DRIVER_INTERFACE );
NextIrpStack->Parameters.QueryInterface.Version = BTHDDI_PROFILE_DRIVER_INTERFACE_VERSION_FOR_QI;
NextIrpStack->Parameters.QueryInterface.Interface = (PINTERFACE) BthInterface;
NextIrpStack->Parameters.QueryInterface.InterfaceSpecificData = NULL;

// Pass the IRP down the driver stack
NTSTATUS Status;
Status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
```

IRP が正常に返された場合、プロファイルドライバーは、インターフェイスに含まれている関数ポインターにアクセスして使用できます。

 

 





