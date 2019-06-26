---
title: センサーの永続的な一意の識別子を作成します。
description: センサーの永続的な一意の識別子を作成します。
ms.assetid: 09ff583e-6bb5-4812-ae3b-970dac671e39
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 766ff37235b6beb096470558d18656f81e03c18f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360692"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor"></a>センサーの永続的な一意の識別子を作成します。


ドライバーは、永続的な一意識別子 (PUID) 各センサーを作成する必要があります。 PUID は、セッション間で格納され、デバイス上のオブジェクトを一意に識別する GUID 値です。 ドライバーは、センサーをという名前のプロパティに対してクエリを実行時に、PUID の値を返す必要があります\_プロパティ\_持続\_UNIQUE\_id。 デバイスに複数のセンサーが含まれている場合各センサーは、独自の PUID 割り当てる必要があります。 アプリケーションは呼び出すことでこの ID を取得することができます、 [ISensor::GetID](https://go.microsoft.com/fwlink/p/?linkid=157812)センサー API のメソッド。

センサーが最初に、コンピューターに接続するときに、各センサーの新しい PUID を作成し、し、後で使用するためには、この値を格納する必要があります。

ドライバーを作成またはセンサー クラスの拡張機能が初期化される前に、たとえば呼び出された場合は、PUID を取得する必要があります[ **IPnpCallbackHardware::OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)します。 このメソッドへのポインターを提供する、 [IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)センサーを表すインターフェイスです。 このポインターを使用して、各デバイスの特定のプロパティ ストアにアクセスすることができます。

次のコード例は、必要に応じて、作成、格納、および、PUID を取得する関数を作成します。

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
[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



