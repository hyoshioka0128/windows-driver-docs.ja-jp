---
title: リソース競合の確認
description: リソース競合の確認
ms.assetid: c994085c-8610-487f-88a5-f11b4a68ec4a
keywords:
- プラグ アンド プレイ (PnP)、リソースの競合
- リソースの競合
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8453c2869b98e8bc5dd6a8324944d1dcf2782a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531569"
---
# <a name="checking-for-resource-conflicts"></a>リソース競合の確認


## <span id="ddk_checking_for_resource_conflicts_dbg"></span><span id="DDK_CHECKING_FOR_RESOURCE_CONFLICTS_DBG"></span>


このセクションでは、リソースの競合を検出するために使用できる手法について説明します。

最初の手法では、監視データをダンプする必要があります。 次の例では、I/O の範囲内の監視データが調べられます。

```dbgcmd
kd> !arbiter 1

DEVNODE ff0daf48
  Port Arbiter "RootPort" at 8045b920
    Allocated ranges:
      10 - 1f S         Owner ff0d6b30
      22 - 3f S         Owner ff0d6b30
      44 - 47 S         Owner ff0d6b30
      4c - 6f S         Owner ff0d6b30
      72 - 7f S         Owner ff0d6b30
      90 - 91 S         Owner ff0d6b30
      93 - 9f S         Owner ff0d6b30
      a2 - bf S         Owner ff0d6b30
      d0 - ef S         Owner ff0d6b30
      100 - 2f7 S       Owner ff0d6b30
      300 - cf7 S       Owner ff0d6b30
      d00 - ffff S      Owner ff0d6b30
    Possible allocation:
      < none >

    DEVNODE ff0d2e28 (PCI_HAL\PNP0A03\0)
      Port Arbiter "PCI I/O Port (b=00)" at e122c2c8
        Allocated ranges:
          0 - f         Owner 00000000
          20 - 21       Owner 00000000
          40 - 43       Owner 00000000
          48 - 4b       Owner 00000000
          60 - 60       Owner ff0d4030
          64 - 64       Owner ff0d4030
          70 - 71       Owner 00000000
          80 - 8f       Owner 00000000
          92 - 92       Owner 00000000
          a0 - a1       Owner 00000000
          c0 - cf       Owner 00000000
          f0 - ff       Owner 00000000
          170 - 177     Owner ff0cf030
          1ce - 1cf S   Owner ff040040
          2f8 - 2ff     Owner 00000000
          376 - 376     Owner ff0cf030
          378 - 37f     Owner ff0d4e70
          3b0 - 3bb S   Owner ff040040
 3c0 - 3cf S   Owner ff0bb900
          3c0 - 3df S   Owner ff040040
          3d4 - 3db S   Owner ff0bb900
          3de - 3df S   Owner ff0bb900
 3ec - 3ef     Owner ff0d0b50 (This device conflicts with another device, see below)
          3f2 - 3f5     Owner ff0d4770
          3f7 - 3f7 S   Owner ff0d4770
          3f8 - 3ff     Owner ff0d4af0
          778 - 77b     Owner ff0d4e70
          cf8 - cff     Owner 00000000
          1000 - 10ff           Owner ff0d1030
          1400 - 140f           Owner ff0d1d30
          1410 - 141f           Owner ff0d1890
          10000 - ffffffffffffffff      Owner 00000000
        Possible allocation:
          < none >
```

2 つの仲裁があることに注意してください: デバイス ツリーのルートにあるいずれか、もう 1 つ PCI\_HAL。 PCI 決定者の要求し、(0xD000-0 xffff、これは、後で、デバイスの PCI アービターをサブ割り当て) を介し、デバイスの範囲を事前に割り当てることに注意してください。 [所有者] フィールドでは、その範囲を所有するデバイス オブジェクトを示します。 所有者のゼロの値は、範囲がバスにないことを示します。 PCI のブリッジの場合などに合格していないすべての範囲に割り当てられる**NULL**します。

次の例では、PCI ブリッジは、その監視には、次の 2 つの範囲が含まれるように I/O 0xD000 0xDFFFF を渡します。

```text
0-CFFFF            Owner 00000000
E0000-FFFFFFFFFFFFFFFF   Owner 00000000
```

FFFFFFFFFFFFFFFF は調停のすべてのリソースが 64 ビットの範囲として扱われるためにです。

**例:**

