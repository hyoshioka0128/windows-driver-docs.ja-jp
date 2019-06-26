---
title: Bluetooth インターフェイスの照会
description: Bluetooth インターフェイスの照会
ms.assetid: 56db29cd-26ab-4262-9b9f-40d46372ffe9
keywords:
- Bluetooth の WDK、インターフェイスのクエリ
- Bluetooth のインターフェイスのクエリを実行します。
- WDK Bluetooth インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e80cd3d00cb30abf85ab3aaffcc4ff9418447fa3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354001"
---
# <a name="querying-for-bluetooth-interfaces"></a>Bluetooth インターフェイスの照会


Bluetooth ドライバー スタックは、プロファイルのドライバーは、Bluetooth デバイスとの対話に使用できる次のインターフェイスを公開します。

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
<td align="left"><p>プロファイル サービスの探索プロトコル (SDP) レコードを作成できるようにする関数へのポインターを取得する GUID_BTHDDI_SDP_NODE_INTERFACE に対するクエリをドライバー。</p>
<p>このインターフェイスに対応する、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_NODE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)"> <strong>BTHDDI_SDP_NODE_INTERFACE</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID_BTHDDI_SDP_PARSE_INTERFACE</p></td>
<td align="left"><p>SDP レコードを解析できるようにする関数へのポインターを取得する GUID_BTHDDI_SDP_PARSE_INTERFACE のプロファイル ドライバー クエリ。</p>
<p>このインターフェイスに対応する、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_PARSE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)"> <strong>BTHDDI_SDP_PARSE_INTERFACE</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GUID_BTHDDI_PROFILE_DRIVER_INTERFACE</p></td>
<td align="left"><p>プロファイル ドライバーのクエリを作成できるようにする関数へのポインターを取得する BTHDDI_PROFILE_DRIVER_INTERFACE は、割り当て、再利用、および、BRBs を解放します。</p>
<p>このインターフェイスに対応する、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_bth_profile_driver_interface" data-raw-source="[&lt;strong&gt;BTH_PROFILE_DRIVER_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_bth_profile_driver_interface)"> <strong>BTH_PROFILE_DRIVER_INTERFACE</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

これらのインターフェイスを取得するプロファイル ドライバー最初をビルドして送信、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IRP Bluetooth ドライバー スタックにします。

次の手順は、これらのインターフェイスのいずれかを取得する一般的なプロセスです。

### <a name="span-idtoqueryforaninterfacespanspan-idtoqueryforaninterfacespanto-query-for-an-interface"></a><span id="to_query_for_an_interface"></span><span id="TO_QUERY_FOR_AN_INTERFACE"></span>インターフェイスを照会するには

1.  割り当ておよび IRP を初期化します。

2.  割り当てし、インターフェイスのインスタンスを初期化します。

3.  インターフェイスを照会するメジャーおよびマイナーの関数コードを指定します。

4.  照会するインターフェイスを指定します。

5.  IRP がドライバー スタックを処理するを渡します。

次の擬似コード例は IRP を設定する方法を示します\_MN\_クエリ\_GUID、Bluetooth ドライバー スタックを照会するインターフェイスの IRP\_BTHDDI\_プロファイル\_ドライバー\_インターフェイス。

**注**  読みやすくするために、次の擬似コードの例では示しませんエラー処理します。

 

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

IRP が正常に返された場合プロファイル ドライバーにアクセスし、インターフェイスに含まれている関数ポインターを使用します。

 

 





