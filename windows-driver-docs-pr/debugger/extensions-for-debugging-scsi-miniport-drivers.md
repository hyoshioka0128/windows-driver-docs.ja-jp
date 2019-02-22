---
title: SCSI ミニポート ドライバーをデバッグするための拡張機能
description: SCSI ミニポート ドライバーをデバッグするための拡張機能
ms.assetid: 6e6c35e5-d9dd-430a-8fc4-86f24344c24d
keywords:
- SCSI ミニポート デバッグ、有用な拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6cc9c9db0203cd571eb22d24eb88b9632115032
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529738"
---
# <a name="extensions-for-debugging-scsi-miniport-drivers"></a>SCSI ミニポート ドライバーをデバッグするための拡張機能


SCSI ミニポート ドライバーをデバッグするときに役立つ次のデバッガー拡張機能。 一般的なデバッガー拡張機能は、SCSI ミニポートのデバッグにこれらの後に最初に、表示されます。

[**!devobj**](-devobj.md)  
**! Devobj**拡張機能は、デバイスに関する詳細情報を表示します。\_オブジェクト。 場合、**現在 Irp**フィールドが null 以外の場合これは、SCSI マップ レジスタの待機されているドライバーによって発生する可能性があります。

以下に例を示します。

```dbgcmd
0: kd> !devobj 8633da70
Device object (8633da70) is for:
 adpu160m1 \Driver\adpu160m DriverObject 8633eeb8
Current Irp 860ef008 RefCount 0 Type 00000004 Flags 00000050
Dacl e129871c DevExt 8633db28 DevObjExt 8633dfd0
ExtensionFlags (0000000000)
AttachedTo (Lower) 863b2978 \Driver\PCI
Device queue is not busy. 
```

[**!errlog**](-errlog.md)  
**! Errlog**拡張機能は、I/O システムのエラー ログで、保留中のエントリの内容を表示します。

[**!object**](-object.md)  
**! オブジェクト**拡張機能がシステム オブジェクトに関する情報を表示します。 この拡張機能では、すべての SCSI デバイスが表示されます。

次に、例を示します。

```dbgcmd
0: kd> !object \device\scsi
Object: e12a2520  Type: (863d12c8) Directory
    ObjectHeader: e12a2508
    HandleCount: 0  PointerCount: 9
    Directory Object: e1001100  Name: Scsi

    Hash Address  Type          Name
    ---- -------  ----          ----
     04  86352040 Device        adpu160m1Port3Path0Target6Lun0
     11  86353040 Device        adpu160m1Port3Path0Target1Lun0
     13  86334a70 Device        lp6nds351
     22  862e6040 Device        adpu160m1Port3Path0Target0Lun0
     24  8633da70 Device        adpu160m1
     25  86376040 Device        adpu160m2
     34  862e5040 Device        adpu160m1Port3Path0Target2Lun0 
```

[**! pcr**](-pcr.md)  
**! Pcr**拡張機能、プロセッサのプロセッサ コントロール リージョン (PCR) についての詳細を表示します。 情報には、役に立ちます、DPC キュー内のアイテムが含まれます。 ときに停止しているドライバーまたはタイムアウトをデバッグします。

[**!minipkd.help**](-minipkd-help.md)  
**! Minipkd.help**拡張機能がすべての Minipkd.dll 拡張機能コマンドの一覧を表示します。

次のようなエラー メッセージが表示されたら、シンボル パスが正しくないし、Scsiport.sys シンボルの正しいバージョンをポイントしていないことを示します。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

