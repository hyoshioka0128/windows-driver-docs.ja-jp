---
title: PCI デバイス構成領域へのアクセス
description: PCI デバイス構成領域へのアクセス
ms.assetid: 05e0ada9-d465-4787-abc5-469a75352ee0
keywords:
- PCI 構成領域 WDK バス
- 構成領域の WDK バス
- IRP_MN_READ_CONFIG
- IRP_MN_WRITE_CONFIG
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6dddd28faeddcb591bc4ee1218c4008b59e2fea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837733"
---
# <a name="accessing-pci-device-configuration-space"></a>PCI デバイス構成領域へのアクセス


周辺コンポーネントインターコネクト (PCI) デバイス上の一部の操作は、デバイスの関数ドライバー用に予約されています。 このような操作には、たとえば、バスのデバイス固有の構成領域へのアクセスや、ダイレクトメモリアクセス (DMA) コントローラーのプログラミングなどがあります。 Microsoft では、次の2つの方法で PCI デバイスの構成領域にアクセスするためのシステムサポートを提供しています。

-   [**バス\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)バスインターフェイス

-   構成 i/o 要求パケット (Irp)、 [**irp\_、\_読み取り\_構成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)と[**irp\_、\_構成の書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)\_

Windows XP および Windows Server 2003 以降のオペレーティングシステムでは、 *PCI ローカルバス*仕様で定義されているように、構成領域のヘッダー、および機能のリンクリストのすべての機能が排他的に制御されています。 ドライバーは、これらのレジスタを変更しないようにする必要があります。

