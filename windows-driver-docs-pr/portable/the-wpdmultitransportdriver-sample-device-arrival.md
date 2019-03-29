---
Description: MultiTransport デバイスのサポート
title: MultiTransport デバイスのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3f686c03b91ec7d64486ac475372590f015725f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349395"
---
# <a name="multitransport-device-support"></a>MultiTransport デバイスのサポート


WpdMultiTransportDriver サンプルは、WpdHelloWorldDriver に基づいており、元のドライバーのソース コードのほとんどは変更されません。 具体的には、オブジェクトの列挙型、プロパティ、および機能をサポートするコードには、非常にいくつかの変更やリビジョンが含まれています。

2 つの主な領域に、WpdMultiTransportDriver のコードに変更履歴が表示されます。 デバイス到着と I/O キュー。 デバイスの到着をサポートするコードが 2 つのファイルで見つかった*Device.cpp*と*Driver.cpp*します。 I/O キューをサポートするコードは「 *Driver.cpp*と*Queue.cpp*

## <a name="span-idmultitransportdevice-arrivalspanspan-idmultitransportdevice-arrivalspanspan-idmultitransportdevice-arrivalspanmultitransport-device-arrival"></a><span id="Multitransport_Device-Arrival"></span><span id="multitransport_device-arrival"></span><span id="MULTITRANSPORT_DEVICE-ARRIVAL"></span>Multitransport デバイス到着


デバイス到着コードは「、 **CDevice::OnPrepareHardware**メソッド (で、 *Device.cpp*ファイル) と、 **CDriver::OnDeviceAdd**メソッド (で*Driver.cpp*ファイル)。

内のコード、 **CDevice::OnPrepareHardware** WPD クラスの拡張機能を初期化する前に、メソッドは、次のタスクを完了します。 (最後の 3 つのタスクは、WPD クラスの拡張機能に渡されるオプションのパラメーターを設定します)。

並列のキューが必要なように、 **IOCTL\_複合\_トランスポート\_要求 Ioctl**デバイス インターフェイスの状態の変更時に、WPD クラスのインストーラーから正しく受信することができます。 2 番目のキューは、トランスポート ドライバーが使用する (たとえば、並列でない) 別のディスパッチ モードを使用できます。 シーケンシャルなキューでは、WUDF は一度に 1 つの要求をのみであるため、管理も簡素化します。 ただし、WPD ドライバーが並列で複数の要求を処理できる場合は、これは必要ありません、セカンダリ キュー。

|                                                                       |                                                                                                                                                                                                                                  |
|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| タスク                                                                  | 説明                                                                                                                                                                                                                      |
| 機能の一意な識別子 (FUID) を作成します。                         | FUID は、ドライバーが初期化中に WPD クラスの拡張機能に渡されるグローバル一意識別子 (GUID) 値です。 (クラスの拡張機能に、各トランスポートにあるこの FUID が関連付けます)。                                   |
| ポインターを取得、 **IQueueCallbackDeviceIoControl**インターフェイス。 | ドライバーは、このポインターを使用して、非-WPD Ioctl クラスの拡張機能を転送します。                                                                                                                                             |
| Multitransport モード オプションを有効にします。                                | このオプションは、multitransport フレームワークを設定する必要があります、WPD クラスの拡張を通知します。                                                                                                                                  |
| 必要に応じてプラグ アンド プレイ (PnP) の値を設定します。                         | これらの値は、フレームワークを multitransport 構成に使用されます。                                                                                                                                                                 |
| 現在のトランスポートの帯域幅を設定します。                                  | この値は、クラスの拡張および複合ドライバーによって使用されます (*WpdComp.dll*)。 複合のドライバーでは、拡張機能から値を取得し、複数のトランスポートがアクティブである場合に最適なトランスポートを決定するために使用します。 |

 

次のコード例から、 **CDevice::OnPrepareHardware**メソッドは、サンプルのドライバーが、機能固有の識別子 (FUID) を作成する方法を示しています。 この GUID の作成の前のコメントを確認してください。

```ManagedCPlusPlus
 // ATTENTION: The following GUID value is provided for illustrative
                // purposes only.
                //
                // Rather than hard-coding a GUID value in your driver, the driver
                // must obtain a GUID value from the device. The driver can provision the GUID value on the
                // device (upon first-connect) by
                // using CoCreateGUID and setting that value into non-volatile storage
                // on the device. The same GUID value is then  reported by each
                // of your device's transports. To avoid a provisioning race condition,
                // always read the value from the device after provisioning. Only
                // provision the GUID one time. Thereafter, always use the value that is provided
                // by the device.
                GUID guidFUID = { 0x245e5e81, 0x2c17, 0x40a4, { 0x8b, 0x10, 0xe9, 0x43, 0xc5, 0x4c, 0x97, 0xb2 } };
```

