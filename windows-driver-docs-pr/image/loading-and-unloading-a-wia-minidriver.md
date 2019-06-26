---
title: WIA ミニドライバーのロードとアンロード
description: WIA ミニドライバーのロードとアンロード
ms.assetid: a5f930c3-f92c-498a-a334-b5eb60fbd61b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93b88277b8eaa89a20f33e9554d091492181cc2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378870"
---
# <a name="loading-and-unloading-a-wia-minidriver"></a>WIA ミニドライバーのロードとアンロード





WIA デバイス ドライバーをインストールした後、WIA サービスを初めて読み込むしようとします。 WIA ミニドライバーの[ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)メソッドは呼び出され、次のタスクを実行する必要があります。

1.  このデバイス ドライバーを初期化するため、呼び出し元の意図を判断する転送モードを確認します。 これは、呼び出すことで、 [ **IStiDeviceControl::GetMyDeviceOpenMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceopenmode)メソッド。

2.  このドライバーを呼び出すことができるように、インストールされているデバイスのポートの名前を取得[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) (Microsoft Windows SDK に記載されている)、デバイスにアクセスする適切なポートでします。 これは、呼び出すことで、 [ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)メソッド。

3.  デバイスのインストール中に書き込まれたデバイス固有のレジストリ設定を読み取ります。 これを使用して行うことができます*hParametersKey*に渡されるパラメーター **IStiUSD::Initialize**します。

WIA サービスの呼び出し、 **IStiUSD::Initialize**メソッド、ドライバーが最初に読み込まれます。 **IStiUSD::Initialize**クライアントは、従来の STI Ddi および呼び出しを使用する場合、メソッドが呼び出されますも、 [ **IStillImage::CreateDevice** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))メソッド。

