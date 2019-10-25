---
title: 共同インストーラーを使用しない USB デバイスのデバイスファームウェアの更新
description: 共同インストーラーを使用せずに USB デバイスのファームウェアを更新する推奨方法について説明します。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4a762b2632f146005bcec69917c4251b4c9c5a9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844781"
---
# <a name="device-firmware-update-for-usb-devices-without-using-a-co-installer"></a>共同インストーラーを使用しない USB デバイスのデバイスファームウェアの更新

USB デバイスベンダーは、共同インストーラーを使用して、受信トレイ USB デバイスドライバーを使用するデバイスのデバイスファームウェアを更新します。 ただし、共同インストーラーは、Windows 10 に必要な新しい "Universal INF" 標準ではサポートされていません。 これにより、既存の USB デバイスのファームウェア更新プロセスに対する問題が生じます。 このトピックでは、共同インストーラーを使用せずに USB デバイスのファームウェアを更新するための推奨される方法について説明します。

## <a name="requirements"></a>要件

USB デバイスのファームウェア更新プロセスの主要な要件は次のとおりです。

1. ユーザー操作のないシームレスなファームウェア更新

1. 信頼性の高い復旧メカニズム (たとえば、bricking のデバイスはありません)

1. Windows 7 以降で動作

## <a name="overview"></a>概要

UVC カメラのような USB デバイスは、フィールド内の更新可能なファームウェアと共にリリースされます。 現時点では、ファームウェアを更新するための標準的な方法はありません。 既存のすべての更新メカニズムに共通するのは、一部のカスタムソフトウェアスイートがクライアントで実行され、ファームウェアがデバイスにダウンロードされることです。 通常、デバイスのインストールプロセスの一環として、ファームウェア更新ソフトウェアスイートがインストールされます。 共同インストーラーの開始時に、ファームウェアの更新プロセスが開始されます。 Windows 10 に共同インストーラーがないと、デバイスベンダーはフィールド内のこれらのデバイスのファームウェアを更新できなくなります。

USB デバイスのファームウェア更新シナリオに共同インストーラーが存在しないようにする場合は、ファームウェアの更新プロセスを開始するために、低いフィルタードライバーを USB デバイスに使用することをお勧めします。 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)の呼び出し中に、フィルタドライバはデバイスのファームウェアバージョンを確認し、必要に応じてファームウェアを更新します。

## <a name="firmware-update-overview"></a>ファームウェアの更新の概要

USB デバイスがシステムに接続されている場合は、汎用受信トレイドライバーがデバイスにインストールされます。 汎用ドライバーをインストールした後、OS は、ベンダー固有のドライバーパッケージの可用性を Windows Update サーバーに照会し、それをダウンロードしてドライバーをインストールします。 インストールされているドライバーパッケージは、ファームウェアの更新を実行します。

ファームウェアを更新する方法は2つあります。

1. ファームウェア更新フィルタードライバー

    1. ベンダは、ファームウェアの更新を実行する低レベルのフィルタードライバーを提供しました。

1. ファームウェア更新デバイスドライバー

    1. ベンダは、デバイスを "ファームウェア更新モード" にする、低いフィルタードライバーを提供しました。

    1. デバイスは、ファームウェア更新デバイスとして列挙されます。

    1. ベンダーが提供するファームウェア更新ドライバーがこのデバイスに対して読み込まれ、ファームウェアが更新されます。

## <a name="method-1-firmware-update-filter-driver"></a>方法 1: ファームウェア更新フィルタードライバー

この方法では、ドライバーの更新プロセスの一環として、USB デバイスドライバーに対する下位フィルタードライバーがインストールされます。 このフィルタードライバーは、ファームウェアの更新を実行します。

Windows Update サーバー上のドライバー更新プログラムパッケージには次のものが含まれます。

- ファームウェア更新プログラム WDF 下位フィルタードライバー

- ファームウェア更新プログラム WDF 下位フィルタードライバーをインストールするための拡張 INF

- "ファームウェアの .bin" ファイル

![ファームウェア更新 UMDF lower フィルタードライバーメソッド](images/fw-update-umdf-lower-filter-driver-method.png)

