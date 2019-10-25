---
title: センサーイベントの発生
description: センサーイベントの発生
ms.assetid: a6e428f8-1613-4e8d-813d-5a54824dab82
keywords:
- センサーイベント
- イベント ハンドラー
- データ更新イベント
- センサーデータ更新イベント
- 状態変更イベント
- センサーの状態変更イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eec9a30bf3b174b4f6d6b5282418315047480b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842527"
---
# <a name="raising-sensor-events"></a>センサーイベントの発生


センサーイベントの動作の詳細については、「[センサードライバーイベントについ](about-sensor-driver-events.md)て」を参照してください。

次のコード例は、データ更新イベントと状態変更イベントを発生させるクラスを示しています。 クラスには、 **Csensormanager**という名前が付けられます。

### <a name="member-variables"></a>メンバー変数

このクラスは、次のメンバー変数を定義します。

```c
// Smart pointer to the sensor class extension object.
CComPtr<ISensorClassExtension> m_spSensorCXT;

// Pointer to the callback class that the class extension calls.
CSensorDdi* m_pDdi;

// The event thread handle
HANDLE m_hEventThread;

// Handle to an event used to signal the thread to close.
HANDLE m_hCloseThread;

// The current report interval.
DWORD m_dwInterval;
```

### <a name="global-variables"></a>グローバル変数

ドライバーは、このクラスによって使用される次のグローバル変数を定義します。

```c
// Sensor ID
static const LPWSTR g_wszSensorID = L"My Sensor ID";

// Default event interval
static const DWORD g_dwDefaultInterval = 1000; // one second
```

### <a name="lifetime-management"></a>有効期間の管理

[ISensorDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nn-sensorsclassextension-isensordriver)を実装する CSensorDdi という名前のコールバッククラスは、最初のクライアントがイベントをサブスクライブするときに CSampleEvents イベントクラスのインスタンスを作成します。 コールバッククラスは、クライアントがイベントにサブスクライブされなくなったときに CSampleEvents インスタンスを破棄します。

CSampleEvents は CSensorDdi にコールバックし、 [**ISensorDriver:: OnGetDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields)など、クラス拡張で使用されるのと同じメソッドを使用して、最新のデータを取得します。

次のコード例には、CSampleEvents イベントクラスのメソッドの実装が含まれています。

```c
CSampleEvents::CSampleEvents()
{
    // Initialize member variables.
    m_hEventThread = NULL;
    m_hCloseThread = NULL;
    m_dwInterval = g_dwDefaultInterval;
};

CSampleEvents::~CSampleEvents()
{
};

// Initialize
// Sets the pointers to the class extension and the callback class.
HRESULT CSampleEvents::Initialize(ISensorClassExtension *pSensorCXT, CSensorDdi* pDdi)
{
    HRESULT hr = S_OK;

    if(NULL == pSensorCXT || NULL == pDdi)
    {
        return E_POINTER;
    }

    // Cache the pointers to the class extension and DDI callback class.
    m_spSensorCXT = pSensorCXT;
    m_pDdi = pDdi;

    // Create the event used to close the thread.
    m_hCloseThread = ::CreateEvent(NULL, FALSE, FALSE, TEXT("CloseThreadEvent"));

    if(NULL == m_hCloseThread)
    {
        hr = E_UNEXPECTED;
    }

    if(SUCCEEDED(hr))
    {
        m_hEventThread = ::CreateThread(NULL,   // Cannot be inherited by child process
                     0,                                       // Default stack size
                     &CSampleEvents::_EventThreadProc,     // Thread proc
                     (LPVOID)this,                            // Thread proc argument
                     0,                                       // Starting state = running
                     NULL);                                   // No thread identifier

        if(NULL == m_hEventThread)
        {
            hr = E_UNEXPECTED;
        }
    }

    return hr;
};

// Uninitializes the event class.
HRESULT CSampleEvents::Uninitialize()
{
    HRESULT hr = S_OK;

    // Stop the event thread.
    ::SetEvent(m_hCloseThread);

    // Wait for the thread to end.
    ::WaitForSingleObject(m_hEventThread, INFINITE);

    if (NULL != m_hEventThread)
    {
        CloseHandle(m_hEventThread);
        m_hEventThread = NULL;
    }

    if(NULL != m_hCloseThread)
    {
        CloseHandle(m_hCloseThread);
        m_hCloseThread = NULL;
    }

    // After Uninitialize, clients must call Initialize to set new pointers.
    m_pDdi = NULL;
    m_spSensorCXT.Release();

    return hr;
};

// Post a state change event
HRESULT CSampleEvents::PostStateEvent()
{
    HRESULT hr = (NULL == m_spSensorCXT) ? E_UNEXPECTED : S_OK ;

    if (SUCCEEDED(hr))
    {
        SensorState st;
        hr = m_pDdi->GetSensorState(&st);

        if (SUCCEEDED(hr))
        {
            // Post the state change event.
            hr = m_spSensorCXT->PostStateChange(g_wszSensorID, st);
        }
    }

    return hr;
}

// Post a data updated event
HRESULT CSampleEvents::PostDataEvent(IPortableDeviceValues* pValues)
{
    HRESULT hr = (NULL == m_spSensorCXT) ? E_UNEXPECTED : S_OK ;

    if (SUCCEEDED(hr))
    {
        CComPtr<IPortableDeviceValuesCollection> spValuesCollection;
        hr = spValuesCollection.CoCreateInstance(CLSID_PortableDeviceValuesCollection);

        if (SUCCEEDED(hr))
        {
            hr = spValuesCollection->Add(pValues);

            if (SUCCEEDED(hr))
            {
                hr = m_spSensorCXT->PostEvent(g_wszSensorID, spValuesCollection);
            }
        }
    }

    return hr;
}
```

