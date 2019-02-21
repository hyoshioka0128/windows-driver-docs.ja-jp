---
Description: Handling Access Control
title: 処理へのアクセス制御
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31fdd53b47f4d7e762368ca571209967beb9e23a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552905"
---
# <a name="handling-access-control"></a>処理へのアクセス制御


WPD ドライバーでは、WPD コマンドのペイロードに I/O マネージャーが適切な ACL の確認を実行するために適切な I/O 制御コード (IOCTL) とが送信されたことを確認する必要があります。 すべてのドライバーでは、この検証を実行する必要がありますので、WPD には、プロセスを自動化するマクロが用意されています。

これらのマクロは、ファイルで定義されている*PortableDevice.h*します。 これらは、次の表で説明します。

| マクロ                                            | 説明                                                                                                                                  |
|--------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 開始\_WPD\_コマンド\_アクセス\_マップ                 | コマンド access のテーブルの先頭を定義します。                                                                                           |
| 宣言\_確認\_WPD\_コマンド\_アクセス            | IOCTL で適切なアクセス フラグで指定された WPD コマンドが送信されることを確認するために使用する関数のインスタンスを宣言します。 |
| 宣言\_WPD\_標準\_コマンド\_アクセス\_エントリ | 含まれるすべての標準の WPD コマンドのエントリを宣言します*PortableDevice.h*します。                                                 |
| 終了\_WPD\_コマンド\_アクセス\_マップ                   | コマンドへのアクセスのテーブルの末尾を定義します。                                                                                                 |
| \_WPD\_IOCTL                                   | 特定の IOCTL が WPD に固有かどうかを判断します。                                                                                         |
| 確認\_WPD\_コマンド\_アクセス                     | 特定の IOCTL とドライバーのモジュールのいずれかで定義されているコマンド アクセス テーブルに対しては、そのパラメーターを比較します。                     |
| WPD\_コマンド\_アクセス\_エントリ                      | コマンドへのアクセスの表に、カスタム エントリを追加します。                                                                                             |

 

サンプル ドライバーでアクセス コントロールの検証が実行される、 **CQueue::OnDeviceIoControl**と**CQueue::ProcessWpdMessage**メソッド。 これらのメソッドがある、 *Queue.cpp*ファイル。 さらに、このファイルには、WPD だけでなく、カスタムの Ioctl とそのアクセス レベルを一覧表示するコマンド アクセス テーブルが含まれています。

```ManagedCPlusPlus
// Add table used to lookup the Access required for Wpd Commands
BEGIN_WPD_COMMAND_ACCESS_MAP(g_WpdCommandAccessMap)
    DECLARE_WPD_STANDARD_COMMAND_ACCESS_ENTRIES
    // Add any custom commands here e.g.
    // WPD_COMMAND_ACCESS_ENTRY(MyCustomCommand, WPD_COMMAND_ACCESS_READWRITE)
END_WPD_COMMAND_ACCESS_MAP

// This allows driver developers to use VERIFY_WPD_COMMAND_ACCESS to check command access function for us.
DECLARE_VERIFY_WPD_COMMAND_ACCESS;
```

**OnDeviceIoControl**メソッドは、IS を使用して\_WPD\_IOCTL マクロ WPD Ioctl を識別するためにして呼び出すことによって処理、 **ProcessWpdMessage**メソッド。

```ManagedCPlusPlus
STDMETHODIMP_ (void)
CQueue::OnDeviceIoControl(
        /* [in] */ IWDFIoQueue*     pQueue,
        /* [in] */ IWDFIoRequest*   pRequest,
        /* [in] */ ULONG            ControlCode,
        /* [in] */ SIZE_T           InputBufferSizeInBytes,
        /* [in] */ SIZE_T           OutputBufferSizeInBytes
        )
{
    HRESULT hr              = S_OK;
    DWORD   dwBytesWritten  = 0;

    if(IS_WPD_IOCTL(ControlCode))
    {
        BYTE*       pInputBuffer         = NULL;
        SIZE_T      cbInputBuffer        = 0;
        BYTE*       pOutputBuffer        = NULL;
        SIZE_T      cbOutputBuffer       = 0;
        ContextMap* pClientContextMap    = NULL;
        CComPtr<IWDFMemory> pMemoryIn;
        CComPtr<IWDFMemory> pMemoryOut;
        CComPtr<IWDFDevice> pDevice;
        CComPtr<IWDFFile>   pFileObject;

        //
        // Get input memory buffer, the memory object is always returned even if the
        // underlying buffer is NULL
        //
        pRequest->GetInputMemory(&pMemoryIn);
        pInputBuffer = (BYTE*) pMemoryIn->GetDataBuffer(&cbInputBuffer);

        //
        // Get output memory buffer, the memory object is always returned even if the
        // underlying buffer is NULL
        //
        pRequest->GetOutputMemory(&pMemoryOut);
        pOutputBuffer = (BYTE*) pMemoryOut->GetDataBuffer(&cbOutputBuffer);

        
        // Get the Context map for this client
        pRequest->GetFileObject(&pFileObject);
        if (pFileObject != NULL)
        {
            hr = pFileObject->RetrieveContext((void**)&pClientContextMap);
            CHECK_HR(hr, "Failed to get Contextmap from WDF File Object");
        }

        if (hr == S_OK)
        {
            // Get the device object
            pQueue->GetDevice(&pDevice );
            hr = ProcessWpdMessage(ControlCode,
                                   pClientContextMap,
                                   pDevice,
                                   pInputBuffer,
                                   (DWORD)cbInputBuffer,
                                   pOutputBuffer,
                                   (DWORD)cbOutputBuffer,
                                   &dwBytesWritten);
        }

   
    }
    else
    {
        hr = E_UNEXPECTED;
        CHECK_HR(hr, "Received invalid/unsupported IOCTL code &#39;0x%lx&#39;",ControlCode);
    }

    // Complete the request
    if (hr == S_OK)
    {
        pRequest->CompleteWithInformation(hr, dwBytesWritten);
    }
    else
    {
        pRequest->Complete(hr);
    }

    return;
}
```

**ProcessWpdMessage**メソッドは、検証を使用して\_WPD\_コマンド\_の先頭で IOCTL とコマンド パラメーター コマンド アクセスに対してテーブルをチェックするアクセス マクロが定義されています。*Queue.cpp*します。

```ManagedCPlusPlus
HRESULT CQueue::ProcessWpdMessage(
    ULONG       ControlCode,
    ContextMap* pClientContextMap,
    IWDFDevice* pDevice,
    PVOID       pInBuffer,
    ULONG       ulInputBufferLength,
    PVOID       pOutBuffer,
    ULONG       ulOutputBufferLength,
    DWORD*      pdwBytesWritten)
{
    HRESULT                        hr = S_OK;
    CComPtr<IPortableDeviceValues> pParams;

    CComPtr<IPortableDeviceValues> pResults;

    CComPtr<WpdBaseDriver>         pWpdBaseDriver;

    if (hr == S_OK)
    {
        hr = m_pWpdSerializer->GetIPortableDeviceValuesFromBuffer((BYTE*)pInBuffer,
                                                                  ulInputBufferLength,
                                                                  &pParams);
        CHECK_HR(hr, "Failed to deserialize command parameters from input buffer");
    }

    // Verify that the command was sent with the appropriate access
    if (hr == S_OK)
    {
        hr = VERIFY_WPD_COMMAND_ACCESS(ControlCode, pParams, g_WpdCommandAccessMap);
        CHECK_HR(hr, "Wpd Command was sent with incorrect access flags");
    }

}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