```dbgcmd
kd> !devobj ff0bb900

Device object (ff0bb900) is for:
 Video0 \Driver\mga_mil DriverObject ff0bbc10
Current Irp 00000000 RefCount 1 Type 00000023 Flags 0000204c
DevExt ff0bb9b8 DevNode ff0bb808
Device queue is not busy.
kd> !devnode ff0bb808

DevNode 0xff0bb808 for PDO 0xff0bb900 at level 0xffffffff
  Parent 0xff0daf48   Sibling 0000000000   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xffffffff
  TargetDeviceNotify List - f 0xff0bb86c  b 0xff0bb86c
  Flags (0x00000400)  DNF_RESOURCE_REPORTED
kd> !devnode ff0bb808 6

DevNode 0xff0bb808 for PDO 0xff0bb900 at level 0xffffffff
  Parent 0xff0daf48   Sibling 0000000000   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xffffffff
  TargetDeviceNotify List - f 0xff0bb86c  b 0xff0bb86c
  Flags (0x00000400)  DNF_RESOURCE_REPORTED
  CmResourceList at 0xe12474e8  Version 0.0  Interface 0x5  Bus #0
    Entry 0 - Port (0x1) Shared (0x3)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x3c0 for 0x10 bytes
    Entry 1 - Port (0x1) Shared (0x3)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x3d4 for 0x8 bytes
    Entry 2 - Port (0x1) Shared (0x3)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x3de for 0x2 bytes
    Entry 3 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      Range starts at 0x0000000040000000 for 0x4000 bytes
    Entry 4 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      Range starts at 0x0000000040800000 for 0x800000 bytes
```

この例に示すように、この操作は範囲 3 c 0 3cf を所有している従来のビデオ カードを取得します。 同じデバイス オブジェクトが一覧表示 (3de 3df や 3 d 4-3dc) を所有している他の範囲の近くです。 同じ追跡手法を使用して、シリアル ポートで使用されていることを 3f8-3ff の範囲が決定されます。

割り込みを変換する同様の手法が必要です。

```dbgcmd
kd> !arbiter 4

DEVNODE ff0daf48
  Interrupt Arbiter "RootIRQ" at 8045bae0
    Allocated ranges:
      31 - 31           Owner ff0d4030
      34 - 34 S         Owner ff0d4af0
      36 - 36           Owner ff0d4770
      3b - 3b S         Owner ff0d1030
      3b - 3b S         Owner ff0d1d30
      3c - 3c           Owner ff0d3c70
 3f - 3f           Owner ff0cf030
    Possible allocation:
      < none >
```

割り込みの 1 つの監視があることに注意してください。 ルート決定者。

たとえば、IRQ に割り込み 3 f を変換します。 まず、デバイス オブジェクト、devnode をダンプします。

```dbgcmd
kd> !devobj ff0cf030

Device object (ff0cf030) is for:
 IdeFdoff0d0398Channel1 \Driver\IntelIde DriverObject ff0d0530
Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001040AttachedDev ff0cd030

DevExt ff0cf0e8 DevNode ff0cfe88
Device queue is not busy.
kd> !devnode ff0cfe88 6

DevNode 0xff0cfe88 for PDO 0xff0cf030 at level 0x3
  Parent 0xff0d1348   Sibling 0000000000   Child 0xff0c84a8
  InterfaceType 0xffffffff  Bus Number 0xfffffff0
  InstancePath is "PCIIDE\IDEChannel\1&1"
  ServiceName is "atapi"
  TargetDeviceNotify List - f 0xff0cfeec  b 0xff0cfeec
  Flags (0x6000120b)  DNF_PROCESSED, DNF_STARTED,
                      DNF_ENUMERATED, DNF_RESOURCE_ASSIGNED,
                      DNF_ADDED, DNF_HAS_BOOT_CONFIG
                      Unknown flags 0x40000000
  CmResourceList at 0xe12321c8  Version 0.0  Interface 0x1  Bus #0
    Entry 0 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x170 for 0x8 bytes
    Entry 1 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x376 for 0x1 bytes
    Entry 2 - Interrupt (0x2) Device Exclusive (0x1)
      Flags (0x01) - LATCHED
      Level 0xf, Vector 0xf, Affinity 0xffffffff

  IoResList at 0xe12363c8 : Interface 0x1  Bus 0  Slot 0
  Reserved Values = {0x0002e0d0, 0x00920092, 0xe1235508}
    Alternative 0 (Version 1.1)
      Preferred Descriptor 0 - NonArbitrated/ConfigData (0x80) Shared (0x3)
        Flags (0000) -
        Data:              : 0x1 0x61004d 0x680063
      Preferred Descriptor 1 - Port (0x1) Device Exclusive (0x1)
        Flags (0x01) - PORT_IO
        0x000008 byte range with alignment 0x000001
        170 - 0x177
      Preferred Descriptor 2 - Port (0x1) Device Exclusive (0x1)
        Flags (0x01) - PORT_IO
        0x000001 byte range with alignment 0x000001
        376 - 0x376
      Preferred Descriptor 3 - Interrupt (0x2) Device Exclusive (0x1)
        Flags (0x01) - LATCHED
        0xf - 0xf
    Alternative 1 (Version 1.1)
      Preferred Descriptor 0 - Port (0x1) Device Exclusive (0x1)
        Flags (0x01) - PORT_IO
        0x000008 byte range with alignment 0x000001
        170 - 0x177
      Preferred Descriptor 1 - Port (0x1) Device Exclusive (0x1)
        Flags (0x01) - PORT_IO
        0x000001 byte range with alignment 0x000001
        376 - 0x376
      Preferred Descriptor 2 - Interrupt (0x2) Device Exclusive (0x1)
        Flags (0x01) - LATCHED
        0xf - 0xf
```

