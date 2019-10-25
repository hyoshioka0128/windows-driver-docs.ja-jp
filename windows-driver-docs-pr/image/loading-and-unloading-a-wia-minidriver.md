---
title: WIA ミニドライバーのロードとアンロード
description: WIA ミニドライバーのロードとアンロード
ms.assetid: a5f930c3-f92c-498a-a334-b5eb60fbd61b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2cfab2b3e58b8afe9c0059292afb26040a06c87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840788"
---
# <a name="loading-and-unloading-a-wia-minidriver"></a>WIA ミニドライバーのロードとアンロード





WIA デバイスドライバがインストールされた後、WIA サービスは初めてそのドライバを読み込もうとします。 WIA ミニドライバーの[**Ib usd:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)メソッドが呼び出され、次のタスクを実行する必要があります。

1.  転送モードを確認して、このデバイスドライバーを初期化するための呼び出し元の意図を判断します。 これを行うには、 [**Istidevicecontrol:: GetMyDeviceOpenMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceopenmode)メソッドを呼び出します。

2.  インストールされているデバイスのポート名を取得します。これにより、このドライバーは、デバイスにアクセスするための適切なポートで[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) (Microsoft Windows SDK に記載されている) を呼び出すことができるようになります。 これを行うには、 [**Istidevicecontrol:: GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)メソッドを呼び出します。

3.  デバイスのインストール中に書き込まれたデバイス固有のレジストリ設定を読み取ります。 これを行うには、 *IhParametersKey* **:: Initialize**に渡されたパラメーターを使用します。

ドライバーが最初に読み込まれるときに、WIA サービスは**Ib usd:: Initialize**メソッドを呼び出します。 **IIStillImage:: Initialize**メソッドは、クライアントがレガシ STI DDIs を使用し、 [ **:: CreateDevice**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))メソッドを呼び出す場合にも呼び出されます。

**I、usd:: Initialize**メソッドは、使用するために、WIA ドライバーとデバイスを初期化する必要があります。 後で必要になったときに、WIA ドライバーは**Iの Devicecontrol**インターフェイスを格納できます。 このインターフェイスを格納する前に、 [**Iの Devicecontrol:: AddRef**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-addref)メソッドを呼び出す必要があります。 インターフェイスを格納する必要がない場合は、そのインターフェイスを無視します。 **I-devicecontrol:: AddRef**を最初に呼び出していない場合は、 **iの devicecontrol**インターフェイス*を解放しないでください。* これにより、予測できない結果が生じる可能性があります。 デバイスのポートに関する情報を取得するには、 [Iの Devicecontrol COM インターフェイス](istidevicecontrol-com-interface.md)が必要です。 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数の呼び出しで使用されるポート名は、 **Istidevicecontrol:: GetMyDevicePortName**メソッドを呼び出すことによって取得できます。 シリアルポートデバイスなどの共有ポートにあるデバイスの場合、 **i、us:: Initialize**でポートを開くことはお勧めしません。 このポートは、 **I、usd:: LockDevice**の呼び出しでのみ開く必要があります。 高速アクセスを提供するために、ポートの終了を内部で制御する必要があります。 ( **I、usd:: LockDevice**および**iUnLockDevice Usd::** での開始と終了は非常に非効率的です。 **CreateFile**を使用すると、デバイスの遅延が発生し、ユーザーに応答しなくなることがあります。

WIA ドライバーが同じデバイスポートで複数の[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)呼び出しをサポートできない場合は、 **iGetMyDeviceOpenMode**メソッドを呼び出す必要があります。

WIA ドライバーは、\_データフラグを作成\_、STI\_デバイスの返されたモード値を確認し、それに応じてポートを開く必要があります。

デバイスのポートを開く必要がある場合は、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)の呼び出しを使用する必要があります。 ポートを開くときに、ファイル\_フラグ\_重複フラグを使用する必要があります。 これにより、デバイスにアクセスするときに、(Windows SDK のドキュメントで説明されている) オーバーラップ構造を使用できるようになります。 重複 i/o を使用すると、ハードウェアへの応答性の高いアクセスを制御できます。 問題が検出されると、WIA ドライバーは**CancelIo** (Windows SDK のドキュメントで説明されている) を呼び出して、現在のすべてのハードウェアアクセスを停止することができます。

次の例は、 **Ib usd:: Initialize**メソッドの実装を示しています。

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

**Ib usd:: Initialize**メソッドの呼び出しが成功すると、WIA サービスは[**ib Usd:: getcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)を呼び出します。 次に、 **i、usd:: GetCapabilities**は、sti のバージョン情報、WIA サポートフラグ (ドライバー機能を示すビットフラグ)、およびすべてのイベント要件を含む、 [ **\_USD\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/ns-stiusd-_sti_usd_caps)構造体を提供します。

次の例は、 **I、usd:: GetCapabilities**の実装を示しています。

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

 

 




