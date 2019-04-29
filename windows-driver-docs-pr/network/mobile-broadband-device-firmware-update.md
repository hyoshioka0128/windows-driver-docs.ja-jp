---
title: モバイル ブロードバンド デバイス ファームウェアの更新
description: このトピックでは、Windows Update (WU) 経由でのファームウェア アップグレード デバイスをサポートする目的で、モバイル ブロード バンド (MB) モジュール製造元にガイダンスを提供します。
ms.assetid: EBB95A11-14EF-4BF5-BE90-DB99624554CD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82939a3021ab3d670e8365b8f99f5533e2f39ced
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386242"
---
# <a name="mobile-broadband-device-firmware-update"></a>モバイル ブロードバンド デバイス ファームウェアの更新


このトピックでは、Windows Update (WU) 経由でのファームウェア アップグレード デバイスをサポートする目的で、モバイル ブロード バンド (MB) モジュール製造元にガイダンスを提供します。 デバイスが準拠する必要があります、 [USB NCM モバイル ブロード バンド インターフェイス モデル (MBIM) V1.0 仕様](https://go.microsoft.com/fwlink/p/?linkid=320791)リリース-IF Device Working Group です。

このトピックの情報に適用されます。

-   Windows 8

## <a name="device-requirements"></a>デバイスの要件


モバイル ブロード バンド Windows Update を使用してファームウェアの更新プログラムをサポートするために、モジュールまたはデバイスの製造元は、次の要件に準拠する必要があります。

-   UMDF (ユーザー モード ドライバー フレームワーク) ベースのモジュールが開発したドライバーまたはデバイスの製造元、INF ファイルおよびファームウェアのペイロードと共にパッケージ化します。 このドキュメントの後半で、サンプルの INF ファイルと詳細が提供されます。
-   デバイスのファームウェアを次の機能を実装する:
    -   ファームウェアのデバイスの ID サービス (FID)。 詳細については、次を参照してください。 **FID デバイス サービス**します。
    -   ファームウェア更新デバイスのサービスをサポートするためにファームウェア。 これは、UMDF ドライバーを呼び出すと、ファームウェアのペイロードの実行/ダウンロードとファームウェア更新プロセスを開始するための機能を提供するデバイスの製造元の特定のデバイス サービス。

**操作方法の概要**

次の図は、高レベルの設計と関連する 3 つのコンポーネント間のやり取りを示しています。MBIM デバイス、Windows 8 オペレーティング システムおよび IHV は、ファームウェアのアップグレードのドライバーを指定します。

![コンポーネントの相互作用を示すイメージ。 これは、次の段落で説明します。](images/mbdevicefirmwareupdate.png)

-   WWAN サービスは、新しい MB デバイスの到着を検出するとデバイス ファームウェア ID (FID) のデバイスのサービスをサポートする場合は確認します。 存在する場合、FID は、GUID として定義されているが取得されます。 IHV は、デバイスでサポートする必要があるファームウェア デバイス サービス仕様が記載されている**下**します。
-   WWAN サービス (Windows OS)"ソフト デバイス-"を使用してノード上で、デバイスのハードウェア id。 として取得した FID が生成されます。これと呼ばれます「ソフト開発ノード」上の図にします。 開発ノードの作成を開始、最適なドライバーを検索する PnP サブシステム (Windows OS) を開始します。 Windows 8、PnP システムは、ローカル ストアからドライバーをインストールするにはまず、1 つは、使用可能な場合、および並列の OS で WU からより一致するドライバーを取得を試みます。 受信トレイの NULL のドライバーが使用される適切な一致するドライバーが"ドライバーが見つかりません"という問題を解決に使用できない場合、既定値として使用されます。
-   FID の一致に基づく、IHV WU パッケージがコンピューターにプルして、インストールされています。 FID が一意のファームウェアの SKU を表すことが必要です (ここでの一意性は組み合わせデバイス VID/PID/REV と MNO によって定義)。 WU パッケージには、IHV UMDF ドライバーとファームウェアのペイロードを作成します。
-   IHV UMDF がソフト開発のノードで読み込まれた後は、ファームウェア更新フローを制御する責任を負います。 ソフト開発ノードの有効期間が MBIM デバイスの物理的な操作に関連付けられていることに注意する必要があります。 UMDF ドライバーは、ファームウェアの更新プログラムを実行するのには、次の手順を実施するものと
    -   デバイス、ファームウェア更新プロセス中に複数回の再起動に許容されるが UMDF ドライバーをアンロードして再読み込みになります。
    -   全体のファームウェア アップグレードなど、プロセスの再起動、60 秒以内に take 配置する必要があります。
    -   ファームウェアの更新が完了し、デバイスは MBIM モードに戻されました、Windows を通知する必要があります。 これは、以前に設定をオフにして行われます DEVPKEY\_デバイス\_PostInstallInProgress プロパティ。 **https://msdn.microsoft.com/library/windows/hardware/hh451399(v=vs.85).aspx** 開発ノードのプロパティを設定する方法について説明します。 以前に設定した DEVPROP を使用してプロパティをクリアする\_型\_空です。
    -   OnPrepareHardware UMDF のコールバック中に、UMDF ドライバーは、デバイスのファームウェアを更新する必要がありますを確認するものとします。 これは、Windows Update を使用して付属していたに対してデバイスのファームウェアのバージョンを比較することによって行います。 追加のガイダンスについては、ファームウェアのバイナリの配置場所に関するドキュメントの後半で提供されます。 ファームウェアの更新が必要な場合は、UMDF ドライバーが必要です。
        -   作業項目のスケジュール設定」の説明に従って **https://msdn.microsoft.com/library/windows/hardware/hh463997(v=VS.85).aspx**します。 作業項目のコンテキストで実際のファームウェアのアップグレードが行われます。
        -   作業項目が正常にスケジューリングされると、ファームウェアの更新の開始について Windows に通知します。 DEVPKEY を設定して、その\_デバイス\_OnPrepareHardware UMDF コールバックのコンテキストでソフト開発ノードで PostInstallInProgress プロパティ。
        -   ファームウェアの更新プログラムの実行中に OnPrepareHardware コールバックのブロックを重要です。 OnPrepareHardware コールバックが、一番 1、2 秒で完了したことが期待されます。

**WU パッケージ向けサンプル INF ファイル**

このセクションでは、WU パッケージの一部であるサンプル INF を提供します。 INF ファイルで重要な点は次のとおりです。

-   ファームウェアのバイナリは、UMDF ドライバー依存しません。
-   ファームウェアのバイナリが配置されているよく知られている、事前定義された場所にファイル名の競合の下に示すようにします。 バイナリできないと、PE と COFF ヘッダーを含む実行可能ファイルができません。
-   `%windir%\Firmware\<IHVCompanyName>\<UniqueBinaryName>.bin`
-   UMDF ドライバーは、この定義済みのよく知られている場所に注意してください。
-   以下のサンプル INF テンプレートは IHV によって満たされる必要がある項目を強調表示します。

```cpp
[Version]
Signature       = "$WINDOWS NT$"
Class           = Firmware
ClassGuid       = {f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
Provider        = %Provider%
DriverVer       = 06/21/2006,6.2.8303.0
CatalogFile     = MBFWDriver.cat
PnpLockdown     = 1

[Manufacturer]
%Mfg%           = Firmware,NTx86

[Firmware.NTx86]
%DeviceDesc%    = Firmware_Install,MBFW\{FirmwareID}    ; From Device Service
;eg.%DeviceDesc%=Firmware_Install,MBFW\{2B13DD42-649C-3442-9E08-D85B26D7825C}

[Firmware_Install.NT]
CopyFiles       = FirmwareDriver_CopyFiles,FirmwareImage_CopyFiles

[Firmware_Install.NT.Services]
AddService      = WUDFRd,0x000001fa,WUDFRD_ServiceInstall

[WUDFRD_ServiceInstall]
DisplayName     = %WudfRdDisplayName%
ServiceType     = 1
StartType       = 3
ErrorControl    = 1
ServiceBinary   = %12%\WUDFRd.sys
LoadOrderGroup  = Base

[Firmware_Install.NT.CoInstallers]
CopyFiles       = WudfCoInstaller_CopyFiles

[WudfCoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000,"WUDFCoinstaller.dll"

[Firmware_Install.NT.Wdf]
UmdfService      = MBIHVFirmwareDriver,MBIHVFirmwareDriver_Install
UmdfServiceOrder = MBIHVFirmwareDriver


[MBIHVFirmwareDriver_Install]
UmdfLibraryVersion  = 1.11
ServiceBinary       = %12%\UMDF\MBFWDriver.dll
DriverCLSID         = {<DriverClassGuid>} ; From UMDF driver

[FirmwareImage_CopyFiles]
MBIHVFirmware-XYZ-1.0.bin   ; Firmware Image

[FirmwareDriver_CopyFiles]
MBFWDriver.dll          ; UMDF driver for SoftDevNode

[DestinationDirs]
FirmwareImage_CopyFiles  = 10,Firmware\MBIHV ; %SystemRoot%\Firmware\MBIHV
FirmwareDriver_CopyFiles = 12,UMDF     ;%SystemRoot%\System32\drivers\UMDF

[SourceDisksFiles]
MBIHVFirmware-XYZ-1.0.bin = 1

[SourceDisksNames]
1 = %DiskName%

; ================== Generic ==================================

[Strings]
Provider        = "MBIHV"
Mfg             = "MBIHV"
DeviceDesc      = "MBIHV Mobile Broadband Firmware Device"
DiskName        = "Firmware Driver Installation Media"
```

**ファームウェア識別デバイス サービス (FID デバイス サービス)**

MBIM 準拠しているデバイスが実装して、CID が照会すると、次のデバイス サービスをレポート\_MBIM\_デバイス\_サービス。 既存の既知のサービスは、セクション 10.1 NCM MBIM 仕様で定義されます。 Microsoft Corporation は、これを次のサービスの定義を拡張します。

サービス名 = **Microsoft ファームウェア ID**

UUID = **UUID\_MSFWID UUID**

値 = **e9f7dea2-feaf-4009-93ce-90a3694103b6**

具体的には、次の CID が定義されている UUID\_MSFWID デバイス サービス。

CID = **CID\_MBIM\_MSFWID\_FIRMWAREID**

コマンド コード = **1**

クエリ = **[はい]**

設定 =**なし**

イベント =**なし**

InformationBuffer ペイロード設定 =**該当なし**

クエリ InformationBuffer ペイロード =**該当なし**

完了 InformationBuffer ペイロード = **UUID**

**CID\_MBIM\_MSFWID\_FIRMWAREID**

MNO またはデバイスのファームウェアの ID を割り当てられている IHV が返されます。 MBIM 仕様のガイドラインに基づいて、UUID がエンコードされます。

クエリ = **MBIM で InformationBuffer\_コマンド\_MSG は使用されません。InformationBuffer MBIM で UUID が返される\_コマンド\_完了します。**

設定 =**サポートされていません。**

要請されていないイベント =**サポートされていません。**

**UMDF ドライバーの動作のコード スニペット**

前述のように、開始し、ファームウェアのアップグレードが完了したときに、Windows に UMDF ドライバーが示されます。 このセクションでは、ドライバーがこれらのイベントの Windows を通知する方法を示すコード スニペットを提供します。

```cpp
/**
 * This is the IPnpCallbackHardware*:OnPrepareHardware handler 
 * in the UMDF driver. This is called every time the firmware 
 * update is device is started. Since this handler should be 
 * blocked from returning actual the firmware update process 
 * should be done in a workitem 
 */
HRESULT
CMyDevice::OnPrepareHardware(IWDFDevice* pDevice)
{
    HRESULT hr = S_OK;
    BOOL bFirmwareUpdateInProgress = FALSE;
    BOOL bFirmwareUpdateNeeded = FALSE;
    BOOL bFirmwareUpdateIsDone = FALSE;

    //
    // The snippets below demonstrates the steps for firmware 
    // update against a MB device that loads the updated firmware 
    // on device boot. So the firmware update driver needs to
    // send the new firmware down to the device and then tell 
    // the device to initiate a stop/start. Once the device has
    // reappeared, it would have automatically loaded the 
    // new firmware
    // 


    //
    // First, determine if firmware update is in progress. This 
    // can be based on some registry key that is saved when
    // firmware update is started
    //

    // Assuming this status is returned in bFirmwareUpdateInProgress
    if (bFirmwareUpdateInProgress)
    {
        //
        // If firmware update is in progress, check if its done. For
        // this it may be necessary to access the MB device. Note that 
        // if the MB device (& hence the Firmware update device) needs
        // multiple stop/starts to do the firmware update. In that case
        // it will be marked as done at the end of the process
        //

        // Assuming this status is returned in bFirmwareUpdateIsDone
        if (bFirmwareUpdateIsDone)
        {
            //
            // Signal the completion of the firmware update
            // process.
            //
            SignalFirmwareUpdateComplete(pDevice);
        }
        else
        {
            //
            // Take appropriate steps to get notified when
            // firmware update is done. Call SignalFirmwareUpdateComplete
            // when that notification is received
            //
        }
    }
    else
    {
        //
        // Determine if firmware update is needed. This can be 
        // based on checking state in the registry of the last
        // firmware version set on the device to the firmware
        // version associated with this driver
        //
        
        // Assuming this status is returned in bFirmwareUpdateNeeded
        if (bFirmwareUpdateNeeded)
        {
            // 
            // Create and queue a workitem to perform the firmware
            // update process. IWDFWorkItem can be used for this
            //
            
            // Assuming the creation/enquing status
            // is returned in hr
            
            if (SUCCEEDED(hr))
            {
                //
                // Work item queued. It will do the firmware update
                // Tell the OS that firmware update is in progress
                //
                SignalFirmwareUpdateInProgress(pDevice);
            }
        }
    }

    //
    // If we have a failure, we clear the firmware update
    // in progress state
    //
    if (FAILED(hr))
    {
        SignalFirmwareUpdateComplete(pDevice);
    }
    return S_OK;
}

/**
 * This function tells the OS that firmware update is in progress.
 * It should be called from the firmware update UMDF driver's 
 * IPnpCallbackHardware*:OnPrepareHardware handler after it has
 * successfully queued a workitem to perform the firmware update
 */
HRESULT
CMyDevice::SignalFirmwareUpdateInProgress(
    __in IWDFDevice* pDevice
    )
{
    HRESULT hr = S_OK;    
    IWDFUnifiedPropertyStoreFactory* spPropertyStoreFactory = NULL;
    IWDFUnifiedPropertyStore* spPropStore = NULL;
    WDF_PROPERTY_STORE_ROOT wdfPropRoot = { sizeof(WDF_PROPERTY_STORE_ROOT), WdfPropertyStoreRootClassHardwareKey };
    DEVPROP_BOOLEAN boolValue = DEVPROP_TRUE;
    
    do
    {
       
        hr = pDevice->QueryInterface(IID_PPV_ARGS(&spPropertyStoreFactory));
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for property store factory. Error = 0x%x", hr);
            break;

        }
        
        hr = spPropertyStoreFactory->RetrieveUnifiedDevicePropertyStore(
            &wdfPropRoot,
            &spPropStore
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for device property store. Error = 0x%x", hr);
            break;
        }

        // Set the OS flag
        hr = spPropStore->SetPropertyData(
            reinterpret_cast<const DEVPROPKEY*>(&DEVPKEY_Device_PostInstallInProgress),
            0, // this property is language neutral
            0,
            DEVPROP_TYPE_BOOLEAN,
            sizeof(DEVPROP_BOOLEAN),
            &boolValue
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to set device property for PostInstallInProgress. Error = 0x%x", hr);
            break;
        }

        //
        // Save some state so that we know we are in the process
        // of firmware update
        //
    } while (FALSE);        

    if (spPropStore)
    {
        spPropStore->Release();
    }

    if (spPropertyStoreFactory)
    {
        spPropertyStoreFactory->Release();
    }

    return hr;
}


/**
 * This function tells the OS that firmware update is done
 * It should be called only after the full firmware update process
 * (including any MB device stop/start) has finished
 */
HRESULT
CMyDevice::SignalFirmwareUpdateComplete(
    __in IWDFDevice* pDevice
    )
{
    HRESULT hr = S_OK;    
    IWDFUnifiedPropertyStoreFactory* spPropertyStoreFactory = NULL;
    IWDFUnifiedPropertyStore* spPropStore = NULL;
    WDF_PROPERTY_STORE_ROOT wdfPropRoot = { sizeof(WDF_PROPERTY_STORE_ROOT), WdfPropertyStoreRootClassHardwareKey };
    
    do
    {
        hr = pDevice->QueryInterface(IID_PPV_ARGS(&spPropertyStoreFactory));
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for property store factory. Error = 0x%x", hr);
            break;

        }

        hr = spPropertyStoreFactory->RetrieveUnifiedDevicePropertyStore(
            &wdfPropRoot,
            &spPropStore
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for device property store. Error = 0x%x", hr);
            break;
        }

        hr = spPropStore->SetPropertyData(
            reinterpret_cast<const DEVPROPKEY*>(&DEVPKEY_Device_PostInstallInProgress),
            0, // this property is language neutral
            0,
            DEVPROP_TYPE_BOOLEAN,
            0,
            NULL
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to clear device property for PostInstallInProgress. Error = 0x%x", hr);
            break;
        }

        //
        // Save some state so that we can do quick check on 
        // whether firmware update is needed or not
        //

    } while (FALSE);        

    if (spPropStore)
    {
        spPropStore->Release();
    }

    if (spPropertyStoreFactory)
    {
        spPropertyStoreFactory->Release();
    }

    return hr;
}
```

 

 





