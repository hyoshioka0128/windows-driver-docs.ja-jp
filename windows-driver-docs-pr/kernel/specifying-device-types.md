---
title: デバイスの種類の指定
description: デバイスの種類の指定
ms.assetid: 32e179f9-ab11-4360-b2fd-4276c6b6b3a0
keywords:
- デバイスオブジェクト WDK カーネル、デバイスの種類
- デバイスの種類 WDK デバイスオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65bc2576b84791b73b17277bc09877e8d292c5e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838417"
---
# <a name="specifying-device-types"></a>デバイスの種類の指定





各デバイスオブジェクトのデバイスの*種類*は、デバイス[ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の **(devicetype**メンバーに格納されています。 デバイスの種類は、ドライバーの基になるハードウェアの種類を表します。

デバイスオブジェクトを作成するすべてのカーネルモードドライバーは、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出すときに、適切なデバイスの種類の値を指定する必要があります。 **IoCreateDevice**ルーチンは、指定されたデバイスの種類を使用して、**デバイス\_オブジェクト**構造の **(devicetype**メンバーを初期化します。

システムでは、次のデバイスの種類の値がアルファベット順に一覧表示されます。

```cpp
#define FILE_DEVICE_8042_PORT           0x00000027
#define FILE_DEVICE_ACPI                0x00000032
#define FILE_DEVICE_BATTERY             0x00000029
#define FILE_DEVICE_BEEP                0x00000001
#define FILE_DEVICE_BUS_EXTENDER        0x0000002a
#define FILE_DEVICE_CD_ROM              0x00000002
#define FILE_DEVICE_CD_ROM_FILE_SYSTEM  0x00000003
#define FILE_DEVICE_CHANGER             0x00000030
#define FILE_DEVICE_CONTROLLER          0x00000004
#define FILE_DEVICE_DATALINK            0x00000005
#define FILE_DEVICE_DFS                 0x00000006
#define FILE_DEVICE_DFS_FILE_SYSTEM     0x00000035
#define FILE_DEVICE_DFS_VOLUME          0x00000036
#define FILE_DEVICE_DISK                0x00000007
#define FILE_DEVICE_DISK_FILE_SYSTEM    0x00000008
#define FILE_DEVICE_DVD                 0x00000033
#define FILE_DEVICE_FILE_SYSTEM         0x00000009
#define FILE_DEVICE_FIPS                0x0000003a
#define FILE_DEVICE_FULLSCREEN_VIDEO    0x00000034
#define FILE_DEVICE_INPORT_PORT         0x0000000a
#define FILE_DEVICE_KEYBOARD            0x0000000b
#define FILE_DEVICE_KS                  0x0000002f
#define FILE_DEVICE_KSEC                0x00000039
#define FILE_DEVICE_MAILSLOT            0x0000000c
#define FILE_DEVICE_MASS_STORAGE        0x0000002d
#define FILE_DEVICE_MIDI_IN             0x0000000d
#define FILE_DEVICE_MIDI_OUT            0x0000000e
#define FILE_DEVICE_MODEM               0x0000002b
#define FILE_DEVICE_MOUSE               0x0000000f
#define FILE_DEVICE_MULTI_UNC_PROVIDER  0x00000010
#define FILE_DEVICE_NAMED_PIPE          0x00000011
#define FILE_DEVICE_NETWORK             0x00000012
#define FILE_DEVICE_NETWORK_BROWSER     0x00000013
#define FILE_DEVICE_NETWORK_FILE_SYSTEM 0x00000014
#define FILE_DEVICE_NETWORK_REDIRECTOR  0x00000028
#define FILE_DEVICE_NULL                0x00000015
#define FILE_DEVICE_PARALLEL_PORT       0x00000016
#define FILE_DEVICE_PHYSICAL_NETCARD    0x00000017
#define FILE_DEVICE_PRINTER             0x00000018
#define FILE_DEVICE_SCANNER             0x00000019
#define FILE_DEVICE_SCREEN              0x0000001c
#define FILE_DEVICE_SERENUM             0x00000037
#define FILE_DEVICE_SERIAL_MOUSE_PORT   0x0000001a
#define FILE_DEVICE_SERIAL_PORT         0x0000001b
#define FILE_DEVICE_SMARTCARD           0x00000031
#define FILE_DEVICE_SMB                 0x0000002e
#define FILE_DEVICE_SOUND               0x0000001d
#define FILE_DEVICE_STREAMS             0x0000001e
#define FILE_DEVICE_TAPE                0x0000001f
#define FILE_DEVICE_TAPE_FILE_SYSTEM    0x00000020
#define FILE_DEVICE_TERMSRV             0x00000038
#define FILE_DEVICE_TRANSPORT           0x00000021
#define FILE_DEVICE_UNKNOWN             0x00000022
#define FILE_DEVICE_VDM                 0x0000002c
#define FILE_DEVICE_VIDEO               0x00000023
#define FILE_DEVICE_VIRTUAL_DISK        0x00000024
#define FILE_DEVICE_WAVE_IN             0x00000025
#define FILE_DEVICE_WAVE_OUT            0x00000026
```

これらの定数は Ntddk と Wdm で定義されています。 これらのファイルをチェックして、追加のデバイスの種類が定義されているかどうかを確認します。

ファイル\_デバイス\_ディスク仕様には、ディスクパーティションと、ディスクとして表示されるすべてのオブジェクトが含まれます。

中間ドライバーは、通常、基になるデバイスを表すデバイスの種類を指定します。 たとえば、システムによって提供される障害トレラントディスクドライバーである*ftdisk*は、種類が FILE\_DEVICE\_disk のデバイスオブジェクトを作成します。ミラーセット、ストライプセット、および管理するボリュームセットの新しいデバイスの種類は定義されていません。

0 ~ 32767 の範囲のファイル\_デバイス\_*XXX*の値は、Microsoft 用に予約されています。 すべてのドライバーライターは、システム定義のデバイスの種類に属するデバイスに対して、これらのシステム定義定数を使用する必要があります。

ハードウェアの種類が定義されているいずれの型とも一致しない場合は、ファイル\_デバイス\_不明 のいずれかの値、または 32768 ~ 65535 の範囲の値を指定します。

 

 




