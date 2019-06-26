---
title: デバイスの種類の指定
description: デバイスの種類の指定
ms.assetid: 32e179f9-ab11-4360-b2fd-4276c6b6b3a0
keywords:
- デバイス オブジェクトの WDK カーネル、デバイスの種類
- デバイスの種類の WDK デバイス オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e5b2d36c9b2f754c26d319d6e2c98077b27f48
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383007"
---
# <a name="specifying-device-types"></a>デバイスの種類の指定





各デバイス オブジェクトには、*デバイスの種類*に格納されている、 **DeviceType**のメンバー、 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)構造体。 デバイスの種類は、ドライバーの基になるハードウェアの種類を表します。

呼び出すときに、デバイス オブジェクトを作成するすべてのカーネル モード ドライバーは、デバイスの適切な型の値を指定する必要があります[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)します。 **IoCreateDevice**ルーチンは、指定されたデバイスの種類を使用して初期化するために、 **DeviceType**のメンバー、**デバイス\_オブジェクト**構造体。

システムでは、アルファベット順で次のデバイスの種類値を定義します。

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

これらの定数は、Ntddk.h と Wdm.h で定義されます。 その他のデバイスの種類が定義されているかどうかを参照してください。 これらのファイルを確認します。

ファイル\_デバイス\_ディスクの仕様は、ディスク パーティションとディスクとして表示される任意のオブジェクトについて説明します。

通常、中間ドライバーは、基になるデバイスを表すデバイスの種類を指定します。 システムが指定したフォールト トレラントなディスク ドライバーなど、 *ftdisk*、ファイルの種類のデバイス オブジェクトを作成します\_デバイス\_; ディスク ミラー セット、ストライプ セット、およびボリュームの新しいデバイスの種類を定義しません。管理を設定します。

ファイル\_デバイス\_*XXX* 0 ~ 32767 の範囲の値は、Microsoft の予約されています。 すべてのドライバー開発者は、デバイスのシステム定義の種類に属するデバイスのこれらのシステム定義の定数を使用する必要があります。

ハードウェアの種類が定義されている型を一致しない場合は、いずれかのファイルの値を指定\_デバイス\_不明、または 32768 65535 までからの範囲内の値。

 

 