たとえば、以降では、開始するには、このデバイスの原因となったリソースの競合がないか確認を試行する**devnode**:

```dbgcmd
kd> !devnode 0xff0d4bc8 6

DevNode 0xff0d4bc8 for PDO 0xff0d4cb0 at level 0
  Parent 0xff0daf48   Sibling 0xff0d4a08   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xffffffff
  InstancePath is "Root\*PNP0501\1_0_17_2_0_0"
  ServiceName is "Serial"
  TargetDeviceNotify List - f 0xff0d4c2c  b 0xff0d4c2c
  Flags (0x60001129)  DNF_PROCESSED, DNF_ENUMERATED,
                      DNF_MADEUP, DNF_INSUFFICIENT_RESOURCES,
                      DNF_ADDED, DNF_HAS_BOOT_CONFIG
                      Unknown flags 0x40000000

  IoResList at 0xe1251e28 : Interface 0x1  Bus 0  Slot 0
  Reserved Values = {0x0043005c, 0x006e006f, 0x00720074}
    Alternative 0 (Version 1.1)
      Preferred Descriptor 0 - NonArbitrated/ConfigData (0x80) Undetermined Shar
ing (0)
        Flags (0000) -
        Data:              : 0xc000 0x0 0x0
      Preferred Descriptor 1 - Port (0x1) Undetermined Sharing (0)
        Flags (0x05) - PORT_IO 10_BIT_DECODE
        0x000008 byte range with alignment 0x000001
        3e8 - 0x3ef
      Preferred Descriptor 2 - Interrupt (0x2) Shared (0x3)
        Flags (0x01) - LATCHED
        0x5 - 0x5
    Alternative 1 (Version 1.1)
      Preferred Descriptor 0 - NonArbitrated/ConfigData (0x80) Undetermined Shar
ing (0)
        Flags (0000) -
        Data:              : 0xc000 0x0 0x0
      Preferred Descriptor 1 - Port (0x1) Undetermined Sharing (0)
        Flags (0x05) - PORT_IO 10_BIT_DECODE
        0x000008 byte range with alignment 0x000008
        3e8 - 0x3ef
      Preferred Descriptor 2 - Interrupt (0x2) Shared (0x3)
        Flags (0x01) - LATCHED
        0x5 - 0x5
```

最初に、これは、I/O の競合であると想定し、(前の例を参照してください) 仲裁をダンプします。 0x3EC 0x3EF 範囲が、シリアル デバイスのリソースの要求と重なる 0xFF0D0B50 によって所有されている結果を示しています。 次に、この範囲は、の所有者のデバイス オブジェクトをダンプし、所有者の devnode をダンプします。

```dbgcmd
kd> !devobj ff0d0b50

Device object (ff0d0b50) is for:
 Resource00413e \Driver\isapnp DriverObject ff0d0e10
Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001040
DevExt ff0d0c08 DevNode ff0d0a68
Device queue is not busy.
kd> !devnode ff0d0a68 6

DevNode 0xff0d0a68 for PDO 0xff0d0b50 at level 0xffffffff
  Parent 0xff0daf48   Sibling 0000000000   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xffffffff
Duplicate PDO 0xff0d0e10  TargetDeviceNotify List - f 0xff0d0acc  b 0xff0d0acc
  Flags (0x00000421)  DNF_PROCESSED, DNF_MADEUP,
                      DNF_RESOURCE_REPORTED
  CmResourceList at 0xe1233628  Version 0.0  Interface 0x1  Bus #0
    Entry 0 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x3ec for 0x4 bytes
```

これは、"擬似-devnode"の読み取りデータ ポートの ISAPNP ドライバーによって割り当てられた範囲に対応します。

