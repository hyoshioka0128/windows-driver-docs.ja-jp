---
Description: MultiTransport デバイスのサポート
title: MultiTransport デバイスのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663b9a3f84ad152d90b7e7825be85b6fd88899af
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968300"
---
# <a name="multitransport-device-support"></a>MultiTransport デバイスのサポート


WpdMultiTransportDriver サンプルは WpdHelloWorldDriver に基づいており、元のドライバーのソースコードのほとんどは変更されません。 特に、オブジェクトの列挙、プロパティ、および機能をサポートするコードには、変更やリビジョンがほとんど含まれていません。

WpdMultiTransportDriver のコードのリビジョンは、デバイスの到着と i/o キューという2つの主な領域に表示されます。 デバイスの到着をサポートするコードは、*デバイス .cpp*と*ドライバー .cpp*の2つのファイルにあります。 I/o キューをサポートするコードについては、「*ドライバー .cpp*と*キュー .cpp* 」を参照してください。

## <a name="span-idmultitransport_device-arrivalspanspan-idmultitransport_device-arrivalspanspan-idmultitransport_device-arrivalspanmultitransport-device-arrival"></a><span id="Multitransport_Device-Arrival"></span><span id="multitransport_device-arrival"></span><span id="MULTITRANSPORT_DEVICE-ARRIVAL"></span>Multitransport デバイス-到着


デバイス到着コードは、 **Cdevice:: on(** *.cpp*ファイル) メソッドと**Cdevice:: Onpreparehardware**メソッド ( *Driver. .cpp*ファイル) にあります。このメソッドには、

**Cdevice:: onモジュール**のメソッドのコードは、WPD クラス拡張を初期化する前に、次のタスクを完了します。 (最後の3つのタスクは、WPD クラス拡張に渡されるオプションパラメーターを設定します)。

デバイスインターフェイスの状態が変化したときに、 **ioctl \_ 複合 \_ トランスポート \_ 要求の ioctl**を WPD クラスインストーラーから正しく受信できるように、並列キューが必要です。 2つ目のキューでは、トランスポートドライバーで別の (たとえば、非並列) ディスパッチモードを使用できます。 WUDF では一度に1つの要求のみが許可されるため、順次キューは管理が簡単です。 ただし、WPD ドライバーが複数の要求を並列処理できる場合、セカンダリキューは必要ありません。

**タスク**: 説明

**機能的な一意識別子 (FUTEX id) を作成します。**: futex id は、初期化中にドライバーが WPD クラス拡張に渡すグローバル一意識別子 (GUID) 値です。 (クラス拡張では、この FUTEX ID が各トランスポートに関連付けられます)。

** **IQueueCallbackDeviceIoControl**インターフェイスへのポインターを取得します。**: ドライバーは、このポインターを使用して、非 WPD ioctl をクラス拡張に転送します。

**Multitransport モードオプションを有効にします。**: このオプションは、multitransport フレームワークを設定する必要があることを WPD クラス拡張に通知します。

**必要なプラグアンドプレイ (PnP) の値を設定します。** これらの値は、multitransport フレームワークを構成するために使用されます。

**現在のトランスポート帯域幅を設定します。**: この値は、クラス拡張と複合ドライバー (*WpdComp.dll*) によって使用されます。 複合ドライバーは拡張から値を取得し、それを使用して、複数のトランスポートがアクティブな場合の最適なトランスポートを決定します。


 

**Cdevice:: on、hardware**メソッドの次のコード例は、サンプルドライバーが機能の一意識別子 (futex id) を作成した方法を示しています。 この GUID を作成する前に、コメントを必ず確認してください。

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

**Cdevice:: OnIQueueCallbackDeviceIoControl hardware**メソッドからの次のコード例では、前の表の3つの残りのタスク**IQueueCallbackDeviceIoControl**を示します (マルチトランスポートモードを有効にし、PnP 値と現在の帯域幅を設定します)。

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

## <a name="span-idmultitransport_queuesspanspan-idmultitransport_queuesspanspan-idmultitransport_queuesspanmultitransport-queues"></a><span id="MultiTransport_Queues"></span><span id="multitransport_queues"></span><span id="MULTITRANSPORT_QUEUES"></span>MultiTransport キュー


WpdHelloWorld ドライバーサンプルでは、WPD シリアライザーから Ioctl を処理するための単一のシーケンシャルキューがサポートされています。 WpdMultiTransportDriver ドライバーでは、並列キューと順次キューという2つのキューがサポートされています。 並列キューは、同時に複数の i/o 要求を処理しますが、順次キューは一度に1つの要求のみを処理します。

**Cdriver:: OnDeviceAdd**メソッドのデバイス到着コードは、両方のキューを準備します。 最初の (または既定の) キューは、各 IOCTL を処理し、ドライバーの2番目の (順次) キューに転送するか、または WPD クラス拡張でサポートされている別のキューに転送する並列キューです。

次のコード例には、並列キューと順次キューの両方を作成するコードが含まれています。

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

**Cdriver:: OnDeviceAdd**メソッドは、i/o キューの作成を処理しますが、両方のキューの機能をサポートするコードは、キューの *.cpp*ファイルにあります。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