**IStiUSD::Initialize**メソッドは、WIA ドライバーと使用のデバイスを初期化する必要があります。 WIA ドライバーが格納できる、 **IStiDeviceControl**インターフェイス ポインターに後で必要な場合。 [ **IStiDeviceControl::AddRef** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-addref)メソッドは、このインターフェイスを格納する前に呼び出す必要があります。 インターフェイスを格納する必要がない場合は、それを無視します。 *いない*リリース、 **IStiDeviceControl**インターフェイスが呼び出さない場合**IStiDeviceControl::AddRef**最初。 予期しない結果がある可能性があります。 [IStiDeviceControl COM インターフェイス](istidevicecontrol-com-interface.md)デバイスのポートに関する情報を取得するが必要です。 呼び出しで使用されるポートの名前、 [ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数を呼び出すことによって取得できます、 **IStiDeviceControl::GetMyDevicePortName**メソッド。 デバイスのシリアル ポートなどの共有ポート上のデバイス用のポートを開く**IStiUSD::Initialize**はお勧めしません。 呼び出しでのみ、ポートを開く必要が**IStiUSD::LockDevice**します。 ポートの終了は、高速アクセスを提供する内部的に管理必要があります。 (開閉**IStiUSD::LockDevice**と**IStiUSD::UnLockDevice**非常に効率的ではありません。 **CreateFile**低速で、ユーザーに応答しないように表示されるデバイス遅延が発生することができます)。

WIA ドライバーは、複数をサポートできない場合[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) 、同じデバイスのポートで呼び出し、 **IStiDeviceControl::GetMyDeviceOpenMode**メソッドを呼び出す必要があります。

WIA ドライバーは、STI に返されたモード値を確認する必要があります\_デバイス\_作成\_データは、フラグを設定し、それに応じて、ポートを開きます。

かどうか、デバイスのポートを開いてへの呼び出し[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)使用する必要があります。 ポート、ファイルを開くときに\_フラグ\_OVERLAPPED フラグを使用する必要があります。 これにより、デバイスにアクセスするときに使用される (Windows SDK のドキュメントで説明)、OVERLAPPED 構造体です。 オーバー ラップ I/O を使用すると、ハードウェアに応答性の高いアクセスを制御ができます。 WIA ドライバーを呼び出すことができます、問題が検出されると、 **CancelIo** (Windows SDK のドキュメントで説明) を現在のすべてのハードウェア アクセスを停止します。

次の例の実装を示しています、 **IStiUSD::Initialize**メソッド。

```cpp
STDMETHODIMP CWIADevice::Initialize(
  PSTIDEVICECONTROL   pIStiDeviceControl,
  DWORD               dwStiVersion,
  HKEY                hParametersKey)
{
  if (!pIStiDeviceControl) {
      return STIERR_INVALID_PARAM;
  }

  HRESULT hr = S_OK;

  //
  // Get the mode of the device to check why we were created.  status, data, or both...
  //

  DWORD dwMode = 0;
  hr = pIStiDeviceControl->GetMyDeviceOpenMode(&dwMode);
  if(FAILED(hr)){
      return hr;
  }

  if(dwMode & STI_DEVICE_CREATE_DATA)
  {
      //
      // device is being opened for data
      //
  }

  if(dwMode & STI_DEVICE_CREATE_STATUS)
  {
      //
      // device is being opened for status
      //
  }

  if(dwMode & STI_DEVICE_CREATE_BOTH)
  {
      //
      // device is being opened for both data and status
      //
  }

  //
  // Get the name of the device port to be used in a call to CreateFile().
  //

  WCHAR szDevicePortNameW[MAX_PATH];
  memset(szDevicePortNameW,0,sizeof(szDevicePortNameW));

  hr = pIStiDeviceControl->GetMyDevicePortName(szDevicePortNameW,
                                            sizeof(szDevicePortNameW)/sizeof(WCHAR));
  if(FAILED(hr)) {
      return hr;
  }

  //
  // Open kernel-mode device driver. Use the FILE_FLAG_OVERLAPPED flag 
  // for proper cancellation
  // of kernel-mode operations and asynchronous file IO. 
  //  The CancelIo() call will function properly if this flag is used.
  //  It is recommended to use this flag.
  //

  m_hDeviceDataHandle = CreateFileW(szDevicePortNameW,
                                   GENERIC_READ | GENERIC_WRITE, // Access mask
                                   0,                            // Share mode
                NULL,                         // SA
                                   OPEN_EXISTING,                // Create disposition
                                   FILE_ATTRIBUTE_SYSTEM|FILE_FLAG_OVERLAPPED,
                                   NULL );

  m_dwLastOperationError = ::GetLastError();

  hr = (m_hDeviceDataHandle != INVALID_HANDLE_VALUE) ?
              S_OK : MAKE_HRESULT(SEVERITY_ERROR,FACILITY_WIN32,m_dwLastOperationError);

  if (FAILED(hr)) {
      return hr;
  }

  //
  // Open DeviceData section to read driver specific information
  //

  HKEY hKey = hParametersKey;
  HKEY hOpenKey = NULL;
  if (RegOpenKeyEx(hKey,                     // handle to open key
                   TEXT("DeviceData"),       // address of name of subkey to open
                   0,                        // options (must be NULL)
                   KEY_QUERY_VALUE|KEY_READ, // just want to QUERY a value
                   &hOpenKey                 // address of handle to open key
     ) == ERROR_SUCCESS) {

      //
      // This is where you read registry entries for your device.
      // The DeviceData section is the proper place to put this 
      // information. Information about your device should
      // have been written using the WIA device's .INF installation
      // file.
      // You can access this information from this location in the
      // Registry. The WIA service owns the hParameters HKEY. 
      // DO NOT CLOSE THIS KEY. Always close any HKEYS opened by
      //  this WIA driver after you are finished.
      //

      //
      // close registry key when finished, reading DeviceData information.
      //

      RegCloseKey(hOpenKey);
  } else {
      return E_FAIL;
  }
  return hr;
}
```

サービス呼び出しで WIA [ **IStiUSD::GetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getcapabilities)呼び出しに成功した後、 **IStiUSD::Initialize**メソッド。 **IStiUSD::GetCapabilities**提供し、 [ **STI\_USD\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/ns-stiusd-_sti_usd_caps) STI バージョンについては、WIA をサポートするフラグを示す (ビット フラグ構造体ドライバーの機能)、そのイベントの要件。

次の例の実装を示しています。 **IStiUSD::GetCapabilities**します。

```cpp
/********************************************************************\
* CWIADevice::GetCapabilities
* Remarks:
* This WIA driver sets the following capability flags:
* 1. STI_GENCAP_WIA - This driver supports WIA
* 2. STI_USD_GENCAP_NATIVE_PUSHSUPPORT - This driver supports push
*    buttons
* 3. STI_GENCAP_NOTIFICATIONS - This driver requires the use of 
*    interrupt events.
*
\********************************************************************/

STDMETHODIMP CWIADevice::GetCapabilities(PSTI_USD_CAPS pUsdCaps)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pUsdCaps) {
      return E_INVALIDARG;
  }

  memset(pUsdCaps, 0, sizeof(STI_USD_CAPS));
  pUsdCaps->dwVersion     = STI_VERSION;    // STI version
  pUsdCaps->dwGenericCaps = STI_GENCAP_WIA| // WIA support
                            STI_USD_GENCAP_NATIVE_PUSHSUPPORT| // button support
                            STI_GENCAP_NOTIFICATIONS; // interrupt event support
  return S_OK;
}
```

 

 