PnP マネージャーは、デバイスを起動しようとしたときに特定のデバイスに割り当てられているリソースが決定します。

1.  ときに呼び出されるルーチンにブレークポイントを配置 IRP\_MN\_開始\_ドライバーがデバイスの要求を受信します。 (その名前がわかって) 場合、ドライバーのディスパッチ ルーチンにブレークポイントを配置できます。 どちらの場合も、ドライバーとそのシンボルを読み込む必要があります。 これは最初のブレークポイントを設定する必要があります。

    たとえば、PCMCIA のすることができますにブレークポイントを設定**pcmcia! pcmciastartpccard**します。 この特定のルーチンを使用する利点は、2 番目のパラメーターが CM リソースの一覧を使用してダンプできます **! cmreslist** (3 の手順を排除すること)。 PCMCIA 例では、次を参照してください。

2.  関心のあるになっているデバイスを決定する (したがまだ行われていない) 場合は、デバイス オブジェクトをダンプし、CM リソースの一覧で devnode をダンプします。 どのリソースがデバイスに割り当てられていたチェックします。 また、リソース、I/O リソースのリストのサブセットであるかどうかを確認することも可能性があります。 入力**g**または 1 つの手順をステップ実行し、デバイスが開始されたかどうかと、どのリソースが割り当てられていたを決定します。 デバイスが開始するリソースのセットを提供が、これを行うに失敗しました、ドライバーが正しく動作していない (たとえばが正しく宣言されている場合いない実際には使用できませんのリソースのセットを使用できます)。

**例:**

```dbgcmd
ntoskrnl!IopStartDevice:
80420212 55               push    ebp
kd> kb
ChildEBP RetAddr  Args to Child
f64138c0 8048b640 ff0ce870 ff0d7c08 ff0cde88 ntoskrnl!IopStartDevice (!devobj ff0ce870)
f64138f0 8048d8e7 ff0cde88 f6413978 ff0cddc8 ntoskrnl!IopStartAndEnumerateDevice
+0x1a
f6413900 8048de7f ff0cde88 f6413978 ff0cf448 ntoskrnl!IopProcessStartDevicesWork
er+0x43
f6413910 8048d8d5 ff0cf448 8048d8a4 f6413978 ntoskrnl!IopForAllChildDeviceNodes+
0x1f
f6413924 8048de7f ff0cf448 f6413978 ff0d3f48 ntoskrnl!IopProcessStartDevicesWork
er+0x31
f6413934 8048d8d5 ff0d3f48 8048d8a4 f6413978 ntoskrnl!IopForAllChildDeviceNodes+
0x1f
f6413948 8048d893 ff0d3f48 f6413978 e12052e8 ntoskrnl!IopProcessStartDevicesWork
er+0x31
f641395c 804f6f1b ff0d7c08 f6413978 8045c520 ntoskrnl!IopProcessStartDevices+0x1
f
f64139d0 804f5cc1 80088000 f6413aec 8045bba0 ntoskrnl!IopInitializeBootDrivers+0
x2f9
f6413b24 804f4db3 80088000 00000001 00000000 ntoskrnl!IoInitSystem+0x3a6
f6413da8 80447610 80088000 00000000 00000000 ntoskrnl!Phase1Initialization+0x6a3

f6413ddc 8045375a 804f4710 80088000 00000000 ntoskrnl!PspSystemThreadStartup+0x5
4
00000000 00000000 00000000 00000000 00000000 ntoskrnl!KiThreadStartup+0x16
kd> !devobj ff0ce870

Device object (ff0ce870) is for:
 NTPNP_PCI0002 \Driver\PCI DriverObject ff0ceef0
Current Irp 00000000 RefCount 0 Type 00000022 Flags 00001040AttachedDev ff0cb9e0

DevExt ff0ce928 DevNode ff0cde88
Device queue is not busy.
kd> !devnode ff0cde88 6

DevNode 0xff0cde88 for PDO 0xff0ce870 at level 0x2
  Parent 0xff0cf448   Sibling 0xff0cddc8   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xffffffff
  InstancePath is "PCI\VEN_8086&DEV_7010\0&69"
  ServiceName is "intelide"
  TargetDeviceNotify List - f 0xff0cdeec  b 0xff0cdeec
  Flags (0x00001209)  DNF_PROCESSED, DNF_ENUMERATED,
                      DNF_RESOURCE_ASSIGNED, DNF_ADDED 
 (note that the device is not yet started)
  CmResourceList at 0xe120fce8  Version 0.0  Interface 0x5  Bus #0
    Entry 0 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0xfff0 for 0x10 bytes (these are the resources used: 0xfff0-0xffff)
    Entry 1 - DevicePrivate (0x81) Device Exclusive (0x1)
      Flags (0000) -
      Data - {0x00000001, 0x00000004, 0000000000}

  IoResList at 0xe120df88 : Interface 0x5  Bus 0  Slot 0x2d
    Alternative 0 (Version 1.1)
      Descriptor 0 - Port (0x1) Device Exclusive (0x1)
        Flags (0x01) - PORT_IO
        0x000010 byte range with alignment 0x000010
 0 - 0xffff     (it could have used any 16 bytes that are 16-byte aligned between 0 and 0xffff)
      Descriptor 1 - DevicePrivate (0x81) Device Exclusive (0x1)
        Flags (0000) -
        Data:              : 0x1 0x4 0x0
```