ドライバー更新プログラムパッケージをインストールするときに、ファームウェア更新プログラム WDF フィルタードライバーの[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが呼び出されます。 このルーチンから、WDF フィルタードライバーはデバイスの HW レジストリキーからデバイスのファームウェアバージョンを取得します。 デバイスのファームウェアは、MSOS 記述子を使用して、デバイスの HW レジストリキーにファームウェアのバージョンを配置している必要があります。

1. デバイスのファームウェアバージョンとフィルタードライバーが必要とするファームウェアのバージョンが異なる場合は、

1. デバイスの HW レジストリキーでファームウェアのバージョンを使用できません

    1. 次に、success を[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) callback に返すことによって、フィルタードライバーがそれ自体をデバイススタックに挿入します。

1. それ以外の場合、フィルタードライバーはデバイススタックに挿入されません。

    1. これは、デバイスに予期されるファームウェアがあるため、ファームウェアを更新する必要がないためです。

WDF filter ドライバーの[EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバックが後で呼び出された場合、フィルタードライバーは CM を使用してデバイスインターフェイスの変更通知を登録する必要があります。これ\_、通知を\_登録するか、IoRegisterPlugPlayNotification (UMDF または KMDF) は、USB デバイスがデバイスを登録するデバイスインターフェイスクラスをリッスンします。 例: RGB カメラ用のファームウェア更新フィルタードライバーは、KSCATEGORY\_VIDEO\_カメラに登録します。 フィルタードライバーは、通知を受信すると、ファームウェアの更新を実行する作業項目を投稿する必要があります。

UMDF ベースのファームウェア更新ドライバーでは、デバイス固有の Api を使用するか、制御転送を直接実行して USB デバイスにアクセスしてファームウェアの更新を実行することができます。 たとえば、カメラ用の UMDF ベースのフィルタードライバーは、カメラ Api を使用してファームウェアの更新を実行します。

KMDF ベースのファームウェア更新ドライバーは、ファームウェアの更新を実行するためにベンダー固有のコマンドを送信できます。

ファームウェアのフラッシュが完了したら、デバイスを切断し、バスに再接続する必要があります。 デバイスは新しいファームウェアで再列挙されます。

"ファームウェア更新フィルタードライバー" を使用する方法は、デバイスのメモリに2つのフルファームウェアイメージ (更新イメージとバックアップイメージ) を保持するのに十分なリソースを持つデバイスに推奨されます。 更新されたファームウェアのダウンロード中にエラーが発生した場合、デバイスは更新を破棄して元のファームウェアでブートすることができます。 そのため、デバイスを bricking ません。

## <a name="method-2-firmware-update-device-driver"></a>方法 2: ファームウェア更新デバイスドライバー

この方法では、ドライバーの更新プロセスの一環として、USB デバイスに対する下位フィルタードライバーがインストールされます。 このフィルタドライバは、ファームウェア更新モードで再起動するコマンドをデバイスに送信します。このモードでは、デバイスはファームウェア更新インターフェイスを公開します。 ファームウェア更新インターフェイスのドライバーは、ファームウェアの更新プログラムを読み込んで実行します。

デバイスの Windows Update サーバー上のドライバー更新プログラムパッケージには次のものが含まれます。

1. デバイスをファームウェア更新モードにする WDF 下位フィルタードライバー

1. WDF lower フィルタードライバーをインストールするための拡張 INF

ドライバー更新プログラムパッケージに加えて、次のように、Windows Update に個別のファームウェア更新デバイスドライバーパッケージが表示されます。

1. WDF ファームウェア更新デバイスドライバーとその INF

1. "ファームウェアの .bin" ファイル。

![ファームウェア更新 WDF driver メソッド](images/fw-update-wdf-driver-method.png)

ドライバー更新プログラムパッケージをインストールするときに、WDF 下位フィルタードライバーの AddDevice ルーチンが呼び出されます。 このルーチンから、フィルタードライバーはデバイスの HW レジストリキーからデバイスのファームウェアのバージョンを照会します。 デバイスのファームウェアでは、MSOS 記述子または USB デバイスの拡張機能 INF を使用して、デバイスの HW レジストリキーに "ファームウェアのバージョン" を配置する必要があります。

1. デバイスのファームウェアバージョンと、必要とされるファームウェアバージョンが異なる場合は、

1. デバイスの HW レジストリキーでファームウェアのバージョンを使用できません

1. 次に、WDF filter ドライバーがデバイススタックに挿入します。

1. それ以外の場合、WDF filter ドライバーはデバイススタックに挿入されません。

WDF filter ドライバーの[EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバックが後で呼び出されると、フィルタードライバーによって、ベンダー固有のコマンドがデバイスに発行され、それがファームウェア更新モードになります。 つまり、デバイスは、ファームウェアの更新インターフェイスを公開して、接続を切断し、再接続します。

システムは、ファームウェア更新デバイスインターフェイスを列挙します。 製造元によって提供されるファームウェア更新パッケージのカスタムファームウェア更新 WDF ドライバーは、このファームウェア更新インターフェイスに対して読み込まれます。 このドライバーは、ファームウェアを更新します。

WDF ファームウェア更新ドライバーの[EVT_WDF_DEVICE_D0_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバックが後で呼び出されると、ドライバーは、ファームウェアの更新を実行する作業項目を投稿する必要があります。

ファームウェアのフラッシュが完了したら、デバイスを切断し、バスに再接続する必要があります。 デバイスは新しいファームウェアで再列挙されます。

この方法は、デバイスのメモリ不足が原因で、更新されたファームウェアイメージを保持できないデバイスに推奨されます。 更新されたファームウェアのダウンロード中にエラーが発生した場合、デバイスは更新を破棄し、デバイスをファームウェア更新モードに再起動して、ファームウェアの更新を再試行することができます。 そのため、デバイスを bricking ません。

## <a name="recovery"></a>[回復]

ファームウェアの更新プロセスは、さまざまな理由で失敗する可能性があります。 その場合、デバイスが再び列挙されると、ファームウェア更新ドライバーがファームウェアを再度更新しようとして、再度失敗する可能性があり、この更新プロセスがループで終了する可能性があります。 ファームウェア更新ドライバーは、実行できる再試行回数に上限を設定する必要があります。 ファームウェアの更新の再試行がしきい値を超えた場合 (たとえば、3回の再試行)、フィルタードライバーは、新しいバージョンのドライバーが WU からダウンロードされるまで、ファームウェアを再度更新しないようにする必要があります。 ファームウェア更新ドライバーは、レジストリを使用して再試行の状態を維持することができます。

デバイスのファームウェア更新の最後に、デバイスをリセットして再列挙することをお勧めします。

ファームウェアの更新を実行する前に、どちらのファームウェア更新方法でも、デバイス機能を停止する必要があります。 これにより、デバイスを開くハンドルがなくなり、OS の再起動要件が回避されます。

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
