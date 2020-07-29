---
title: センサーの永続的な一意識別子を作成する (以前のバージョン)
description: センサーの永続的な一意識別子を作成する (以前のバージョン)
ms.assetid: 09ff583e-6bb5-4812-ae3b-970dac671e39
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff2f246ab8953bd6589a16c23c0e87940d93dacd
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264447"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor-previous-version"></a>センサーの永続的な一意識別子を作成する (以前のバージョン)


ドライバーは、センサーごとに永続的な一意識別子 (PUID) を作成する必要があります。 PUID は、セッション間で格納され、デバイス上のオブジェクトを一意に識別する GUID 値です。 センサープロパティの永続的な一意の ID という名前のプロパティを照会すると、ドライバーは PUID の値を返す必要があり \_ \_ \_ \_ ます。 デバイスに複数のセンサーが含まれている場合は、各センサーに独自の PUID が割り当てられている必要があります。 アプリケーションは、センサー API で[ISensor:: GetID](https://go.microsoft.com/fwlink/p/?linkid=157812)メソッドを呼び出すことによって、この ID を取得できます。

センサーがコンピューターに初めて接続し、後で使用するためにこの値を保存するときに、センサーごとに新しい PUID を作成する必要があります。

ドライバーは、センサークラス拡張が初期化される前に、 [**IPnpCallbackHardware:: On ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)で呼び出されたときなど、PUID を作成または取得する必要があります。 このメソッドは、センサーを表す[Iwdfdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスへのポインターを提供します。 このポインターを使用して、各デバイスの特定のプロパティストアにアクセスできます。

次のコード例では、必要に応じて、PUID を作成、格納、および取得する関数を作成します。

```cpp
// Sets the persistent unique ID property in the WDF property store
// and returns the GUID for use in PortableDeviceValues property bags.
HRESULT CMyDevice::GetUniqueID(__in IWDFDevice* pWdfDevice,
                                            __in LPCWSTR wszSensorID, __out GUID* puid)
{
    HRESULT hr = S_OK;

    // Smart pointer to the WDF property store.
    // This pointer can store or retrieve the ID.
    CComPtr<IWDFNamedPropertyStore> spPropStore;
    if (SUCCEEDED(hr))
    {
        // Create the property store for this device or
        // retrieve the existing one.
        hr = pWdfDevice->RetrieveDevicePropertyStore(NULL, WdfPropertyStoreCreateIfMissing, &spPropStore, NULL);
    }

    if(SUCCEEDED(hr))
    {
        GUID idGuid;

        PROPVARIANT vID;

        // Try to get the PUID value previously stored as a string.
        hr = spPropStore->GetNamedValue(wszSensorID, &vID);
        if (SUCCEEDED(hr))
        {
            // Convert the PUID string to a GUID.
            hr = ::CLSIDFromString(vID.bstrVal, &idGuid);
        }
        else
        {
            // There was no value in the store, so create a new value.
            hr = ::CoCreateGuid(&idGuid);

            if (SUCCEEDED(hr))
            {
                // Convert the GUID to a string.
                LPOLESTR lpszGUID = NULL;
                hr = ::StringFromCLSID(idGuid, &lpszGUID);
                if (SUCCEEDED(hr))
                {
                    // Put the new value into the property store.
                    PropVariantInit(&vID);
                    vID.vt = VT_LPWSTR;
                    vID.pwszVal = lpszGUID;
                    hr = spPropStore->SetNamedValue(wszSensorID, &vID);
                    PropVariantClear(&vID);
                }
            }
        }

        // Return the PUID GUID.
        *puid = idGuid;
    }

    return hr;
}
```

## <a name="related-topics"></a>関連トピック
[センサーの地理位置情報ドライバーのサンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