### <a name="thread-procedure"></a>スレッドプロシージャ

次のコード例は、CSampleEvents クラスを使用してデータ更新イベントを発生させるスレッドプロシージャを示しています。

```c
DWORD WINAPI CSampleEvents::_EventThreadProc(__in LPVOID pvData)
{
// Cast the argument to the correct type.
 CSampleEvents* pThis = static_cast<CSampleEvents*>(pvData);

// New threads must always CoInitialize...
    HRESULT hr = CoInitializeEx(NULL, COINIT_MULTITHREADED);

    if (SUCCEEDED(hr))
    {
        // Wait loop timed to use current report interval.
        while (WAIT_TIMEOUT == WaitForSingleObject(pThis->m_hCloseThread, pThis->m_dwInterval))
        {
            if(NULL == pThis->m_pDdi ||
               NULL == pThis->m_spSensorCXT.p)
            {
                Trace(TRACE_LEVEL_ERROR, "%!FUNC!: NULL pointer in helper function.");
                hr = E_POINTER;
            }

            CComPtr<IPortableDeviceValues> spEventParams;
            CComPtr<IPortableDeviceKeyCollection> spKeys;

            if(SUCCEEDED(hr))
            {
                // Use the Ddi class to create the key collection.
                hr = pThis->m_pDdi->OnGetSupportedDataFields(g_wszSensorID, &spKeys);
            }

            if(SUCCEEDED(hr))
            {
                CComPtr<IWDFFile> spTemp;

                // Get the data fields.
                // Note that we're using a DDI call as a helper function, here.
                // Setting the first parameter to NULL will be problematic if you
                // choose to track or use IWDFFile pointers in OnGetDataFields.
                // This sample does not do so, therefore this is a safe thing to do
                // in this code.
                hr = pThis->m_pDdi->OnGetDataFields(spTemp, g_wszSensorID, spKeys,
                                                              &spEventParams);
            }

            if(SUCCEEDED(hr))
            {
                // Add the data event property key.
                hr = spEventParams->SetGuidValue(SENSOR_EVENT_PARAMETER_EVENT_ID,
                                                                SENSOR_EVENT_DATA_UPDATED);

                if(SUCCEEDED(hr))
                {
                    // Post the event.
                    hr = pThis->PostDataEvent(spEventParams);
                }
            }
        }
    }

 CoUninitialize();

    return SUCCEEDED(hr) ? 0 : 1;
};
```

## <a name="related-topics"></a>関連トピック
[センサーの地理位置情報ドライバーのサンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