[ **.Sympath (シンボル パスの設定)** ](-sympath--set-symbol-path-.md)パスを変更して、現在のパスを表示するコマンドを使用できます。 [ **.Reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンドが、現在のパスからシンボルを再読み込みします。

[**! minipkd.adapter アダプター**](-minipkd-adapter.md)  
**! Minipkd.adapter**拡張機能には、指定したアダプターに関する詳細情報が表示されます。 **アダプター**を調べるには、 **DevExt**フィールドに、 **! minipkd.adapters**を表示します。

[**! minipkd.adapters**](-minipkd-adapters.md)  
**! Minipkd.adapters**拡張機能は、すべてのアダプター SCSI ポート ドライバーと連動する、Windows によって指定されているを表示し、個々 のデバイスは、各アダプターに関連付けられています。

以下に例を示します。

```dbgcmd
0: kd> !minipkd.adapters
Adapter \Driver\lp6nds35     DO 86334a70         DevExt 86334b28
Adapter \Driver\adpu160m     DO 8633da70         DevExt 8633db28
 LUN 862e60f8 @(0,0,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e6040
 LUN 863530f8 @(0,1,0) c ev p d pnp(00/ff) pow(0,0) DevObj 86353040
 LUN 862e50f8 @(0,2,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e5040
 LUN 863520f8 @(0,6,0)   ev     pnp(00/ff) pow(0,0) DevObj 86352040
Adapter \Driver\adpu160m     DO 86376040         DevExt 863760f8 
```

次のようなエラー メッセージは、シンボル パスに誤りがあり、Scsiport.sys 記号の正しいバージョンを指していないか、SCSI ポート ドライバーと連携するすべてのアダプターを識別する Windows されていないことを示します。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

場合、 [ **! minipkd.help** ](-minipkd-help.md)返しますヘルプ情報を正常に SCSI ポート シンボルでは、適切な拡張機能コマンド。

[**! minipkd.exports アダプター**](-minipkd-exports.md)  
**! Minipkd.exports**拡張機能には、指定したアダプターのミニポート エクスポートのアドレスが表示されます。

[**! minipkd.lun {LUN |デバイス}**](-minipkd-lun.md)  
**! Minipkd.lun**拡張機能には、指定した論理ユニットの拡張機能 (LUN) に関する情報が表示されます。 LUN は、そのアドレスでいずれかを指定 (調べることで見つかります、 **LUN**フィールドに、 **! minipkd.adapters**表示) または物理デバイス オブジェクトが (に含まれている、 **DevObj**のフィールド、 **! minipkd.adapters**表示)。

[**!minipkd.portconfig PortConfig**](-minipkd-portconfig.md)  
**! Minipkd.portconfig**拡張機能は、指定されたポートに関する詳細情報を表示します。\_構成\_データ。 **PortConfig**で見つかる、**ポートの構成情報**のフィールド、 **! minipkd.adapter**を表示します。

[**!minipkd.req {Adapter | Device}**](-minipkd-req.md)  
**! Minipkd.req**拡張機能は、指定されたアダプターまたは LUN のデバイスのすべての現在アクティブな要求に関する情報を表示します。

[**!minipkd.srb SRB**](-minipkd-srb.md)  
**! Minipkd.srb**拡張機能には、指定された SCSI 要求ブロック (SRB) に関する詳細情報が表示されます。 アドレスでは、SRB を指定します。 現在アクティブな要求のすべてのアドレスが記載されて、 **SRB**からの出力のフィールド、 **! minipkd.req**コマンド。

[**! scsikd.classext\[デバイス\[レベル\]\]**](-scsikd-classext.md)  
**! Scsikd.classext**拡張機能には、指定したクラスのプラグ アンド プレイ (PnP) デバイスまたはそのようなすべてのデバイスの一覧に関する詳細情報が表示されます。 *デバイス*デバイス オブジェクトまたはクラスの PnP デバイスのデバイスの拡張機能です。 場合*デバイス*は省略すると、すべてのクラスの PnP 拡張機能の一覧が表示されます。

以下に例を示します。

```dbgcmd
0: kd> !scsikd.classext 

 ' !scsikd.classext 8633e3f0 '   (             ) "IBM     " / "DDYS-T09170M    " / "S93E" / "        XBY45906"
 ' !scsikd.classext 86347b48 '   (paging device) "IBM     " / "DDYS-T09170M    " / "S80D" / "        VDA60491"
  ' !scsikd.classext 86347360 '   (             ) "UNISYS  " / "003451ST34573WC " / "5786" / "HN0220750000181300L6"
  ' !scsikd.classext 861d1898 '   (             ) "" / "MATSHITA CD-ROM CR-177" / "7T03" / ""

 usage: !classext <class fdo> <level [0-2]> 
```

[**! scsikd.scsiext デバイス**](-scsikd-scsiext.md)  
**! Scsikd.scsiext**拡張機能が指定された SCSI ポート拡張機能に関する詳細情報が表示されます。 *デバイス*アダプターまたは LUN のいずれかのデバイスの拡張機能、デバイス オブジェクトにすることができます。

例をいくつか紹介します。

```dbgcmd
0: kd> !scsikd.scsiext 86353040
Common Extension:
   < ..omitted.. >
Logical Unit Extension:
  Address (3, 0, 1, 0) Claimed  Enumerated Visible
  LuFlags (0x00000000):
  Retry 0x00          Key 0x008889ff
  Lock 0x00000000  Pause 0x00000000   CurrentLock: 0x00000000
  HwLuExt 0x862e6f00  Adapter 0x8633db28  Timeout 0x0000000a
  NextLun 0x00000000  ReadyLun 0x00000000
  Pending 0x00000000  Busy 0x00000000     Untagged 0x00000000
  < ..omitted.. >
Request list @0x86353200:
      Tick count is 2526
      SrbData 8615d700  Srb 8611f4fc  Irp 8611f2b8   Key 60197  <1s
      SrbData 85e72868  Srb 86100c3c Irp 861009f8   Key e29dc7  <1s

0: kd> !scsikd.scsiext 8633da70 
Common Extension:
   < ..omitted.. >
Adapter Extension:
  Port 3     IsPnp VirtualSlot HasInterrupt
  LowerPdo 0x84f9fb68   HwDevExt 0x84634004   Active Requests 0x00000000
  MaxBus 0x03   MaxTarget 0x40   MaxLun 0x08
  Port Flags (0x00001000): PD_DISCONNECT_RUNNING
  NonCacheExt 0x850d4000  IoBase 0xd80f0000   Int 0x23  < ..omitted.. > 
```

[**! scsikd.srbdata アドレス**](-scsikd-srbdata.md)  
**! Scsikd.srbdata**拡張機能は、指定 SRB に関する詳細情報を表示します。\_データ追跡ブロックします。

 

 





