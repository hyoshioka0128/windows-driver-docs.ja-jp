---
title: デバイスのファームウェア共同インストーラーを使用せずに USB デバイスを更新します。
description: 共同インストーラーなしの USB デバイスのファームウェアを更新する推奨方法について説明します。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: ad53b257200cd14db227111a6cf7ed0767b2acf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374104"
---
# <a name="device-firmware-update-for-usb-devices-without-using-a-co-installer"></a>デバイスのファームウェア共同インストーラーを使用せずに USB デバイスを更新します。

USB デバイスのベンダーでは、共同インストーラーを使用して、受信トレイの USB デバイス ドライバーを使用するデバイスのデバイスのファームウェアを更新します。 ただし、共同インストーラーはサポートされていませんで、新しい"ユニバーサル INF"standard、Windows 10 での要件であります。 これにより、既存の USB デバイスのファームウェア更新プロセスにという課題が伴います。 このトピックでは、共同インストーラーなしの USB デバイスのファームウェアを更新する推奨方法について説明します。

## <a name="requirements"></a>要件

USB デバイスのファームウェア更新プロセスの主要な要件は次のとおりです。

1. ユーザーの操作なしでのシームレスなファームウェアの更新

1. 信頼性の高い復旧メカニズムが (たとえば、ありません bricking デバイスの)

1. Windows 7 以降の動作します。

## <a name="overview"></a>概要

UVC カメラなどの USB デバイスは、フィールドの更新可能なファームウェアでリリースします。 現在のファームウェアを更新する標準的な方法はありません。 既存のすべての更新メカニズムに共通する 1 つは、いくつかのカスタム ソフトウェア スイートは、クライアントで実行し、デバイスにファームウェアのダウンロードには。 通常、デバイスのインストール プロセスの一部としてソフトウェア スイートを更新するファームウェアがインストールされています。 共同インストーラー キック、ファームウェア更新プロセスを開始します。 Windows 10 での共同インストーラーがない場合では、デバイスのベンダーが、フィールドにこれらのデバイスのファームウェアを更新できなくなります。

USB デバイスのファームウェア更新のシナリオは、USB デバイスが低いフィルター ドライバーを使用するは、共同インストーラーがないことを回避するために推奨される方法は、ファームウェア更新プロセスを開始します。 中に、 [ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)を呼び出すと、フィルター ドライバーはデバイス ファームウェアのバージョンを確認し、必要に応じてファームウェアを更新します。

## <a name="firmware-update-overview"></a>ファームウェアの更新の概要

システム、USB デバイスが接続されているときに、デバイスの汎用的な受信トレイのドライバーがインストールされています。 一般的なドライバーをインストールした後は、OS は、ベンダーの特定のドライバー パッケージの可用性の Windows Update サーバーに照会、ダウンロードと、ドライバーがインストールされます。 インストールされているドライバー パッケージでは、ファームウェアの更新プログラムを実行します。

ファームウェアを更新することが 2 つの方法はあります。

1. ファームウェアの更新プログラム フィルター ドライバー

    1. 仕入先は、下位のフィルター ドライバー、ファームウェアの更新を実行するを指定します。

1. ファームウェア更新デバイス ドライバー

    1. 仕入先は、「ファームウェア更新モード」で、デバイスは、下位のフィルター ドライバーを指定します。

    1. ファームウェア更新デバイスとして、デバイスを列挙します。

    1. ベンダー提供のファームウェア更新のドライバーとファームウェア更新をこのデバイスに対して読み込まれます。

## <a name="method-1-firmware-update-filter-driver"></a>方法 1:ファームウェアの更新プログラム フィルター ドライバー

このメソッドでドライバーの更新プロセスの一環として、USB デバイス ドライバーを下位のフィルター ドライバーがインストールされます。 このフィルター ドライバーでは、ファームウェアの更新プログラムを実行します。

Windows の更新サーバー上のドライバー更新プログラム パッケージが含まれます。

- ファームウェア更新 WDF 低いフィルター ドライバー

- ファームウェア更新 WDF 低いフィルター ドライバーをインストールする INF の拡張機能

- "Firmware.bin"ファイル

![ファームウェア更新 UMDF 低いフィルター ドライバー メソッド](images/fw-update-umdf-lower-filter-driver-method.png)