PCMCIA の例:

```dbgcmd
kd> bp pcmcia!pcmciastartpccard
Loading symbols for 0x8039d000       pcmcia.sys ->   pcmcia.sys
kd> kb
Loading symbols for 0x80241000         ndis.sys ->   ndis.sys
ChildEBP RetAddr  Args to Child
f6413814 803a7cbd ff0d0c30 e11d8808 ff0d0c30 pcmcia!PcmciaStartPcCard 
f6413838 803a3798 ff0d0c30 ff0d1500 ff0d1588 pcmcia!PcmciaPdoPnpDispatch+0x169
f6413848 80418641 ff0d0c30 ff0d1588 00000000 pcmcia!PcmciaDispatch+0x3a
f641385c 802455cf ff0d1614 ff0d1638 00040000 ntoskrnl!IofCallDriver+0x35
f641387c 802497cf ff0d1588 ff0d0c30 ff0c8210 NDIS!ndisPassIrpDownTheStack+0x3b
f64138ac 80418641 ff0c8210 ff0d161c ff0d1640 NDIS!ndisPnPDispatch+0x1f9
f64138c0 8048de68 ff0c3508 ff0d16a8 00000000 ntoskrnl!IofCallDriver+0x35
f64138d4 8041ff5e ff0c8210 f64138f8 ff0c3508 ntoskrnl!IopAsynchronousCall+0x90
f6413920 8048b4ae ff0d0c30 ff0e0a68 ff0d16a8 ntoskrnl!IopStartDevice+0x76
f6413950 8048d707 ff0d16a8 f64139fc 00000000 ntoskrnl!IopStartAndEnumerateDevice+0x1a
f6413960 8048dc9f ff0d16a8 f64139fc ff0d1e88 ntoskrnl!IopProcessStartDevicesWorker+0x43
f6413970 8048d6f5 ff0d1e88 8048d6c4 f64139fc ntoskrnl!IopForAllChildDeviceNodes+0x1f
f6413984 8048dc9f ff0d1e88 f64139fc ff0d3268 ntoskrnl!IopProcessStartDevicesWorker+0x31
f6413994 8048d6f5 ff0d3268 8048d6c4 f64139fc ntoskrnl!IopForAllChildDeviceNodes+0x1f
f64139a8 8048dc9f ff0d3268 f64139fc ff0d7b28 ntoskrnl!IopProcessStartDevicesWorker+0x31
f64139b8 8048d6f5 ff0d7b28 8048d6c4 f64139fc ntoskrnl!IopForAllChildDeviceNodes+0x1f
f64139cc 8048d6b3 ff0d7b28 f64139fc 80087000 ntoskrnl!IopProcessStartDevicesWorker+0x31
f64139e0 804f6c97 ff0e0a68 f64139fc 8045c140 ntoskrnl!IopProcessStartDevices+0x1f
f6413a30 804f5601 000001e0 80087000 00000000 ntoskrnl!IopInitializeSystemDrivers+0x5b
f6413b7c 804f4820 80087000 00000001 00000000 ntoskrnl!IoInitSystem+0x3fe
kd> !cmreslist e11d8808

CmResourceList at 0xe11d8808  Version 0.0  Interface 0x1  Bus #0
  Entry 0 - Interrupt (0x2) Device Exclusive (0x1)
    Flags (0x01) - LATCHED
    Level 0x9, Vector 0x9, Affinity 0xffffffff
  Entry 1 - Port (0x1) Device Exclusive (0x1)
    Flags (0x01) - PORT_MEMORY PORT_IO
    Range starts at 0xdfe0 for 0x20 bytes (started with IRQ 9, IO dfe0-dfff)
  Entry 2 - DevicePrivate (0x81) Device Exclusive (0x1)
    Flags (0000) -
    Data - {0x00010120, 0000000000, 0000000000}

kd> g 
```

 

 