次のコード例、 **CDevice::OnPrepareHardware**メソッドは、前の表の 3 つの残りのタスクを示しています (の取得、 **IQueueCallbackDeviceIoControl**ポインターの有効化multitransport のモード、PnP 値と現在の帯域幅を設定します。

```ManagedCPlusPlus
     if (hr == S_OK)
                {
                    m_pWpdBaseDriver->m_pQueueCallback = NULL;

                    HRESULT hrTemp = m_pPortableDeviceClassExtension->QueryInterface(
                        __uuidof(IQueueCallbackDeviceIoControl),
                        (void**)&m_pWpdBaseDriver->m_pQueueCallback
                        );
                    CHECK_HR(hrTemp, "Failed to obtain IQueueCallbackDeviceIoControl interface from class extension");

                    if (hrTemp == S_OK)
                    {
                        // Enable the Multi-Transport Mode option
                        hr = pOptions->SetBoolValue(WPD_CLASS_EXTENSION_OPTIONS_MULTITRANSPORT_MODE, TRUE);
                        CHECK_HR(hr, "Failed to enable multi-transport mode");

                        // Create a PnP ID value collection
                        if (hr == S_OK)
                        {
                            hr = CreateIDValues(DEVICE_MANUFACTURER_VALUE,
                                                DEVICE_MODEL_VALUE,
                                                DEVICE_FIRMWARE_VERSION_VALUE,
                                                &guidFUID,
                                                &pIDs);
                            CHECK_HR(hr, "Failed to Create the ID value collection");
                        }

                        // Add the PnP ID value collection to the options
                        if (hr == S_OK)
                        {
                            hr = pOptions->SetIPortableDeviceValuesValue(WPD_CLASS_EXTENSION_OPTIONS_DEVICE_IDENTIFICATION_VALUES, pIDs);
                            CHECK_HR(hr, "Failed to set WPD_CLASS_EXTENSION_OPTIONS_DEVICE_IDENTIFICATION_VALUES");
                        }

                        // Add the transport bandwidth (in kilobits per second units) to the options
                        // (0 indicates bandwidth unknown)
                        if (hr == S_OK)
                        {
                            // Set the transport bandwidth (optional)
                            hr = pOptions->SetUnsignedIntegerValue(WPD_CLASS_EXTENSION_OPTIONS_TRANSPORT_BANDWIDTH, 0L);
                            CHECK_HR(hr, "Failed to set WPD_CLASS_EXTENSION_OPTIONS_TRANSPORT_BANDWIDTH");
                        }
                    }
                }
```

## <a name="span-idmultitransportqueuesspanspan-idmultitransportqueuesspanspan-idmultitransportqueuesspanmultitransport-queues"></a><span id="MultiTransport_Queues"></span><span id="multitransport_queues"></span><span id="MULTITRANSPORT_QUEUES"></span>MultiTransport キュー


WpdHelloWorld ドライバーのサンプルでは、WPD シリアライザーからプロセスの Ioctl に、1 つの連続したキューをサポートします。 WpdMultiTransportDriver ドライバーは、2 つのキューをサポートしています。 キューを並列および順次のキュー。 並列のキューが、複数を処理するシーケンシャル キューは、一度に 1 つだけの要求を処理中に I/O の同時要求すると、します。

コードでは、デバイスの到着、 **CDriver::OnDeviceAdd**メソッドは、両方のキューを準備します。 最初の (または既定の) キューは各 IOCTL を処理し、いずれか 2 つ目 (シーケンシャル) のキューに、ドライバーまたは WPD クラスの拡張機能でサポートされている別のキューに転送する並列キューです。

次のコード例には、並列および順次の両方のキューを作成するコードが含まれています。

```ManagedCPlusPlus
        //
        // Create the default queue callback object
        //
        CComPtr<IUnknown> pIUnknown;
        if(S_OK == hr)
        {
            hr = CDefaultQueue::CreateInstance(&pIUnknown);
        }

        //
        // Configure the default queue.
        //
        if(S_OK == hr)
        {
            CComPtr<IWDFIoQueue> pDefaultQueue;
            hr = pIWDFDevice->CreateIoQueue(
                              pIUnknown,
                              TRUE,                         // bDefaultQueue
                              WdfIoQueueDispatchParallel,
                              TRUE,                         // bPowerManaged
                              FALSE,                        // bAllowZeroLengthRequests
                              &pDefaultQueue);
        }
        pIUnknown = NULL;

        //
        // Create the WPD queue callback object
        //
        if(S_OK == hr)
        {
            hr = CQueue::CreateInstance(&pIUnknown);
        }

        //
        // Configure the WPD queue.
        //
        if(S_OK == hr)
        {
            hr = pIWDFDevice->CreateIoQueue(
                              pIUnknown,
                              FALSE,                        // bDefaultQueue
                              WdfIoQueueDispatchSequential,
                              TRUE,                         // bPowerManaged
                              FALSE,                        // bAllowZeroLengthRequests
                              &pWpdBaseDriver->m_pWpdQueue);
        }
```

中に、 **CDriver::OnDeviceAdd** I/O キューの作成を処理するメソッド、両方のキューで機能をサポートするコードがある、 *Queue.cpp*ファイル。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