ドライバーの更新プログラム パッケージをインストールするときに WDF のファームウェアの更新にフィルター ドライバーの[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンが呼び出されます。 このルーチンでは、WDF フィルター ドライバーはデバイス ハードウェアのレジストリ キーから、デバイスのファームウェア バージョン用に表示されます。 デバイスのファームウェアがデバイス ハードウェアのレジストリ キーに MSO 記述子を使用してファームウェアのバージョンを配置が必要があります。

1. デバイスのファームウェアのバージョンとフィルター ドライバーの予期されるファームウェア バージョンが異なる場合、または

1. ファームウェアのバージョンがデバイス ハードウェアのレジストリ キーでご利用いただけません

    1. 次に、フィルター ドライバーに自動的に挿入デバイス スタックを成功を返すことによって[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)コールバック。

1. それ以外の場合、フィルター ドライバーに挿入されない自体、デバイス スタック

    1. デバイスがある必要なファームウェアとファームウェアの更新の必要性がないためです。

ときに、 [EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) WDF フィルター ドライバーのコールバックが、後で呼び出されると、フィルター ドライバーは、CM を使用して、デバイス インターフェイスの変更通知を登録する必要があります\_登録\_通知のほか、IoRegisterPlugPlayNotification (UMDF または KMDF) USB デバイスをデバイスのインターフェイス クラスをリッスンするようには、デバイスを登録します。 例: KSCATEGORY の RGB カメラのファームウェアの更新プログラム フィルター ドライバーは登録\_ビデオ\_カメラ。 通知を受信するには、フィルター ドライバーは、ファームウェアの更新を実行する作業項目を投稿する必要があります。

ベース UMDF ドライバーを更新するファームウェアがデバイスを使用できる特定の Api やコントロールの問題は、ファームウェア更新を実行する USB デバイスにアクセスするには、直接転送します。 たとえば、カメラの UMDF ベースのフィルター ドライバーはカメラ Api を使用して、ファームウェア更新を実行するは。

ベース KMDF ドライバーのファームウェア更新は、仕入先にファームウェア更新を実行する特定のコマンドを送信できます。

ファームウェアをフラッシュの完了時にデバイスが接続を切断し、バスに再接続する必要があります。 デバイスは、新しいファームウェア再列挙型になります。

「ファームウェアの更新フィルター ドライバー」を使用するメソッドは、デバイスのメモリに 2 つのファームウェアの完全なイメージ (イメージの更新およびバックアップ イメージ) を保持するために十分なリソースがあるデバイスをお勧めします。 理由は、更新したファームウェアのダウンロード中にエラーがある場合は、デバイスは、更新プログラムの破棄し、その元のファームウェアを起動します。 したがって、bricking デバイスがありません。

## <a name="method-2-firmware-update-device-driver"></a>方法 2:ファームウェア更新デバイス ドライバー

このメソッドでドライバーの更新プロセスの一環として USB デバイスに下位のフィルター ドライバーがインストールされます。 このフィルター ドライバーはコマンドを送信するデバイスのファームウェア更新モードで再起動をデバイスがファームウェアの更新プログラム インターフェイスを公開します。 ドライバー、ファームウェアの更新プログラム インターフェイスを読み込むをファームウェア更新を実行します。

デバイスの Windows の更新のサーバー上のドライバー更新プログラム パッケージが含まれます。

1. ファームウェアでデバイスを配置する WDF 低いフィルター ドライバーの更新モード

1. WDF の低いフィルター ドライバーをインストールする INF の拡張機能

個別のファームウェア更新デバイス ドライバー パッケージを Windows 更新、上に存在するだけでなく、ドライバーの更新プログラム パッケージを使用します。

1. WDF のファームウェア更新デバイス ドライバーと、INF、および

1. "Firmware.bin"ファイルです。

![ファームウェア更新 WDF ドライバー メソッド](images/fw-update-wdf-driver-method.png)

Lower、ドライバーの更新プログラム パッケージを WDF のインストール中にフィルター ドライバーの AddDevice ルーチンが呼び出されます。 このルーチンでは、フィルター ドライバーがデバイス ハードウェアのレジストリ キーから、デバイスのファームウェア バージョンのクエリします。 デバイスのファームウェアは、「ファームウェア バージョン」、MSO 記述子またはデバイスのハードウェアのレジストリ キーに、USB デバイスの拡張機能、INF を使用して配置する必要があります。

1. デバイスのファームウェアのバージョンと、フィルター ドライバーとファームウェアのバージョンが異なる予想される場合または

1. ファームウェアのバージョンがデバイス ハードウェアのレジストリ キーでご利用いただけません

1. 次に、WDF フィルター ドライバーに自動的に挿入デバイス スタック。

1. それ以外の場合、WDF フィルター ドライバーに挿入されない自体、デバイス スタック

ときに、 [EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)後で、WDF フィルター ドライバーのコールバックが呼び出される、フィルター ドライバーのベンダーが発行するデバイスのファームウェア更新モードで配置される特定のコマンド。 つまり、デバイスは切断し、再接続、ファームウェアの更新プログラム インターフェイスを公開します。

システムは、ファームウェア更新デバイス インターフェイスが列挙されます。 カスタムのファームウェア更新 WDF ドライバー、ファームウェアの更新プログラム パッケージのベンダーによって提供されるは、このインターフェイスのファームウェア更新の負荷になります。 このドライバー、ファームウェアが更新されます。

ときに、 [EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)後で、ドライバーの WDF ファームウェア更新のコールバックが呼び出される、ドライバー、ファームウェアの更新を実行する作業項目を投稿する必要があります。

ファームウェアをフラッシュの完了時にデバイスが接続を切断し、バスに再接続する必要があります。 デバイスは、新しいファームウェア再列挙型になります。

このメソッドは、デバイス上のメモリが不足しているのため、更新されたバージョンと元のファームウェア イメージを保持できないデバイスをお勧めします。 理由は、再試行できるは、ファームウェアの更新と更新したファームウェアのダウンロード中にエラーがある場合は、デバイスの更新プログラムの破棄しデバイスをもう一度そのファームウェアの更新モードを起動できます。 したがって、bricking デバイスがありません。

## <a name="recovery"></a>回復

ファームウェアの更新プロセスは、さまざまな理由で失敗します。 その場合は、デバイスが再び列挙されたときに、ファームウェアの更新ドライバー、ファームウェアの更新をもう一度試みることがあり、再び失敗する可能性があり、ループ内でこの更新プロセスが最終的に可能性があります。 ドライバーがファームウェアの更新は、実行でき、再試行の回数に上限を配置する必要があります。 ファームウェアの更新時に、フィルター ドライバーは WU から新しいバージョンのドライバーがダウンロードされるまで、もう一度、ファームウェアの更新を試行する必要があります (たとえば、3 回) のしきい値を超えて再試行回数を取得します。 ファームウェア ドライバーの更新は、レジストリを使用して、再試行の状態を保持する可能性があります。

デバイス ファームウェアの更新の最後では推奨自体、デバイスをリセットし、再列挙します。

どちらのメソッドのファームウェアの更新、デバイスの機能は、ファームウェアの更新を実行する前に停止する必要があります。 これにより、デバイスに対して開いているハンドルがない任意の OS 再起動の必要性を回避できます。

## <a name="sample-inf"></a>サンプル INF

```INF
;==============================================================================
; Microsoft Extension INF for USB Camera Firmware Update UMDF Filter Driver
; Copyright (C) Microsoft Corporation.  All rights reserved.
;==============================================================================

[Version]
Signature="$WINDOWS NT$"
Class=Extension
ClassGUID={e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider=%CONTOSO%
ExtensionId = {BC6EE554-271C-48C8-B713-8078833962BD} ; replace with your own GUID
CatalogFile.NT = SampleExtension.cat
DriverVer=08/28/2017,10.0.1700.000

[SourceDisksFiles]
ContosoFirmwareUpdateFilterDriver.dll=1
ContosoFirmware.bin=1

[SourceDisksNames]
1 = %MediaDescription%

[DestinationDirs]
UMDriverCopy=12,UMDF ; copy to drivers\UMDF
ContosoFirmwareCopy=12,ContosoFirmware ; copy to drivers\ContosoFirmware
DefaultDestDir = 12

[UMDriverCopy]
ContosoFirmwareUpdateFilterDriver.dll

[ContosoFirmwareCopy]
ContosoFirmware.bin

[Manufacturer]
%CONTOSO% = ContosoFirmwareUpdateFilterDriver,ntamd64

[ContosoFirmwareUpdateFilterDriver.ntamd64]
; replace with your camera device VID PID
%ContosoCamera.DeviceDesc% = ContosoFirmwareUpdateFilterDriver_Install, USB\VID_1234&PID_1234&REV_1234

[ContosoFirmwareUpdateFilterDriver_Install]
CopyFiles=UMDriverCopy, ContosoFirmwareCopy

[ContosoFirmwareUpdateFilterDriver_Install.HW]
AddReg = ContosoFirmwareUpdateFilterDriver.AddReg

[ContosoFirmwareUpdateFilterDriver.AddReg]
; Load the redirector as an lower filter on this specific device.
; 0x00010008 - FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
HKR,,"LowerFilters",0x00010008,"WUDFRd"

[ContosoFirmwareUpdateFilterDriver_Install.Services]
AddService=WUDFRd,0x000001f8,WUDFRD_ServiceInstall

[WUDFRD_ServiceInstall]
DisplayName = %WudfRdDisplayName%
ServiceType = 1
StartType = 3
ErrorControl = 1
ServiceBinary = %12%\WUDFRd.sys

[ContosoFirmwareUpdateFilterDriver_Install.Wdf]
UmdfService=ContosoFirmwareUpdateFilterDriver, ContosoFirmwareUpdateFilterDriver.UmdfFilter
UmdfServiceOrder=ContosoFirmwareUpdateFilterDriver

[ContosoFirmwareUpdateFilterDriver.UmdfFilter]
UmdfLibraryVersion=2.0.0
ServiceBinary= "%12%\UMDF\ContosoFirmwareUpdateFilterDriver.dll"

[Strings]
CONTOSO = "Contoso Inc."
ContosoCamera.DeviceDesc = "Contoso Camera Extension"
MediaDescription="Contoso Camera Firmware Update Filter Driver Installation Media"
WudfRdDisplayName = "WDF Reflector Driver"
```
