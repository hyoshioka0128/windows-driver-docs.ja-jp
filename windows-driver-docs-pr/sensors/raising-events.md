---
title: センサー イベントを発生させる
description: センサー イベントを発生させる
ms.assetid: a6e428f8-1613-4e8d-813d-5a54824dab82
keywords:
- センサー イベント
- イベント ハンドラー (event handler)
- データ更新イベント
- センサー データの更新イベント
- 状態変更イベント
- センサーの状態変更イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e49f2feb782430b31fcdc110d4a231ffa4f5408
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348817"
---
# <a name="raising-sensor-events"></a>センサー イベントを発生させる


センサー イベントを使用する方法についての詳細については、次を参照してください。[センサー ドライバー イベントについて](about-sensor-driver-events.md)します。

次のコード例では、データ更新、および状態変更イベントを発生させるクラスを示します。 クラスの名前は**CSensorManager**します。

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

ドライバーは、このクラスで使用される次のグローバル変数を定義します。

```c
// Sensor ID
static const LPWSTR g_wszSensorID = L"My Sensor ID";

// Default event interval
static const DWORD g_dwDefaultInterval = 1000; // one second
```

### <a name="lifetime-management"></a>有効期間管理

コールバック クラスを実装する、CSensorDdi をという名前[ISensorDriver](https://msdn.microsoft.com/library/windows/hardware/ff545566)、最初のクライアントがイベントにサブスクライブするときに、CSampleEvents イベント クラスのインスタンスを作成します。 コールバック クラスは、クライアントは不要になったイベントをサブスクライブしている場合、CSampleEvents インスタンスを破棄します。

CSampleEvents にコールバックでは、最新のデータを取得する CSensorDdi など、クラスの拡張が使用する同じメソッドを使用して[ **ISensorDriver::OnGetDataFields**](https://msdn.microsoft.com/library/windows/hardware/ff545607)します。

次のコード例には、CSampleEvents イベント クラスのメソッドの実装が含まれています。

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

### <a name="thread-procedure"></a>スレッド処理

次のコード例では、データ更新イベントを発生させる CSampleEvents クラスを使用するスレッド プロシージャを示します。

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
[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



