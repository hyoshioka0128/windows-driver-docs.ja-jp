---
title: PCI デバイス構成領域へのアクセス
description: PCI デバイス構成領域へのアクセス
ms.assetid: 05e0ada9-d465-4787-abc5-469a75352ee0
keywords:
- 構成領域 WDK の PCI バス
- 領域 WDK バスの構成
- IRP_MN_READ_CONFIG
- IRP_MN_WRITE_CONFIG
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65d7ced2c053cea016b909171b0250e8fe7dd4fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366127"
---
# <a name="accessing-pci-device-configuration-space"></a>PCI デバイス構成領域へのアクセス


デバイスの機能のドライバーでは、周辺機器のコンポーネントの相互接続 (PCI) デバイスの操作の一部は予約されます。 このような操作などが、バスのデバイスに固有の構成領域にアクセスして、ダイレクト メモリ アクセス (DMA) コント ローラーをプログラミングします。 マイクロソフトは、2 つの方法で PCI デバイスの構成領域にアクセスするためのシステムのサポートを提供します。

-   [ **BUS\_インターフェイス\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff540707)バスのインターフェイス

-   構成の I/O 要求パケット (Irp) [ **IRP\_MN\_読み取り\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)と[ **IRP\_MN\_書き込み\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff551769)

Windows XP と Windows Server 2003 以降のオペレーティング システムで定義されている構成領域のヘッダーを排他的に制御がある、 *PCI ローカル バス*とすべての機能で機能仕様リンクのリスト。 ドライバーは、これらのレジスタを変更する必要がありますしません。

ただし、ドライバーは、ヘッダーまたはベンダー定義な IRP を使用して、機能の一覧に属していない構成領域に書き込むことができます\_MN\_書き込み\_構成の要求または**SetBusData**メソッド バスの\_インターフェイス\_標準。 ドライバーは IRP を使用して、デバイスの機能を読み取ることができますも\_MN\_読み取り\_構成の要求または**GetBusData**メソッド バスの\_インターフェイス\_標準。 IRP を使用する\_MN\_読み取り\_構成または IRP\_MN\_書き込み\_構成では、ドライバーは、パッシブで実行する必要があります\_レベル。 機能とドライバーを照会している対応する構造については、次を参照してください。、 [PCI 構造](https://msdn.microsoft.com/library/windows/hardware/ff537590)セクション。

ドライバーが拡張 PCI デバイス構成領域から読み取ることができます (つまり、複数の構成データの 256 バイト)、IRP を使用して\_MN\_読み取り\_構成の要求または**GetBusData**のメソッドバス\_インターフェイス\_標準。 同様に、ドライバーは IRP を使用して拡張 PCI デバイス構成領域に記述できます\_MN\_書き込み\_構成の要求または**SetBusData**メソッド バスの\_インターフェイス\_標準です。 デバイスには、拡張の構成領域がないか、プラットフォームがデバイスで、拡張の構成領域のパスを定義していない場合、0 xffff および書き込み要求は影響しません、読み取り要求を返します。 操作が成功したかを判断、ドライバーは、読み取りまたは書き込みバイト数を調べることができます。

PCI Express および PCI X モード 2 の 256 バイトより大きい拡張 PCI デバイスの構成領域をサポートします。 ドライバーは、読み取りし、書き込みでは、適切なハードウェアと BIOS サポートのみが、この構成領域に。 ACPI BIOS 内でルート バスに PNP0A08 または PNP0A03 のいずれかの PNP ID が必要です。 ルートのバス PNP0A03 の PNP ID と、\_関数 4 DSM メソッドは、現在のモードが PCI X モード 2 を示す必要があります。 すべてのブリッジとデバイスする必要がありますか、pci express または PCI X モード 2 で動作します。

さらに、システムでは、構成のメモリ マップ領域のアクセスをサポートする必要があります。 システム/の BIOS ファームウェアで、MCFG テーブルを定義することになります。 Windows Vista および Windows Server 2008 以降のオペレーティング システムは自動的に構成のメモリ マップ領域のアクセスをサポートします。

次のコード例では、デバイスの電源管理機能のデータに対してクエリを実行する方法を示します。

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

 

 




