---
Description: UMDF ベースの USB クライアント ドライバーのソース コードについて説明します。
title: USB クライアント ドライバー コードの構造 (UMDF)
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: e12fc7464e54cde537320794d4b5c2a5f5c31907
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815109"
---
# <a name="understanding-the-usb-client-driver-code-structure-umdf"></a>USB クライアント ドライバー コード構造 (UMDF) を理解します。


このトピックでは、UMDF に基づく USB クライアント ドライバーのソース コードについて学習します。 コード例は、によって生成される、 **USB ユーザー モード ドライバー** Microsoft Visual Studio 2019 に含まれているテンプレートです。 テンプレート コードでは、Active Template Library (ATL) を使用して、COM インフラストラクチャを生成します。 ATL と、クライアント ドライバーで COM 実装の詳細については、ここで説明しません。

UMDF のテンプレート コードを生成する方法については、次を参照してください。 [、最初の USB クライアント ドライバー (UMDF) を書き込む方法](implement-driver-entry-for-a-usb-driver--umdf-.md)します。 テンプレート コードは、これらのセクションについて説明します。

-   [ドライバーのコールバックのソース コード](#driver-callback-source-code)
-   [デバイスのコールバックのソース コード](#device-callback-source-code)
-   [キュー ソース コード](#queue-source-code)
-   [ドライバーのエントリのソース コード](#driver-entry-source-code)

テンプレート コードの詳細を説明する前に、UMDF ドライバーの開発に関連するヘッダー ファイル (Internal.h) 内のいくつかの宣言を見てみましょう。

Internal.h には、Windows Driver Kit (WDK) で含まれている、これらのファイルが含まれています。

```ManagedCPlusPlus
#include "atlbase.h"
#include "atlcom.h"

#include "wudfddi.h"
#include "wudfusb.h"
```

Atlbase.h と atlcom.h ATL サポートの宣言が含まれます。 クライアント ドライバーによって実装される各クラス実装 ATL クラスのパブリック CComObjectRootEx します。

Wudfddi.h は常に UMDF ドライバーの開発に含まれています。 ヘッダー ファイルには、さまざまな宣言とメソッドおよび UMDF ドライバーをコンパイルする必要のある構造体の定義が含まれています。

Wudfusb.h には、UMDF 構造と、フレームワークによって提供される USB I/O ターゲット オブジェクトと通信するために必要なメソッドの宣言および定義が含まれています。

Internal.h の次のブロックは、デバイス インターフェイスの GUID 定数を宣言します。 アプリケーションは、この GUID を使用して、使用して、デバイスを識別するハンドルを開く**SetupDiXxx** Api。 GUID は、フレームワークは、デバイス オブジェクトを作成した後に登録されます。

```ManagedCPlusPlus
// Device Interface GUID
// f74570e5-ed0c-4230-a7a5-a56264465548

DEFINE_GUID(GUID_DEVINTERFACE_MyUSBDriver_UMDF_,
    0xf74570e5,0xed0c,0x4230,0xa7,0xa5,0xa5,0x62,0x64,0x46,0x55,0x48);
```

次の部分では、トレース マクロとトレース GUID を宣言します。 注トレース GUID。これは、トレースを有効にするために必要があります。

```ManagedCPlusPlus
#define WPP_CONTROL_GUIDS                                              \
    WPP_DEFINE_CONTROL_GUID(                                           \
        MyDriver1TraceGuid, (f0261b19,c295,4a92,aa8e,c6316c82cdf0),    \
                                                                       \
        WPP_DEFINE_BIT(MYDRIVER_ALL_INFO)                              \
        WPP_DEFINE_BIT(TRACE_DRIVER)                                   \
        WPP_DEFINE_BIT(TRACE_DEVICE)                                   \
        WPP_DEFINE_BIT(TRACE_QUEUE)                                    \
        )                             

#define WPP_FLAG_LEVEL_LOGGER(flag, level)                             \
    WPP_LEVEL_LOGGER(flag)

#define WPP_FLAG_LEVEL_ENABLED(flag, level)                            \
    (WPP_LEVEL_ENABLED(flag) &&                                        \
     WPP_CONTROL(WPP_BIT_ ## flag).Level >= level)

#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)
```

フォワード Internal.h で [次へ] 行は、コールバックのキュー オブジェクトのクライアント ドライバー実装クラスを宣言します。 テンプレートによって生成された他のプロジェクト ファイルも含まれています。 このトピックの後半では、実装とプロジェクトのヘッダー ファイルがについて説明します。

```ManagedCPlusPlus
// Forward definition of queue.

typedef class CMyIoQueue *PCMyIoQueue;

// Include the type specific headers.

#include "Driver.h"
#include "Device.h"
#include "IoQueue.h"
```

クライアント ドライバーをインストールした後、Windows は、クライアント ドライバーとは、ホスト プロセスのインスタンスのフレームワークを読み込みます。 ここでは、フレームワークは、読み込みをクライアント ドライバーを初期化します。 フレームワークは、これらのタスクを実行します。

1.  作成、*ドライバー オブジェクト*framework を表すには、クライアント ドライバー。
2.  要求、 [IDriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff554885)クラス ファクトリからインターフェイス ポインター。
3.  作成、*デバイス オブジェクト*framework。
4.  PnP マネージャーは、デバイスを起動した後、デバイス オブジェクトを初期化します。

ドライバーは、読み込みと初期化が、いくつかのイベントが発生して、フレームワークにより、それらを処理に参加するクライアント ドライバー。 クライアント ドライバーの側では、ドライバーは、これらのタスクを実行します。

1.  実装し、エクスポート、 [ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760)クライアント ドライバーのモジュールから関数のフレームワークは、ドライバーへの参照を取得できます。
2.  実装するコールバック クラスを提供します、 [IDriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff554885)インターフェイス。
3.  実装するコールバック クラスを提供します**IPnpCallbackXxx**インターフェイス。
4.  デバイス オブジェクトへの参照を取得し、クライアント ドライバーの要件に従って構成します。

## <a name="driver-callback-source-code"></a>ドライバーのコールバックのソース コード


フレームワークを作成、*ドライバー オブジェクト*、Windows によって読み込まれるクライアント ドライバーのインスタンスを表します。 クライアント ドライバーでは、少なくとも 1 つのドライバー コールバック フレームワーク、ドライバーに登録を提供します。

ドライバーのコールバックの完全なソース コードは、Driver.h と Driver.c です。

クライアント ドライバーが実装するドライバー コールバック クラスを定義する必要があります[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)と[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)インターフェイス。 ヘッダー ファイル、Driver.h、という CMyDriver、ドライバーのコールバックを定義するクラスを宣言します。

```ManagedCPlusPlus
EXTERN_C const CLSID CLSID_Driver;

class CMyDriver :
    public CComObjectRootEx<CComMultiThreadModel>,
    public CComCoClass<CMyDriver, &CLSID_Driver>,
    public IDriverEntry
{
public:

    CMyDriver()
    {
    }

    DECLARE_NO_REGISTRY()

    DECLARE_NOT_AGGREGATABLE(CMyDriver)

    BEGIN_COM_MAP(CMyDriver)
        COM_INTERFACE_ENTRY(IDriverEntry)
    END_COM_MAP()

public:

    // IDriverEntry methods

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnInitialize(
        __in IWDFDriver *FxWdfDriver
        )
    {
        UNREFERENCED_PARAMETER(FxWdfDriver);
        return S_OK;
    }

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnDeviceAdd(
        __in IWDFDriver *FxWdfDriver,
        __in IWDFDeviceInitialize *FxDeviceInit
        );

    virtual
    VOID
    STDMETHODCALLTYPE
    OnDeinitialize(
        __in IWDFDriver *FxWdfDriver
        )
    {
        UNREFERENCED_PARAMETER(FxWdfDriver);
        return;
    }

};

OBJECT_ENTRY_AUTO(CLSID_Driver, CMyDriver)
```

ドライバーのコールバックはつまり、実装する必要があります、COM クラスである必要があります[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)と関連するメソッド。 テンプレート コードで ATL クラス CComObjectRootEx と CComCoClass を含む、 **IUnknown**メソッド。

Windows は、ホスト プロセスをインスタンス化した後、フレームワークには、ドライバー オブジェクトが作成されます。 フレームワークが、ドライバー コールバック クラスの呼び出しのドライバーの実装のインスタンスを作成するためには、 [ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760) (で説明した、[ドライバー エントリのソース コード](#driver-entry-source-code)セクション) と、クライアント ドライバーの入手[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)インターフェイス ポインター。 その呼び出しは、フレームワーク ドライバー オブジェクトをドライバーのコールバック オブジェクトを登録します。 登録が成功は、フレームワークは、特定のドライバー固有のイベントが発生したときにクライアント ドライバーの実装を呼び出します。 フレームワークを呼び出す最初のメソッドは、 [ **IDriverEntry::OnInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff554885_oninitialize)メソッド。 クライアント ドライバーの実装で**IDriverEntry::OnInitialize**、クライアント ドライバーがドライバーのグローバル リソースを割り当てることができます。 これらのリソースを解放する必要があります[ **IDriverEntry::OnDeinitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff554885_ondeinitialize)クライアント ドライバーをアンロードする準備中である直前に、フレームワークによって呼び出されます。 テンプレート コードの最小限の実装を提供する、 **OnInitialize**と**OnDeinitialize**メソッド。

最も重要なメソッド[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)は[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554885_ondeviceadd)します。 ドライバーのフレームワークでは、(次のセクションで説明) framework デバイス オブジェクトを作成する前に呼び出す**IDriverEntry::OnDeviceAdd**実装します。 メソッドを呼び出すと、フレームワークに渡します、 [ **IWDFDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff558893)ドライバー オブジェクトへのポインターと[ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)ポインター。 クライアント ドライバーを呼び出すことができます**IWDFDeviceInitialize**メソッドを特定の構成オプションを指定します。

通常、クライアント ドライバーはで、次のタスクを実行します。 その[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)実装。

-   デバイス オブジェクトを作成するための構成情報を指定します。
-   ドライバーのデバイス コールバック クラスをインスタンス化します。
-   Framework デバイス オブジェクトを作成し、デバイス、そのコールバック オブジェクトをフレームワークに登録します。
-   フレームワークのデバイス オブジェクトを初期化します。
-   デバイスのインターフェイス、クライアント ドライバーの GUID を登録します。

テンプレート コードで**IDriverEntry::OnDeviceAdd**静的メソッドを呼び出す、CMyDevice::CreateInstanceAndInitialize、デバイス コールバック クラスで定義されています。 静的メソッドでは、まず、クライアント ドライバーのデバイス コールバック クラスをインスタンス化され、フレームワークのデバイス オブジェクトが作成されます。 デバイスのコールバック クラスには、上記のリストに記載されている残りのタスクを実行する構成をという名前のパブリック メソッドも定義します。 デバイスのコールバック クラスの実装は、次のセクションで説明します。
次のコード例は、 [ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)テンプレート コードで実装します。

```ManagedCPlusPlus
HRESULT
CMyDriver::OnDeviceAdd(
    __in IWDFDriver *FxWdfDriver,
    __in IWDFDeviceInitialize *FxDeviceInit
    )
{
    HRESULT hr = S_OK;
    CMyDevice *device = NULL;

    hr = CMyDevice::CreateInstanceAndInitialize(FxWdfDriver,
                                                FxDeviceInit,
                                                &device);

    if (SUCCEEDED(hr))
    {
        hr = device->Configure();
    }

    return hr;
}
```

次のコード例では、Device.h でデバイス クラスの宣言を示します。

```ManagedCPlusPlus
class CMyDevice :
    public CComObjectRootEx<CComMultiThreadModel>,
    public IPnpCallbackHardware
{

public:

    DECLARE_NOT_AGGREGATABLE(CMyDevice)

    BEGIN_COM_MAP(CMyDevice)
        COM_INTERFACE_ENTRY(IPnpCallbackHardware)
    END_COM_MAP()

    CMyDevice() :
        m_FxDevice(NULL),
        m_IoQueue(NULL),
        m_FxUsbDevice(NULL)
    {
    }

    ~CMyDevice()
    {
    }

private:

    IWDFDevice *            m_FxDevice;

    CMyIoQueue *            m_IoQueue;

    IWDFUsbTargetDevice *   m_FxUsbDevice;

private:

    HRESULT
    Initialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit
        );

public:

    static
    HRESULT
    CreateInstanceAndInitialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit,
        __out CMyDevice **Device
        );

    HRESULT
    Configure(
        VOID
        );
public:

    // IPnpCallbackHardware methods

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnPrepareHardware(
            __in IWDFDevice *FxDevice
            );

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnReleaseHardware(
        __in IWDFDevice *FxDevice
        );

};
```

## <a name="device-callback-source-code"></a>デバイスのコールバックのソース コード


*Framework デバイス オブジェクト*クライアント ドライバーのデバイス スタックに読み込まれるデバイス オブジェクトを表す framework クラスのインスタンスです。 デバイス オブジェクトの機能については、次を参照してください。[デバイス ノードとデバイス スタック](https://msdn.microsoft.com/library/windows/hardware/hh406296)します。

デバイス オブジェクトの完全なソース コードは Device.h と Device.c にあります。

Framework デバイス クラスの実装、 [ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)インターフェイス。 クライアント ドライバーがドライバーの実装でそのクラスのインスタンスを作成する責任を負います[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554896)します。 クライアント ドライバーを取得しますが、オブジェクトの作成後、 **IWDFDevice**デバイス オブジェクトの操作を管理するには、そのインターフェイスの新しいオブジェクトと呼び出しメソッドへのポインター。

**IDriverEntry::OnDeviceAdd 実装**

クライアント ドライバーを実行するタスクの説明について簡単に、前のセクションで[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554896)します。 これらのタスクの詳細を次に示します。 クライアント ドライバー:

-   デバイス オブジェクトを作成するための構成情報を指定します。

    フレームワークのクライアント ドライバーの実装を呼び出して、 [ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)フレームワークは、メソッドに渡します、 [ **IWDFDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff556965)ポインター。 クライアント ドライバーでは、このポインターを使用して、デバイス オブジェクトを作成するための構成情報を指定します。 たとえば、クライアント ドライバーでは、クライアント ドライバーが、フィルターまたは関数のドライバーがかどうかを指定します。 フィルター ドライバーとしてクライアント ドライバーを識別するために呼び出す[ **IWDFDeviceInitialize::SetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff556965_setfilter)します。 その場合は、フレームワークはフィルター デバイス オブジェクト (FiDO); を作成します。それ以外の場合、関数のデバイス オブジェクト (FDO) が作成されます。 設定できるもう 1 つのオプションは、呼び出すことによって同期モードを[ **IWDFDeviceInitialize::SetLockingConstraint**](https://msdn.microsoft.com/library/windows/hardware/ff556965_setlockingconstraint)します。

-   呼び出し、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)メソッドを渡すことによって、 [ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)インターフェイス ポインター、 [ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)デバイス コールバック オブジェクト、およびポインターのポインターの参照[ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)変数。

    場合、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)呼び出しが成功するとします。

    -   フレームワークは、デバイス オブジェクトを作成します。
    -   フレームワークは、フレームワークをデバイス コールバックを登録します。

        デバイス コールバックを組み合わせる framework デバイス オブジェクトを使用すると後、は、PnP 状態などの特定のイベントを処理フレームワークと、クライアント ドライバーと、電源状態の変更。 たとえば、PnP のマネージャーは、デバイスを起動するときに、フレームワークに通知されます。 フレームワークが呼び出され、デバイス コールバックの[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)実装します。 すべてのクライアント ドライバーでは、少なくとも 1 つのデバイスのコールバック オブジェクトを登録する必要があります。

    -   クライアント ドライバーは、デバイスの新しいオブジェクトのアドレスを受け取る、 [ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)変数。 フレームワークのデバイス オブジェクトへのポインターを受け取ると、クライアント ドライバーは、I/O のフローのキューの設定や、デバイス インターフェイスの GUID を登録するなどの初期化タスクを開始できます。

-   呼び出し[ **IWDFDevice::CreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550965)デバイス インターフェイス、クライアント ドライバーの GUID を登録します。 アプリケーションは、GUID を使用して、クライアント ドライバーに要求を送信できます。 GUID 定数は、Internal.h で宣言されます。
-   デバイスからの I/O の転送キューを初期化します。

テンプレート コードでは、初期化、構成情報を指定し、デバイス オブジェクトを作成するヘルパー メソッドを定義します。

次のコード例では、初期化の実装を示します。

```ManagedCPlusPlus
HRESULT
CMyDevice::Initialize(
    __in IWDFDriver           * FxDriver,
    __in IWDFDeviceInitialize * FxDeviceInit
    )
{
    IWDFDevice *fxDevice = NULL;
    HRESULT hr = S_OK;
    IUnknown *unknown = NULL;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    FxDeviceInit->SetLockingConstraint(None);

    FxDeviceInit->SetPowerPolicyOwnership(TRUE);

    hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to get IUnknown %!hresult!",
                    hr);
        goto Exit;
    }

    hr = FxDriver->CreateDevice(FxDeviceInit, unknown, &fxDevice);
    DriverSafeRelease(unknown);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create a framework device %!hresult!",
                    hr);
        goto Exit;
    }

     m_FxDevice = fxDevice;

     DriverSafeRelease(fxDevice);

Exit:

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return hr;
}
```

前のコード例では、クライアント ドライバーは、デバイス オブジェクトを作成し、そのデバイス コールバックを登録します。 デバイス オブジェクトを作成する前に、ドライバーはメソッドを呼び出すことによって、構成の基本設定を指定します、 [ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)インターフェイス ポインター。 その以前のクライアント ドライバーの呼び出しで、フレームワークによって渡された同じポインターは[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)メソッド。

クライアント ドライバーでは、デバイス オブジェクトの電源ポリシー所有者になるを指定します。 電源ポリシー所有者は、クライアント ドライバーはシステムの電源状態が変更されたときに、デバイスが入力する適切な電源状態を判断します。 電源の状態遷移を実行するには、デバイスに関連する要求を送信するため、ドライバーもします。 既定ではない、電源ポリシー所有者に UMDF ベースのクライアント ドライバーです。フレームワークは、すべての電源の状態遷移を処理します。 フレームワークでは、デバイスを自動的に送信されます**D3** 、システムがスリープ状態とは逆に、デバイスに**D0** 、システムの稼働状態に入ったとき**S0**. 詳細については、次を参照してください。 [UMDF で電源ポリシー所有権](https://msdn.microsoft.com/library/windows/hardware/ff560462)します。

別の構成オプションでは、クライアント ドライバーが、フィルター ドライバーまたはデバイスの機能のドライバーがかどうかを指定します。 コード例では、クライアント ドライバーに明示的に指定していないことの優先順位に注意してください。 つまり、クライアント ドライバーは、関数ドライバー、フレームワークは、デバイス スタックで FDO を作成する必要があります。 かどうかには、クライアント ドライバーは、フィルター ドライバーを希望していますし、ドライバーを呼び出す必要があります、 [ **IWDFDeviceInitialize::SetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff556985)メソッド。 その場合は、フレームワークは、デバイス スタックで、FiDO を作成します。

クライアント ドライバーでは、クライアント ドライバーのコールバックにフレームワークのいずれもが同期されるも指定します。 クライアント ドライバーでは、すべての同期タスクを処理します。 クライアント ドライバーの呼び出し、その設定を指定する、 [ **IWDFDeviceInitialize::SetLockingConstraint** ](https://msdn.microsoft.com/library/windows/hardware/ff556991)メソッド。

次に、クライアント ドライバーを取得、 [ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)呼び出すことによって、デバイス コールバック クラスへのポインター [ **iunknown::queryinterface**](https://msdn.microsoft.com/library/windows/desktop/ms682521)します。 クライアント ドライバーの呼び出し、その後、 [ **IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)、framework デバイス オブジェクトを作成しを使用して、クライアント ドライバーのデバイスのコールバックを登録する**IUnknown**ポインター。

クライアント ドライバーがデバイス オブジェクトのアドレスを格納することに注意してください (経由で受信した、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)呼び出し)、デバイス コールバック クラスのプライベート データ メンバーにし、解放します。DriverSafeRelease (Internal.h で定義されたインライン関数) を呼び出すことによって参照されます。 デバイス オブジェクトの有効期間が、framework によって追跡されるためです。 そのため、クライアント ドライバーでは、デバイス オブジェクトの追加の参照カウントを保持する必要はありません。

テンプレート コードでは、パブリック メソッドの構成では、デバイス インターフェイスの GUID を登録し、キューの設定を定義します。 次のコード例では、デバイス コールバック クラス CMyDevice で、Configure メソッドの定義を示します。 構成によって呼び出される[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896) framework デバイス オブジェクトを作成した後。

```ManagedCPlusPlus
CMyDevice::Configure(
    VOID
    )
{

    HRESULT hr = S_OK;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

     hr = CMyIoQueue::CreateInstanceAndInitialize(m_FxDevice, this, &m_IoQueue);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create and initialize queue %!hresult!",
                    hr);
        goto Exit;
    }

    hr = m_IoQueue->Configure();
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to configure queue %!hresult!",
                    hr);
        goto Exit;
    } 

    hr = m_FxDevice->CreateDeviceInterface(&GUID_DEVINTERFACE_MyUSBDriver_UMDF_,NULL);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create device interface %!hresult!",
                    hr);
        goto Exit;
    }

Exit:

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return hr;
}
```

クライアント ドライバーを前のコード例には、2 つの主要なタスクを実行します。 I/O フローのキューを初期化し、デバイスを登録するインターフェイスの GUID。

キューが作成され、CMyIoQueue クラスで構成されています。 最初のタスクでは、CreateInstanceAndInitialize をという名前の静的メソッドを呼び出すことによってそのクラスのインスタンスを作成します。 クライアント ドライバーでは、キューを初期化するために構成を呼び出します。 CreateInstanceAndInitialize と構成は、CMyIoQueue、これについては、このトピックの説明で宣言されます。

クライアント ドライバーの呼び出しも[ **IWDFDevice::CreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550965)デバイス インターフェイス、クライアント ドライバーの GUID を登録します。 アプリケーションは、GUID を使用して、クライアント ドライバーに要求を送信できます。 GUID 定数は、Internal.h で宣言されます。

**IPnpCallbackHardware 実装と USB の特定のタスク**

次の実装を見て、 [ **IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764) Device.cpp のインターフェイス。

すべてのデバイス コールバック クラスを実装する必要があります、 [ **IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)インターフェイス。 このインターフェイスでは、2 つの方法があります。[**IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764_onpreparehardware)と[ **IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556764_onreleasehardware)します。 フレームワークでは、これらのメソッドを呼び出す 2 つのイベントに応答: PnP マネージャーでのデバイスとデバイスを削除するときの開始時です。 場合は、デバイスが起動して、ハードウェアへの通信が確立されているが、デバイスは稼働状態に入っていません (**D0**)。 したがって、 **IPnpCallbackHardware::OnPrepareHardware**クライアント ドライバーは、ハードウェアからデバイス情報を取得、リソースの割り当て、およびドライバーの有効期間中に必要なフレームワーク オブジェクトを初期化します。 PnP マネージャーでは、デバイスを削除するときに、ドライバーは、システムからアンロードされます。 フレームワークは、クライアント ドライバーの**IPnpCallbackHardware::OnReleaseHardware**それらのリソースおよび framework オブジェクトのドライバーはリリースの実装。

PnP マネージャーでは、その他の種類の PnP 状態の変更に起因するイベントを生成できます。 フレームワークは、既定のこれらのイベントの処理を提供します。 クライアント ドライバーは、これらのイベントの処理に参加を選択できます。 USB デバイスが、ホストから切り離されたシナリオを検討してください。 PnP マネージャーでは、そのイベントを認識し、フレームワークに通知します。 クライアント ドライバーは、イベントへの応答に追加のタスクを実行する必要がある場合、ドライバーを実装する必要があります、 [ **IPnpCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff556762)インターフェイスと、関連[ **IPnpCallback: OnSurpriseRemoval** ](https://msdn.microsoft.com/library/windows/hardware/ff556762_onsurpriseremoval)デバイス コールバック クラスのメソッド。 それ以外の場合、フレームワークは、そのイベントの既定の処理を続行します。

USB クライアント ドライバーは、サポートされているインターフェイス、代替の設定とエンドポイントに関する情報を取得し、データ転送のすべての I/O 要求を送信する前にようを構成する必要があります。 UMDF は、さまざまなクライアント ドライバーの構成タスクを簡略化する専用の I/O ターゲット オブジェクトを提供します。 USB デバイスを構成するには、クライアント ドライバーには、PnP マネージャーは、デバイスを起動した後にのみ利用可能なデバイス情報が必要です。

このテンプレート コードでこれらのオブジェクトを作成し、 [ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)メソッド。

通常、クライアント ドライバー (デバイスの設計) に応じてこれらの構成タスクの 1 つ以上を実行します。

1.  インターフェイスの数など、現在の構成に関する情報を取得します。 フレームワークは、USB デバイスで最初の構成を選択します。 クライアント ドライバーでは、複数の構成のデバイスの場合、別の構成を選択できません。
2.  エンドポイントの数などのインターフェイスに関する情報を取得します。
3.  インターフェイスは、1 つ以上の設定をサポートしている場合は、各インターフェイスの代替設定を変更します。 既定では、フレームワークは、USB デバイスで最初の構成の各インターフェイスの最初の代替設定を選択します。 クライアント ドライバーは、代替の設定を選択できます。
4.  各インターフェイス内のエンドポイントに関する情報を取得します。

これらのタスクを実行するには、クライアント ドライバーは、WDF によって提供される専用の USB I/O ターゲット オブジェクトのこれらの型を使用できます。

| USB I/O ターゲット オブジェクト     | 説明                                                                                                                                                                                                                                                                                                                               | UMDF インターフェイス                                  |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| *ターゲット デバイス オブジェクト*    | USB デバイスを表し、デバイス記述子を取得し、デバイスに対する制御要求を送信するためのメソッドを提供します。                                                                                                                                                                                                             | [IWDFUsbTargetDevice](https://msdn.microsoft.com/library/windows/hardware/ff560362) |
| *ターゲット インターフェイス オブジェクト* | 個別のインターフェイスを表し、代替の設定を選択し、設定に関する情報を取得するクライアント ドライバーを呼び出すことができるメソッドを提供します。                                                                                                                                                                          | [IWDFUsbInterface](https://msdn.microsoft.com/library/windows/hardware/ff560312)       |
| *パイプ オブジェクトのターゲット*      | インターフェイスの現在の代替設定で構成されているエンドポイントの個別のパイプを表します。 USB バス ドライバーでは、選択した構成の各インターフェイスを選択し、インターフェイス内で各エンドポイントへの通信チャネルを設定します。 USB 用語では、その通信チャネルと呼ばれる、*パイプ*します。 | [IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)     |



次のコード例の実装を示しています。 [ **IPnpCallbackHardware::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556766)します。

```ManagedCPlusPlus
HRESULT
CMyDevice::OnPrepareHardware(
    __in IWDFDevice * /* FxDevice */
    )
{
    HRESULT hr;
    IWDFUsbTargetFactory *usbFactory = NULL;
    IWDFUsbTargetDevice *usbDevice = NULL;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    hr = m_FxDevice->QueryInterface(IID_PPV_ARGS(&usbFactory));

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to get USB target factory %!hresult!",
                    hr);
        goto Exit;
    }

    hr = usbFactory->CreateUsbTargetDevice(&usbDevice);

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create USB target device %!hresult!",
                    hr);

        goto Exit;
    }

     m_FxUsbDevice = usbDevice;

Exit:

    DriverSafeRelease(usbDevice);

    DriverSafeRelease(usbFactory);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return hr;
}
```

フレームワークの USB I/O ターゲット オブジェクトを使用するには、クライアント ドライバーはまず、USB ターゲット デバイス オブジェクトを作成する必要があります。 Framework のオブジェクト モデルでは、USB ターゲットのデバイス オブジェクトは、USB デバイスを表すデバイス オブジェクトの子です。 USB ターゲットのデバイス オブジェクトは、framework によって実装され、構成の選択などの USB デバイスのすべてのデバイス レベルのタスクを実行します。

前のコード例でクライアント ドライバー フレームワークのデバイス オブジェクトに照会し、取得、 [ **IWDFUsbTargetFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff560387) USB ターゲットのデバイス オブジェクトを作成するクラス ファクトリへのポインター。 クライアント ドライバーを呼び出してそのポインターを使用して、 [ **IWDFUsbTargetDevice::CreateUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560387_createusbtargetdevice)メソッド。 メソッドは、USB ターゲットのデバイス オブジェクトを作成しへのポインターを返します、 [ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)インターフェイス。 メソッドは、既定値 (最初) の構成とその構成で各インターフェイスの場合は 0 を設定する代替も選択します。

テンプレート コードが、USB ターゲット デバイス オブジェクトのアドレスを格納 (経由で受信した、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)呼び出し)、デバイス コールバック クラスのプライベート データ メンバーにし、解放します。DriverSafeRelease を呼び出すことによって参照されます。 USB のターゲット デバイス オブジェクトの参照カウントは、フレームワークによって保持されます。 オブジェクトが、デバイス オブジェクトが生きている限り有効です。 クライアント ドライバーは、への参照を解放する必要があります[ **IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556768)します。

ドライバーを呼び出すクライアント ドライバーでは、USB ターゲットのデバイス オブジェクトが作成されたら、 [ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)これらのタスクを実行するメソッド。

-   デバイス、構成、インターフェイスの記述子、およびデバイスの速度などの他の情報を取得します。
-   書式を設定し、コントロールの I/O 要求を既定のエンドポイントに送信します。
-   全体の USB デバイスの電源ポリシーを設定します。

詳細については、次を参照してください。 [UMDF で USB デバイスを使用して](https://msdn.microsoft.com/library/windows/hardware/ff561472)します。
次のコード例の実装を示しています。 [ **IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556768)します。

```ManagedCPlusPlus
HRESULT
CMyDevice::OnReleaseHardware(
    __in IWDFDevice * /* FxDevice */
    )
{
    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    if (m_FxUsbDevice != NULL) {

        m_FxUsbDevice->DeleteWdfObject();
        m_FxUsbDevice = NULL;
    }

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return S_OK;
}
```

## <a name="queue-source-code"></a>キュー ソース コード


*Framework キュー オブジェクト*特定のフレームワークのデバイス オブジェクトの I/O キューを表します。 キュー オブジェクトの完全なソース コードは、IoQueue.h と IoQueue.c です。

**IoQueue.h**

IoQueue.h ヘッダー ファイルは、キューのコールバック クラスを宣言します。

```ManagedCPlusPlus
class CMyIoQueue :
    public CComObjectRootEx<CComMultiThreadModel>,
    public IQueueCallbackDeviceIoControl
{

public:

    DECLARE_NOT_AGGREGATABLE(CMyIoQueue)

    BEGIN_COM_MAP(CMyIoQueue)
        COM_INTERFACE_ENTRY(IQueueCallbackDeviceIoControl)
    END_COM_MAP()

    CMyIoQueue() : 
        m_FxQueue(NULL),
        m_Device(NULL)
    {
    }

    ~CMyIoQueue()
    {
        // empty
    }

    HRESULT
    Initialize(
        __in IWDFDevice *FxDevice,
        __in CMyDevice *MyDevice
        );

    static 
    HRESULT 
    CreateInstanceAndInitialize( 
        __in IWDFDevice *FxDevice,
        __in CMyDevice *MyDevice,
        __out CMyIoQueue**    Queue
        );

    HRESULT
    Configure(
        VOID
        )
    {
        return S_OK;
    }


    // IQueueCallbackDeviceIoControl

    virtual
    VOID
    STDMETHODCALLTYPE
    OnDeviceIoControl( 
        __in IWDFIoQueue *pWdfQueue,
        __in IWDFIoRequest *pWdfRequest,
        __in ULONG ControlCode,
        __in SIZE_T InputBufferSizeInBytes,
        __in SIZE_T OutputBufferSizeInBytes
        );

private:

    IWDFIoQueue *               m_FxQueue;

    CMyDevice *                 m_Device;

};
```

上記のコード例では、クライアント ドライバーは、キューのコールバック クラスを宣言します。 インスタンス化する場合は、クライアント ドライバーにディスパッチ要求が処理するフレームワークのキュー オブジェクトとオブジェクトが働いてきました。 クラスは、作成し、フレームワークのキュー オブジェクトを初期化する 2 つのメソッドを定義します。 CreateInstanceAndInitialize 静的メソッドでは、キューのコールバック クラスをインスタンス化を作成し、フレームワークのキュー オブジェクトを初期化する Initialize メソッドを呼び出します。 また、キュー オブジェクトのディスパッチ オプションも指定します。

```ManagedCPlusPlus
HRESULT 
CMyIoQueue::CreateInstanceAndInitialize(
    __in IWDFDevice *FxDevice,
    __in CMyDevice *MyDevice,
    __out CMyIoQueue** Queue
    )
{

    CComObject<CMyIoQueue> *pMyQueue = NULL;
    HRESULT hr = S_OK;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Entry");

    hr = CComObject<CMyIoQueue>::CreateInstance( &pMyQueue );
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_QUEUE,
                    "%!FUNC! Failed to create instance %!hresult!",
                    hr);
        goto Exit;
    }

    hr = pMyQueue->Initialize(FxDevice, MyDevice);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_QUEUE,
                    "%!FUNC! Failed to initialize %!hresult!",
                    hr);
        goto Exit;
    }

    *Queue = pMyQueue;

Exit:

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Exit");

    return hr;
}
```

次のコード例では、Initialize メソッドの実装を示します。

```ManagedCPlusPlus
HRESULT
CMyIoQueue::Initialize(
    __in IWDFDevice *FxDevice,
    __in CMyDevice *MyDevice
    )
{
    IWDFIoQueue *fxQueue = NULL;
    HRESULT hr = S_OK;
    IUnknown *unknown = NULL;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Entry");

    assert(FxDevice != NULL);
    assert(MyDevice != NULL);

    hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_QUEUE,
                    "%!FUNC! Failed to query IUnknown interface %!hresult!",
                    hr);
        goto Exit;
    }

    hr = FxDevice->CreateIoQueue(unknown,
                                 FALSE,     // Default Queue?
                                 WdfIoQueueDispatchParallel,  // Dispatch type
                                 TRUE,     // Power managed?
                                 FALSE,     // Allow zero-length requests?
                                 &fxQueue); // I/O queue
    DriverSafeRelease(unknown);

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR, 
                   TRACE_QUEUE, 
                   "%!FUNC! Failed to create framework queue.");
        goto Exit;
    }

    hr = FxDevice->ConfigureRequestDispatching(fxQueue,
                                               WdfRequestDeviceIoControl,
                                               TRUE);

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR, 
                   TRACE_QUEUE, 
                   "%!FUNC! Failed to configure request dispatching %!hresult!.",
                   hr);
        goto Exit;
    }

    m_FxQueue = fxQueue;
    m_Device= MyDevice;

Exit:

    DriverSafeRelease(fxQueue);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Exit");

    return hr;
}
```

上記のコード例では、クライアント ドライバーは、フレームワークのキュー オブジェクトを作成します。 フレームワークは、クライアント ドライバーに要求のフローを処理するために、キュー オブジェクトを提供します。

ドライバーの呼び出し、オブジェクトは、クライアントを作成する[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)上、 [ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)で取得した参照、以前の呼び出し[ **IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)します。

[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)呼び出し、クライアント ドライバー特定の構成オプションを指定します、フレームワークは、キューを作成する前にします。 これらのオプションは、キューに電源管理は、し、長さ 0 の要求を許可し、ドライバーの既定のキューとして機能するかどうかを決定します。 クライアント ドライバーは、この一連の情報を提供します。

-   そのキュー コールバック クラスへの参照

    指定します、 [ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)そのキュー コールバック クラスへのポインター。 これは、フレームワークのキュー オブジェクトと、クライアント ドライバーのキューのコールバック オブジェクトの間のパートナーシップを作成します。 I/O マネージャーは、アプリケーションから新しい要求を受信したときに、フレームワークに通知します。 フレームワークを使用して、 **IUnknown**キューのコールバック オブジェクトによって公開されるパブリック メソッドの呼び出しへのポインター。

-   既定のインスタンスまたはセカンダリ キュー

    キューは、既定のキューまたはセカンダリ キューのいずれかである必要があります。 フレームワークのキュー オブジェクトは、既定のキューとして動作している場合、すべての要求はキューに追加されます。 セカンダリ キューには、特定の種類の要求は専用です。 クライアント ドライバーは、セカンダリ キューを要求する場合、ドライバーは呼び出す必要がありますも、 [ **IWDFDevice::ConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff557014)メソッドでフレームワークを配置する必要がありますの要求の種類を示すために、指定されたキューです。 テンプレートのコードでは、クライアント ドライバーに FALSE を渡します。、 *bDefaultQueue*パラメーター。 セカンダリ キューと既定のキューを作成する方法を指示するとします。 後で呼び出す**IWDFDevice::ConfigureRequestDispatching**をキューにデバイス I/O 制御のみを持つ必要があるかを示す要求 (このセクションのコード例を参照してください)。

-   ディスパッチの種類

    キュー オブジェクトのディスパッチの型は、クライアント ドライバーに、フレームワークが要求を配信する方法を決定します。 並列、またはクライアント ドライバーで定義されたカスタムのメカニズムによって、順次配信メカニズムは使用できます。 シーケンシャルなキューの場合、クライアント ドライバーが、前回の要求を完了するまで、要求は配信されません。 ディスパッチを並列モードでは、フレームワークは、I/O マネージャーから到着すると、すぐに、要求を転送します。 これは、クライアント ドライバーが別の処理中に要求を受信できることを意味します。 カスタムのメカニズムで、クライアントでは、ドライバーが処理する準備ができたとき、framework のキュー オブジェクトから、次の要求が手動で取得します。 テンプレート コードで並列ディスパッチ モードのクライアント ドライバーを要求します。

-   電源管理対象のキュー

    フレームワークのキュー オブジェクトは、デバイスの PnP と電源の状態と同期する必要があります。 作業状態のデバイスでない場合は、すべての要求のディスパッチ フレームワークのキュー オブジェクトが停止します。 動作状態では、ディスパッチ、キュー オブジェクトが再開します。 電源管理対象のキューでは、フレームワークにより、同期を実行します。それ以外の場合、クライアント ドライブは、そのタスクを処理する必要があります。 テンプレート コードでは、クライアントは、電源管理対象のキューを要求します。

-   許可される長さ 0 の要求

    クライアント ドライバーは、キューに配置するのではなくバッファーに長さ 0 の I/O 要求を完了するためにフレームワークに指示できます。 テンプレート コードでは、クライアントは、このような要求を完了するためにフレームワークを要求します。

1 つのフレームワークのキュー オブジェクトは、いくつかの種類の読み取り、書き込み、およびデバイスの I/O のコントロールなどの要求を処理しにできます。 テンプレート コードに基づくクライアント ドライバーでは、デバイス I/O 制御の要求のみを処理できます。 クライアント ドライバーのキューのコールバック クラスを実装、そのため、 [ **IQueueCallbackDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556852)インターフェイスとその[ **IQueueCallbackDeviceIoControl::OnDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556852_ondeviceiocontrol)メソッド。 これにより、クライアントを呼び出すために、フレームワークのドライバーの実装**IQueueCallbackDeviceIoControl::OnDeviceIoControl**フレームワークがデバイスの I/O 制御要求を処理する場合。

対応する他の種類の要求では、クライアント ドライバーを実装する必要があります**IQueueCallbackXxx**インターフェイス。 たとえば、クライアント ドライバーは、読み取り要求を処理する必要がある場合、キュー コールバック クラス、 [ **IQueueCallbackRead** ](https://msdn.microsoft.com/library/windows/hardware/ff556872)インターフェイスとその[ **IQueueCallbackRead::OnRead** ](https://msdn.microsoft.com/library/windows/hardware/ff556872_onread)メソッド。 要求とコールバック インターフェイスの種類については、次を参照してください。 [I/O キュー イベントのコールバック関数](https://msdn.microsoft.com/library/windows/hardware/ff560424)します。

次のコード例は、 [ **IQueueCallbackDeviceIoControl::OnDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556854)実装します。

```ManagedCPlusPlus
VOID
STDMETHODCALLTYPE
CMyIoQueue::OnDeviceIoControl(
    __in IWDFIoQueue *FxQueue,
    __in IWDFIoRequest *FxRequest,
    __in ULONG ControlCode,
    __in SIZE_T InputBufferSizeInBytes,
    __in SIZE_T OutputBufferSizeInBytes
    )
{
    UNREFERENCED_PARAMETER(FxQueue);
    UNREFERENCED_PARAMETER(ControlCode);
    UNREFERENCED_PARAMETER(InputBufferSizeInBytes);
    UNREFERENCED_PARAMETER(OutputBufferSizeInBytes);

    HRESULT hr = S_OK;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Entry");

    if (m_Device == NULL) {
        // We don't have pointer to device object
        TraceEvents(TRACE_LEVEL_ERROR, 
                   TRACE_QUEUE, 
                   "%!FUNC!NULL pointer to device object.");
        hr = E_POINTER;
        goto Exit;
    }

    //
    // Process the IOCTLs
    //

Exit:

    FxRequest->Complete(hr);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Exit");

    return;

}
```

キュー メカニズムのしくみを見てみましょう。 USB デバイスと通信して、アプリケーション最初にデバイスを識別するハンドルが開きを呼び出してデバイス I/O 制御要求を送信、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/hh404258)関数の特定のコントロールのコード。 、コントロールのコードの種類に応じて、アプリケーションは、その呼び出しの入力と出力バッファーを指定できます。 呼び出しは、I/O マネージャーによって、フレームワークに通知を最終的に受信されます。 フレームワークはフレームワーク要求オブジェクトを作成し、フレームワークのキュー オブジェクトに追加します。 テンプレート コードでは、キュー オブジェクトが作成された WdfIoQueueDispatchParallel フラグが、コールバックが呼び出される、要求がキューに追加されるとすぐにします。

要求 (およびその入力と出力のバッファー) を保持している framework 要求オブジェクトにハンドルを渡すために、フレームワークが、クライアント ドライバーのイベントのコールバックを呼び出すと、アプリケーションによって送信されます。 さらに、その要求を含むフレームワークのキュー オブジェクトへのハンドルを送信します。 イベントのコールバックでは、クライアント ドライバーが要求を処理に応じて。 テンプレート コードは、単に、要求を完了します。 クライアント ドライバーより複雑なタスクを実行できます。 たとえば、アプリケーションでは、特定のデバイス情報を要求している場合イベントのコールバック、クライアント ドライバーを USB 制御の要求を作成し、送信要求されたデバイス情報を取得する USB ドライバー スタックに。 USB 制御の要求は、後ほど[USB 制御転送](usb-control-transfer.md)します。

## <a name="driver-entry-source-code"></a>ドライバーのエントリのソース コード


テンプレート コードでは、driver エントリは、Dllsup.cpp に実装されます。

**Dllsup.cpp**

含めるセクションの後に、クライアント ドライバーの GUID 定数が宣言されています。 GUID は、ドライバーのインストール ファイル (INF) の GUID と一致する必要があります。

```ManagedCPlusPlus
const CLSID CLSID_Driver =
{0x079e211c,0x8a82,0x4c16,{0x96,0xe2,0x2d,0x28,0xcf,0x23,0xb7,0xff}};
```

次のコード ブロックは、クライアント ドライバーのクラス ファクトリを宣言します。

```ManagedCPlusPlus
class CMyDriverModule :
    public CAtlDllModuleT< CMyDriverModule >
{
};

CMyDriverModule _AtlModule;
```

テンプレート コードでは、ATL のサポートを使用して、複雑な COM コードをカプセル化します。 クラス ファクトリは、テンプレート クラスは、クライアント ドライバーを作成するために必要なすべてのコードを含む CAtlDllModuleT を継承します。

次のコード スニペットは、DllMain の実装を示しています。

```ManagedCPlusPlus
extern "C"
BOOL
WINAPI
DllMain(
    HINSTANCE hInstance,
    DWORD dwReason,
    LPVOID lpReserved
    )
{
    if (dwReason == DLL_PROCESS_ATTACH) {
        WPP_INIT_TRACING(MYDRIVER_TRACING_ID);

        g_hInstance = hInstance;
        DisableThreadLibraryCalls(hInstance);

    } else if (dwReason == DLL_PROCESS_DETACH) {
        WPP_CLEANUP();
    }

    return _AtlModule.DllMain(dwReason, lpReserved);
}
```

クライアント ドライバーが実装されている場合、 [ *DllMain* ](https://msdn.microsoft.com/library/windows/desktop/ms682583)関数は、Windows と見なします*DllMain*クライアント ドライバー モジュールのエントリ ポイントであります。 Windows の呼び出し*DllMain* WUDFHost.exe のクライアント ドライバーのモジュールを読み込んだ後。 Windows の呼び出し*DllMain* Windows は、メモリ内のクライアント ドライバーをアンロードする前にもう一度だけです。 *DllMain*を割り当て、ドライバー レベルでグローバル変数を解放できます。 テンプレート コードでは、クライアント ドライバーを初期化します、WPP トレースに必要なリソースを解放し、ATL クラスの DllMain の実装を呼び出します。

記述する方法については、 [ *DllMain*](https://msdn.microsoft.com/library/windows/desktop/ms682583)を参照してください[DllMain の実装](https://msdn.microsoft.com/library/aa370448)します。

次のコード スニペットでは、DllGetClassObject の実装を示します。

```ManagedCPlusPlus
STDAPI
DllGetClassObject(
    __in REFCLSID rclsid,
    __in REFIID riid,
    __deref_out LPVOID FAR* ppv
    )
{
    return _AtlModule.DllGetClassObject(rclsid, riid, ppv);
}
```

コード テンプレートでは、クラス ファクトリと[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760) ATL で実装されます 上記のコード スニペットは、ATL を呼び出すだけ**DllGetClassObject**実装します。 一般に、 **DllGetClassObject**次のタスクを実行する必要があります。

1.  フレームワークによって渡された CLSID が、クライアント ドライバーの GUID であることを確認します。 フレームワークは、ドライバーの INF ファイルからのクライアント ドライバーの CLSID を取得します。 検証するには、中に指定された GUID が、INF で指定したものと一致することを確認します。
2.  クライアント ドライバーによって実装される、クラス ファクトリをインスタンス化します。 テンプレート コードでこれは ATL クラスによってカプセル化します。
3.  ポインターを取得、 [ **IClassFactory** ](https://msdn.microsoft.com/library/windows/desktop/ms694364)クラス ファクトリと、フレームワークに戻る、取得したポインターのインターフェイス。

クライアント ドライバーのモジュールがメモリに読み込まれた後、フレームワーク ドライバーによって提供される[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760)関数。 フレームワークの呼び出しで**DllGetClassObject**、フレームワークは、CLSID をクライアント ドライバーを識別し、要求へのポインターに渡します、 [ **IClassFactory** ](https://msdn.microsoft.com/library/windows/desktop/ms694364)クラス ファクトリのインターフェイスです。 クライアント ドライバーをドライバー コールバックの作成を容易にするクラス ファクトリを実装します。 そのため、クライアント ドライバーでは、少なくとも 1 つのクラス ファクトリを含める必要があります。 フレームワーク[ **IClassFactory::CreateInstance** ](https://msdn.microsoft.com/library/windows/desktop/ms682215)を要求し、 [ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)ドライバー コールバックへのポインタークラス。

**Exports.def**

呼び出すために、フレームワークの順序で[ **DllGetClassObject**](https://msdn.microsoft.com/library/windows/desktop/ms680760)、クライアント ドライバーは、.def ファイルから関数をエクスポートする必要があります。 ファイルには既に Visual Studio プロジェクトが含まれます。

```ManagedCPlusPlus
; Exports.def : Declares the module parameters.

LIBRARY     "MyUSBDriver_UMDF_.DLL"

EXPORTS
        DllGetClassObject   PRIVATE
```

ドライバーのプロジェクトに含まれている Export.def から前のコード スニペットで、クライアントが、ライブラリとドライバーのモジュールの名前と[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760)エクスポート します。 詳細については、次を参照してください。 [DEF ファイルを使用する DLL からエクスポート](https://msdn.microsoft.com/library/d91k01sh(VS.80).aspx)します。