ただし、ドライバーは、ヘッダーに属していない構成領域またはベンダー定義の機能リストに書き込むことができます。これを行うには、IRP\_\_書き込み\_CONFIG 要求またはバスの**Setbusdata**メソッドを使用\_INTERFACE\_STANDARD。 また、ドライバーは、IRP\_\_読み取り\_構成要求またはバス\_\_インターフェイスの**Getbusdata**メソッドを使用して、デバイスの機能を読み取ることもできます。 IRP\_を使用するには、\_CONFIG または IRP\_\_読み取り\_構成\_を使用して、ドライバーをパッシブ\_レベルで実行する必要があります。 ドライバーがクエリを実行できる機能とそれに対応する構造の一覧については、「 [PCI 構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」セクションを参照してください。

ドライバーは、IRP\_\_読み取り\_構成要求またはバス\_インターフェイスの**Getbusdata**メソッドを使用して、拡張された PCI デバイス構成領域 (つまり、構成データの256バイト以上) から読み取ることができ\_規格. 同様に、ドライバーは、IRP\_\_書き込み\_CONFIG 要求またはバス\_インターフェイス\_標準の**Setbusdata**メソッドを使用して、拡張 PCI デバイス構成領域に書き込むことができます。 デバイスに拡張された構成領域がない場合、またはプラットフォームがデバイスの拡張構成領域のパスを定義していない場合、読み取り要求は0xFFFF を返し、書き込み要求は無効になります。 操作が成功したかどうかを判断するために、ドライバーは、読み取りまたは書き込みのバイト数を調べることができます。

PCI Express と PCI X モード2では、256バイトを超える拡張 PCI デバイス構成領域がサポートされます。 ドライバーは、この構成領域に対して読み取りと書き込みを行うことができますが、適切なハードウェアと BIOS をサポートしている必要があります。 ACPI BIOS では、ルートバスの PNP ID は PNP0A08 または PNP0A03 のいずれかである必要があります。 PNP ID が PNP0A03 のルートバスの場合、\_DSM メソッド (関数 4) は、現在のモードが PCI X モード2であることを示す必要があります。 すべてのブリッジとデバイスは、PCI express であるか、または PCI X モード2で動作している必要があります。

また、システムでは、メモリマップトの構成領域へのアクセスをサポートする必要があります。 これは、システムの BIOS/ファームウェアで MCFG テーブルを定義することによって行います。 Windows Vista および Windows Server 2008 以降のオペレーティングシステムでは、メモリマップトの構成領域へのアクセスが自動的にサポートされます。

次のコード例は、デバイスの電源管理機能データを照会する方法を示しています。

```cpp
#define LSZ sizeof(ULONG)
#define HEADERSIZE (FIELD_OFFSET (PCI_COMMON_CONFIG, DeviceSpecific)) / LSZ

 // The PCI_COMMON_CONFIG structure includes 
// device specific data. The following
// structure is used to retrieve the
// 64 bytes of data that precedes the
// device-specific data.

typedef struct {
    ULONG  Reserved[HEADERSIZE];
} PCI_COMMON_HEADER, *PPCI_COMMON_HEADER;

PCI_COMMON_HEADER Header;
PCI_COMMON_CONFIG *pPciConfig = (PCI_COMMON_CONFIG *)&Header;
// declare power management capabilities header
 PCI_PM_CAPABILITY  PowerMgmtCapability;
PCI_PM_CAPABILITY  *pPowerMgmtCapability = &Capability; 
UCHAR CapabilityOffset;

// Read the first part of the header
// to get the status register and
// the capabilities pointer.
// The "capabilities pointer" is
// actually an offset from the
// beginning of the header to a
// linked list of capabilities.
BusInterface.GetBusData(Context,
    PCI_WHICHSPACE_CONFIG,
    pPciConfig, // output buffer
    0, // offset of the capability to read
 sizeof(PCI_COMMON_HEADER)); // just 64 bytes

// Check the Status register to see if 
// this device supports capability lists.
 
if ((pPciConfig->Status &
   PCI_STATUS_CAPABILITIES_LIST) == 0) {
   // does not support capabilities list
   return(STATUS_NOT_IMPLEMENTED);
}

// The device supports capability lists.
// Find the capabilities.

// The position of the capabilities pointer
// in the header depends on whether this is 
// a bridge type device. Check the type.

if ((pPciConfig->HeaderType & 
   (~PCI_MULTIFUNCTION)) == PCI_BRIDGE_TYPE) {
   CapabilityOffset = 
       pPciConfig->u.type1.CapabilitiesPtr;
} else if ((pPciConfig->HeaderType & 
   (~PCI_MULTIFUNCTION)) == PCI_CARDBUS_TYPE) {
   CapabilityOffset = 
       pPciConfig->u.type2.CapabilitiesPtr;
} else {
   CapabilityOffset = 
       pPciConfig->u.type0.CapabilitiesPtr;
}

// Loop through the capabilities in search
// of the power management capability. The
// list is NULL-terminated, so the last 
// offset will always be zero.

while (CapabilityOffset != 0) {

    // Read the header of the capability at 
    // this offset.

    // If the retrieved capability is not
    // the power management capability that
    // we are looking for, follow the
    // link to the next capability and
    // continue looping.

    BusInterface.GetBusData(Context,
        PCI_WHICHSPACE_CONFIG,
        pPowerMgmtCapability,
        CapabilityOffset,
        sizeof(PCI_CAPABILITIES_HEADER));

    if (Capability->Header.CapabilityID ==
 PCI_CAPABILITY_ID_POWER_MANAGEMENT) {
        // Found the power management capability
        break;
    } else {
        // This is some other capability.
        // Keep looking for the power 
        // management capability.
        CapabilityOffset = Capability->Header.Next;
    }
}

if (CapabilityOffset == 0) {
    // We didn't find a power management
    // capability. Return an error.
    return(STATUS_NOT_IMPLEMENTED);
}

// Skip past the capabilities header and read
// the rest of the power management capability

BusInterface.GetBusData(Context,
   PCI_WHICHSPACE_CONFIG,
   // write to location immediately following header
   & (pPowerMgmtCapability->Header) + 1, 
   CapabilityOffset + 
       sizeof(PCI_CAPABILITIES_HEADER),
   sizeof(PCI_PM_CAPABILITY) - 
       sizeof(PCI_CAPABILITIES_HEADER)
);
```

 

 




