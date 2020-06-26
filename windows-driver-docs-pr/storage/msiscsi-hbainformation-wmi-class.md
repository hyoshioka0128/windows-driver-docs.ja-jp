---
title: MSiSCSI \_ hbainformation WMI クラス
description: MSiSCSI \_ hbainformation WMI クラス
ms.assetid: 24c44f97-5ff3-46fa-a5bf-aa76f7f0d3f2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6f7daf125f456105ae9f299ce05ebeec1efce205
ms.sourcegitcommit: df7d6565a4cd2659c46d5fd83ef04a1672c60dbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382729"
---
# <a name="msiscsi_hbainformation-wmi-class"></a>MSiSCSI_HBAInformation WMI クラス

ISCSI イニシエーターサービスは、MSiSCSI_HBAInformation WMI クラスを使用してアダプターと通信します。 読み込まれるミニポートドライバーのインスタンスごとに、このクラスの個別のインスタンスを用意する必要があります。

このクラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI_HBAInformation クラスは、*管理 .mof*で次のように定義されています。

```cpp
class MSiSCSI_HBAInformation {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), DisplayName("Adapter Id") : amended,
    DisplayInHex, description("Id that is globally unique to
    each instance of each adapter. Using the address of the
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(2), DisplayName("Integrated Networking") :
    amended, description("TRUE if TCP/IP traffic is
    integrated with the Windows networking TCP/IP stack via
    a software only initiator") : amended]
    boolean  IntegratedTCPIP;
  [WmiDataId(3), Displayname("Requires Binary Addresses") :
    amended, description("TRUE if HBA requires binary ip
    addresses. If unchecked then DNS must be available on
    HBA.") : amended]
    boolean  RequiresBinaryIpAddresses;
  [read, WmiDataId(4), DisplayName("Minimum iSCSI
    Version")
    : amended, description("Minimum version number of the
    iScsi spec supported by HBA") : amended]
    uint8  VersionMin;
  [read, WmiDataId(5), DisplayName("Maximum iSCSI
    Version")
    : amended, description("Maximum version number of the
    iSCSI spec supported by HBA") : amended]
    uint8  VersionMax;
  [read, WmiDataId(6), DisplayName("Multifunction Device") :
    amended, description("TRUE if this adapter is a
    multifunction device, that is it also exposes a netcard
    interface") : amended]
    boolean  MultifunctionDevice;
  [read, WmiDataId(7), DisplayName("Valid Cache") : amended,
    description("TRUE if the adapter caches are valid") :
    amended] boolean  CacheValid;
  [read, WmiDataId(8), Displayname("Number of ports") :
    amended, description("Number of ports attached to HBA")
    : amended] uint32  NumberOfPorts;
  [read, WmiDataId(9), Displayname("Status") : amended,
    description("Current status of HBA") : amended,
    Values{ "Working", "Degraded", "Critical", "Failed"},
    ValueMap{ "0",     "1",        "2",        "3" },
    cpp_quote(
    "#define ISCSI_HBA_STATUS_WORKING           0\n"
    "#define ISCSI_HBA_STATUS_DEGRADED          1\n"
    "#define ISCSI_HBA_STATUS_CRITICAL          2\n"
    "#define ISCSI_HBA_STATUS_FAILED            3\n"
    )] uint32  Status;
  [read, WmiDataId(10), DisplayName("Functionality
    Supported") : amended, Description("Bit flags that
    indicate various functionality supported") : amended,
    BitValueMap{"0x00000001",
                "0x00000002",
                "0x00000004",
                "0x00000008",
                "0x00000010",
                "0x00000020"
                },
    BitValues{"Preshared Key Cache",
              "iSCSI Authentication Cache",
              "Tunnel Mode",
              "CHAP authentication via RADIUS",
              "Discovery via iSNS",
              "Discovery via SLP"
              } : amended,
    cpp_quote(
    "\n"
    "//\n"
    "// Flags that define the functionality
    supported by the HBA\n"
    "//\n"
    "#define ISCSI_HBA_PRESHARED_KEY_CACHE  0x00000001\n"
    "#define ISCSI_HBA_ISCSI_AUTHENTICATION_CACHE
     x00000002\n"
    "#define ISCSI_HBA_IPSEC_TUNNEL_MODE    0x00000004\n"
    "#define ISCSI_HBA_CHAP_VIA_RADIUS      0x00000008\n"
    "#define ISCSI_HBA_ISNS_DISCOVERY       0x00000010\n"
    "#define ISCSI_HBA_SLP_DISCOVERY        0x00000020\n"
    "\n")]
    uint32  FunctionalitySupported;
  [read, WmiDataId(11), DisplayName("Generational Guid") :
    amended, Description("Generational Guid") : amended]
    uint8  GenerationalGuid[16];
  [read, WmiDataId(12), DisplayName("Max CDB Length") :
    amended, Description("Max CDB Length") : amended]
    uint32  MaxCDBLength;
  [read, WmiDataId(13), DisplayName("Bi-directional SCSI
    command supported") : amended, Description("Bi-
    directional SCSI command supported") : amended]
    boolean  BiDiScsiCommands;
  [read, WmiDataId(14), DisplayName("Manufacturer") :
    amended, description("A text string describing the
    manufacturer of HBA") : amended, MaxLen(255)]
    string  VendorID;
  [read, WmiDataId(15), Displayname("Model") : amended,
    description("A text string set by the manufacturer
    describing the model of HBA") : amended, MaxLen(255)]
    string  VendorModel;
  [read, WmiDataId(16), Displayname("Version") : amended,
    description("A text string set by the manufacturer
    describing the version of HBA") : amended, MaxLen(255)]
    string  VendorVersion;
  [read, WmiDataId(17), displayName("Firmware Version") :
    amended, description("A text string set by the
    manufacturer describing the firmware version of HBA") : amended, MaxLen(255)]
    string  FirmwareVersion;
  [read, WmiDataId(18), displayName("ASIC Version") :
    amended, description("A text string set by the
    manufacturer describing the firmware version of HBA") :
    amended, MaxLen(255)]
    string  AsicVersion;
  [read, WmiDataId(19), displayName("Option Rom Version") :
  amended, description("A text string set by the
  manufacturer describing the option rom version of HBA")
  : amended, MaxLen(255)]
  string  OptionRomVersion;
  [read, WmiDataId(20), Displayname("Serial Number") :
    amended, description("A text string set by the
    manufacturer describing the serial number of HBA") :
    amended, MaxLen(255)]
    string  SerialNumber;
  [read, WmiDataId(21), Displayname("Driver Name") :
    amended, description("A text string specifying the name
    of the driver for the HBA") : amended, MaxLen(255)]
    string  DriverName;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi \_ hbainformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_hbainformation)データ構造を生成します。
