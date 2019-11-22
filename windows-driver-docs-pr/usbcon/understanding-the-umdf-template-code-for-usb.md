---
Description: UMDF ベースの USB クライアントドライバーのソースコードについて説明します。
title: USB クライアントドライバーコードの構造 (UMDF)
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 48218236c5567ce49ec8cf747113e6c051cd3b35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844331"
---
# <a name="understanding-the-usb-client-driver-code-structure-umdf"></a>USB クライアントドライバーのコード構造 (UMDF) について


このトピックでは、UMDF ベースの USB クライアントドライバーのソースコードについて説明します。 このコード例は、Microsoft Visual Studio 2019 に含まれている**USB ユーザーモードドライバー**テンプレートによって生成されます。 このテンプレートコードは、Active Template Library (ATL) を使用して COM インフラストラクチャを生成します。 ATL とクライアントドライバーでの COM 実装の詳細については、ここでは説明しません。

UMDF テンプレートコードを生成する手順については、「[最初の USB クライアントドライバー (umdf) を作成する方法](implement-driver-entry-for-a-usb-driver--umdf-.md)」を参照してください。 テンプレートコードについては、次のセクションで説明します。

-   [ドライバーコールバックのソースコード](#driver-callback-source-code)
-   [デバイスコールバックのソースコード](#device-callback-source-code)
-   [キューのソースコード](#queue-source-code)
-   [ドライバーエントリのソースコード](#driver-entry-source-code)

テンプレートコードの詳細について説明する前に、UMDF ドライバー開発に関連するヘッダーファイル (内部 .h) のいくつかの宣言を見てみましょう。

内部 .h には、Windows Driver Kit (WDK) に含まれている次のファイルが含まれています。

```ManagedCPlusPlus
#include "atlbase.h"
#include "atlcom.h"

#include "wudfddi.h"
#include "wudfusb.h"
```

Atlbase .h および atlbase には、ATL サポートの宣言が含まれています。 クライアントドライバーによって実装される各クラスは、ATL クラスパブリック CComObjectRootEx を実装します。

Wudfddi. h は、常に UMDF ドライバー開発のために含まれています。 ヘッダーファイルには、UMDF ドライバーをコンパイルするために必要なメソッドと構造体のさまざまな宣言と定義が含まれています。

Wudfusb. h には、フレームワークによって提供される USB i/o ターゲットオブジェクトと通信するために必要な、UMDF 構造体およびメソッドの宣言と定義が含まれています。

内部 .h の次のブロックは、デバイスインターフェイスの GUID 定数を宣言します。 アプリケーションでは、この GUID を使用して、 **Setupdixxx** api を使用してデバイスへのハンドルを開くことができます。 GUID は、フレームワークがデバイスオブジェクトを作成した後に登録されます。

```ManagedCPlusPlus
// Device Interface GUID
// f74570e5-ed0c-4230-a7a5-a56264465548

DEFINE_GUID(GUID_DEVINTERFACE_MyUSBDriver_UMDF_,
    0xf74570e5,0xed0c,0x4230,0xa7,0xa5,0xa5,0x62,0x64,0x46,0x55,0x48);
```

次の部分では、トレースマクロとトレース GUID を宣言します。 トレース GUID をメモします。トレースを有効にするために必要になります。

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

内部 .h の次の行は、キューコールバックオブジェクトのクライアントドライバーで実装されたクラスを宣言します。 また、テンプレートによって生成されるその他のプロジェクトファイルも含まれます。 実装とプロジェクトのヘッダーファイルについては、このトピックで後ほど説明します。

```ManagedCPlusPlus
// Forward definition of queue.

typedef class CMyIoQueue *PCMyIoQueue;

// Include the type specific headers.

#include "Driver.h"
#include "Device.h"
#include "IoQueue.h"
```

クライアントドライバーをインストールすると、Windows によって、クライアントドライバーとフレームワークがホストプロセスのインスタンスに読み込まれます。 ここから、フレームワークによってクライアントドライバーが読み込まれ、初期化されます。 フレームワークは、次のタスクを実行します。

1.  クライアントドライバーを表す*ドライバーオブジェクト*をフレームワークに作成します。
2.  クラスファクトリから[Idriverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)インターフェイスポインターを要求します。
3.  フレームワークに*デバイスオブジェクト*を作成します。
4.  PnP マネージャーがデバイスを起動した後に、デバイスオブジェクトを初期化します。

ドライバーの読み込み中および初期化中に、いくつかのイベントが発生し、フレームワークによってクライアントドライバーが処理に参加できるようになります。 クライアントドライバー側では、ドライバーは次のタスクを実行します。

1.  フレームワークがドライバーへの参照を取得できるように、クライアントドライバーモジュールから[**DllGetClassObject**](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject)関数を実装してエクスポートします。
2.  [Idriverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)インターフェイスを実装するコールバッククラスを提供します。
3.  **IPnpCallbackXxx**インターフェイスを実装するコールバッククラスを提供します。
4.  デバイスオブジェクトへの参照を取得し、クライアントドライバーの要件に従って構成します。

## <a name="driver-callback-source-code"></a>ドライバーコールバックのソースコード


フレームワークは、Windows によって読み込まれるクライアントドライバーのインスタンスを表す*driver オブジェクト*を作成します。 クライアントドライバーは、ドライバーをフレームワークに登録する少なくとも1つのドライバーコールバックを提供します。

ドライバーコールバックの完全なソースコードは、Driver. .h と Driver. c にあります。

クライアントドライバーは、 [**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイスと[**Idriverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)インターフェイスを実装するドライバーコールバッククラスを定義する必要があります。 ヘッダーファイル Driver .h は、ドライバーコールバックを定義する CMyDriver というクラスを宣言します。

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

ドライバーコールバックは COM クラスである必要があります。これは、 [**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)と関連メソッドを実装する必要があることを意味します。 テンプレートコードでは、ATL クラス CComObjectRootEx と CComCoClass に**IUnknown**メソッドが含まれています。

Windows によってホストプロセスがインスタンス化されると、フレームワークによってドライバーオブジェクトが作成されます。 これを行うには、フレームワークによってドライバーコールバッククラスのインスタンスが作成され、 [**DllGetClassObject**](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) ([ドライバーエントリのソースコード](#driver-entry-source-code)セクションで説明) のドライバーの実装が呼び出され、クライアントドライバーの[**idriverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)が取得されます。インターフェイスポインター。 この呼び出しによって、ドライバーコールバックオブジェクトがフレームワークドライバーオブジェクトに登録されます。 正常に登録されると、特定のドライバー固有のイベントが発生したときに、フレームワークによってクライアントドライバーの実装が呼び出されます。 フレームワークが呼び出す最初のメソッドは、 [**Idriverentry:: OnInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff554885_oninitialize)メソッドです。 クライアントドライバーによる**Idriverentry:: OnInitialize**の実装では、クライアントドライバーがグローバルドライバーリソースを割り当てることができます。 これらのリソースは、クライアントドライバーのアンロードを準備する直前に、フレームワークによって呼び出される[**Idriverentry:: OnDeinitialize**](https://msdn.microsoft.com/library/windows/hardware/ff554885_ondeinitialize)でリリースされる必要があります。 このテンプレートコードは、 **oninitialize**メソッドと**ondeinitialize**メソッドに対して最小限の実装を提供します。

[**Idriverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)の最も重要な方法は、 [**Idriverentry:: ondeviceadd**](https://msdn.microsoft.com/library/windows/hardware/ff554885_ondeviceadd)です。 フレームワークは、フレームワークデバイスオブジェクト (次のセクションで説明します) を作成する前に、ドライバーの**Idriverentry:: OnDeviceAdd**実装を呼び出します。 メソッドを呼び出すと、フレームワークは[**Iwdfdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)ポインターを driver オブジェクトと[**Iwdfdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)ポインターに渡します。 クライアントドライバーは、 **Iwdfdeviceinitialize**メソッドを呼び出して、特定の構成オプションを指定できます。

通常、クライアントドライバーは、 [**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)実装で次のタスクを実行します。

-   作成するデバイスオブジェクトの構成情報を指定します。
-   ドライバーのデバイスコールバッククラスをインスタンス化します。
-   フレームワークデバイスオブジェクトを作成し、そのデバイスコールバックオブジェクトをフレームワークに登録します。
-   フレームワークデバイスオブジェクトを初期化します。
-   クライアントドライバーのデバイスインターフェイス GUID を登録します。

テンプレートコードでは、 **Idriverentry:: OnDeviceAdd**は、デバイスコールバッククラスで定義されている静的メソッド CMyDevice:: CreateInstanceAndInitialize を呼び出します。 静的メソッドは、まずクライアントドライバーのデバイスコールバッククラスをインスタンス化し、次にフレームワークデバイスオブジェクトを作成します。 デバイスコールバッククラスは、前の一覧で説明した残りのタスクを実行する Configure という名前のパブリックメソッドも定義します。 デバイスコールバッククラスの実装については、次のセクションで説明します。
次のコード例は、テンプレートコードでの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)実装を示しています。

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

次のコード例は、Device. h でのデバイスクラスの宣言を示しています。

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

## <a name="device-callback-source-code"></a>デバイスコールバックのソースコード


*Framework device オブジェクト*は、クライアントドライバーのデバイススタックに読み込まれるデバイスオブジェクトを表すフレームワーククラスのインスタンスです。 デバイスオブジェクトの機能の詳細については、「[デバイスノードとデバイススタック](https://docs.microsoft.com/windows-hardware/drivers/debugger/device-node-and-stack-debugger-commands)」を参照してください。

デバイスオブジェクトの完全なソースコードは、デバイス .h と Device .c にあります。

Framework device クラスは、 [**Iwdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスを実装します。 クライアントドライバーは、ドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)の実装で、そのクラスのインスタンスを作成します。 オブジェクトが作成されると、クライアントドライバーは、新しいオブジェクトへの**Iwdfdevice**ポインターを取得し、そのインターフェイスでメソッドを呼び出して、デバイスオブジェクトの操作を管理します。

**IDriverEntry:: OnDeviceAdd 実装**

前のセクションでは、クライアントドライバーが[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)で実行するタスクについて簡単に見てきました。 これらのタスクの詳細については、こちらを参照してください。 クライアントドライバー:

-   作成するデバイスオブジェクトの構成情報を指定します。

    フレームワークは、 [**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドのクライアントドライバーの実装に対する呼び出しで、 [**Iwdfdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)ポインターを渡します。 クライアントドライバーは、このポインターを使用して、作成するデバイスオブジェクトの構成情報を指定します。 たとえば、クライアントドライバーは、クライアントドライバーがフィルターと関数ドライバーのどちらであるかを指定します。 クライアントドライバーをフィルタードライバーとして識別するには、 [**Iwdfdeviceinitialize:: SetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff556965_setfilter)を呼び出します。 その場合は、フレームワークによってフィルターデバイスオブジェクト (FiDO) が作成されます。それ以外の場合は、関数デバイスオブジェクト (FDO) が作成されます。 もう1つの方法として、 [**Iwdfdeviceinitialize:: Setロック制約**](https://msdn.microsoft.com/library/windows/hardware/ff556965_setlockingconstraint)を呼び出して同期モードを設定することもできます。

-   [**Iwdfdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスポインター、デバイスコールバックオブジェクトの[**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)参照、およびポインターからポインターへの[**iwdfdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)変数を渡すことによって、 [**iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドを呼び出します。

    [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)の呼び出しが成功した場合は、次のようになります。

    -   フレームワークは、デバイスオブジェクトを作成します。
    -   フレームワークは、デバイスコールバックをフレームワークに登録します。

        デバイスのコールバックがフレームワークのデバイスオブジェクトとペアリングされると、フレームワークとクライアントドライバーが特定のイベント (PnP 状態や電源状態の変化など) を処理します。 たとえば、PnP マネージャーがデバイスを起動すると、フレームワークに通知されます。 次に、フレームワークは、デバイスコールバックの[**IPnpCallbackHardware:: On ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)の実装を呼び出します。 すべてのクライアントドライバーは、少なくとも1つのデバイスコールバックオブジェクトを登録する必要があります。

    -   クライアントドライバーは、 [**Iwdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)変数に新しいデバイスオブジェクトのアドレスを受け取ります。 フレームワークデバイスオブジェクトへのポインターを受け取ると、クライアントドライバーは初期化タスクを続行できます。たとえば、i/o フローのキューの設定や、デバイスインターフェイス GUID の登録などです。

-   [**Iwdfdevice:: CreateDeviceInterface**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea)を呼び出して、クライアントドライバーのデバイスインターフェイス GUID を登録します。 アプリケーションでは、GUID を使用してクライアントドライバーに要求を送信できます。 GUID 定数は内部 .h で宣言されています。
-   デバイスとの間で i/o 転送を行うキューを初期化します。

このテンプレートコードは、構成情報を指定し、デバイスオブジェクトを作成するヘルパーメソッド初期化を定義します。

次のコード例は、Initialize の実装を示しています。

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

前のコード例では、クライアントドライバーはデバイスオブジェクトを作成し、デバイスのコールバックを登録します。 デバイスオブジェクトを作成する前に、ドライバーは[**Iwdfdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスポインターでメソッドを呼び出すことによって、構成設定を指定します。 これは、クライアントドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドの前の呼び出しでフレームワークによって渡されたポインターと同じです。

クライアントドライバーは、デバイスオブジェクトの電源ポリシー所有者であることを指定します。 クライアントドライバーは、電源ポリシーの所有者として、システムの電源状態が変化したときにデバイスが入力する適切な電源の状態を決定します。 また、ドライバーは、電源状態を移行するために、関連する要求をデバイスに送信する役割も担います。 既定では、UMDF ベースのクライアントドライバーは、電源ポリシーの所有者ではありません。フレームワークは、すべての電源状態遷移を処理します。 システムがスリープ状態になると、フレームワークによってデバイスが**D3**に自動的に送信され、その逆に、システムが**S0**の状態になったときにデバイスが**D0**に戻されます。 詳細については、「 [UMDF の電源ポリシーの所有権](https://docs.microsoft.com/windows-hardware/drivers/wdf/power-policy-ownership-in-umdf)」を参照してください。

もう1つの構成オプションは、クライアントドライバーがフィルタードライバーであるか、デバイスの関数ドライバーであるかを指定することです。 このコード例では、クライアントドライバーが明示的に設定を指定していないことに注意してください。 これは、クライアントドライバーが関数ドライバーであり、フレームワークがデバイススタックに FDO を作成する必要があることを意味します。 クライアントドライバーがフィルタードライバーである場合、ドライバーは[**Iwdfdeviceinitialize:: SetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter)メソッドを呼び出す必要があります。 その場合は、フレームワークによってデバイススタックに FiDO が作成されます。

クライアントドライバーは、クライアントドライバーのコールバックに対するフレームワークの呼び出しが同期されていないことも指定します。 クライアントドライバーは、すべての同期タスクを処理します。 この設定を指定するために、クライアントドライバーは[**Iwdfdeviceinitialize:: Setロック制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)メソッドを呼び出します。

次に、クライアントドライバーは、 [**iunknown:: QueryInterface**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))を呼び出すことによって、デバイスコールバッククラスへの[**iunknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)ポインターを取得します。 その後、クライアントドライバーは[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出します。これにより、フレームワークデバイスオブジェクトが作成され、 **IUnknown**ポインターを使用してクライアントドライバーのデバイスコールバックが登録されます。

クライアントドライバーは、デバイスコールバッククラスのプライベートデータメンバーに ( [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)呼び出しを通じて受信された) デバイスオブジェクトのアドレスを格納し、DriverSafeRelease を呼び出してその参照を解放することに注意してください (inline関数は内部 .h で定義されています)。 これは、デバイスオブジェクトの有効期間がフレームワークによって追跡されるためです。 そのため、デバイスオブジェクトの追加の参照カウントを保持するために、クライアントドライバーは必要ありません。

テンプレートコードは、デバイスインターフェイス GUID を登録し、キューを設定するパブリックメソッド構成を定義します。 次のコード例は、デバイスコールバッククラス CMyDevice の Configure メソッドの定義を示しています。 Configure は、フレームワークデバイスオブジェクトが作成された後に、 [**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)によって呼び出されます。

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

前のコード例では、クライアントドライバーは主に2つのタスクを実行します。 i/o フローのキューの初期化と、デバイスインターフェイス GUID の登録です。

キューは、CMyIoQueue クラスで作成され、構成されます。 最初のタスクでは、CreateInstanceAndInitialize という名前の静的メソッドを呼び出して、そのクラスをインスタンス化します。 クライアントドライバーは、キューを初期化するように構成を呼び出します。 CreateInstanceAndInitialize と Configure は CMyIoQueue で宣言されています。これについては、このトピックの後半で説明します。

また、クライアントドライバーは、 [**Iwdfdevice:: CreateDeviceInterface**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea)を呼び出して、クライアントドライバーのデバイスインターフェイス GUID を登録します。 アプリケーションでは、GUID を使用してクライアントドライバーに要求を送信できます。 GUID 定数は内部 .h で宣言されています。

**IPnpCallbackHardware の実装と USB 固有のタスク**

次に、 [**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)でのインターフェイスの実装について説明します。

すべてのデバイスコールバッククラスは、 [**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)インターフェイスを実装する必要があります。 このインターフェイスには、 [**IPnpCallbackHardware:: OnIPnpCallbackHardware hardware**](https://msdn.microsoft.com/library/windows/hardware/ff556764_onpreparehardware)と[ **:: onpreparehardware**](https://msdn.microsoft.com/library/windows/hardware/ff556764_onreleasehardware)の2つのメソッドがあります。 このフレームワークは、PnP マネージャーがデバイスを起動したときと、デバイスを削除したときの2つのイベントに応答して、これらのメソッドを呼び出します。 デバイスが起動すると、ハードウェアへの通信が確立されますが、デバイスが動作状態 (**D0**) に入っていません。 このため、 **IPnpCallbackHardware:: On hardware**では、クライアントドライバーは、ハードウェアからデバイス情報を取得し、リソースを割り当て、ドライバーの有効期間中に必要なフレームワークオブジェクトを初期化することができます。 PnP マネージャーによってデバイスが削除されると、ドライバーはシステムからアンロードされます。 このフレームワークは、ドライバーがこれらのリソースとフレームワークオブジェクトを解放できる、クライアントドライバーの**IPnpCallbackHardware:: OnReleaseHardware**実装を呼び出します。

Pnp マネージャーは、PnP 状態の変更によって発生する他の種類のイベントを生成できます。 フレームワークは、これらのイベントに対して既定の処理を提供します。 クライアントドライバーは、これらのイベントの処理に参加することを選択できます。 USB デバイスがホストから切断されているシナリオを考えてみましょう。 PnP マネージャーはそのイベントを認識し、フレームワークに通知します。 クライアントドライバーがイベントに応答して追加のタスクを実行する必要がある場合、ドライバーは、デバイスコールバッククラスの[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)インターフェイスと関連する[**IPnpCallback:: OnSurpriseRemoval**](https://msdn.microsoft.com/library/windows/hardware/ff556762_onsurpriseremoval)メソッドを実装する必要があります。 それ以外の場合、フレームワークはイベントの既定の処理を続行します。

USB クライアントドライバーは、サポートされているインターフェイス、代替設定、およびエンドポイントに関する情報を取得し、データ転送の i/o 要求を送信する前にそれらを構成する必要があります。 UMDF には、クライアントドライバーの多くの構成タスクを簡略化する、特殊な i/o ターゲットオブジェクトが用意されています。 USB デバイスを構成するには、PnP マネージャーがデバイスを起動した後にのみ使用可能なデバイス情報がクライアントドライバーに必要です。

このテンプレートコードは、 [**IPnpCallbackHardware:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)メソッドでこれらのオブジェクトを作成します。

通常、クライアントドライバーは、デバイスの設計に応じて、次の1つまたは複数の構成タスクを実行します。

1.  インターフェイスの数など、現在の構成に関する情報を取得します。 フレームワークは、USB デバイスの最初の構成を選択します。 複数構成のデバイスの場合、クライアントドライバーで別の構成を選択することはできません。
2.  エンドポイントの数などのインターフェイスに関する情報を取得します。
3.  インターフェイスが複数の設定をサポートしている場合は、各インターフェイス内の代替設定を変更します。 既定では、フレームワークは、USB デバイスの最初の構成で各インターフェイスの最初の代替設定を選択します。 クライアントドライバーは、別の設定を選択することができます。
4.  各インターフェイス内のエンドポイントに関する情報を取得します。

これらのタスクを実行するために、クライアントドライバーは、WDF によって提供されるこれらの特殊な USB i/o ターゲットオブジェクトを使用できます。

| USB i/o ターゲットオブジェクト     | 説明                                                                                                                                                                                                                                                                                                                               | UMDF インターフェイス                                  |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| *ターゲットデバイスオブジェクト*    | USB デバイスを表し、デバイス記述子を取得し、デバイスに制御要求を送信するためのメソッドを提供します。                                                                                                                                                                                                             | [IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) |
| *ターゲットインターフェイスオブジェクト* | 個々のインターフェイスを表し、クライアントドライバーが別の設定を選択して設定に関する情報を取得するために呼び出すことができるメソッドを提供します。                                                                                                                                                                          | [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)       |
| *ターゲットパイプオブジェクト*      | インターフェイスの現在の代替設定で構成されているエンドポイントの個々のパイプを表します。 USB バスドライバーは、選択された構成内の各インターフェイスを選択し、インターフェイス内の各エンドポイントへの通信チャネルを設定します。 USB 用語では、その通信チャネルは*パイプ*と呼ばれます。 | [IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)     |



次のコード例は、 [**IPnpCallbackHardware:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)の実装を示しています。

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

フレームワークの USB i/o ターゲットオブジェクトを使用するには、まず、クライアントドライバーで USB ターゲットデバイスオブジェクトを作成する必要があります。 フレームワークオブジェクトモデルでは、USB ターゲットデバイスオブジェクトは、USB デバイスを表すデバイスオブジェクトの子です。 USB ターゲットデバイスオブジェクトは、フレームワークによって実装され、構成の選択など、USB デバイスのすべてのデバイスレベルのタスクを実行します。

前のコード例では、クライアントドライバーは、フレームワークデバイスオブジェクトに対してクエリを行い、USB ターゲットデバイスオブジェクトを作成するクラスファクトリへの[**IWDFUsbTargetFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetfactory)ポインターを取得します。 クライアントドライバーは、そのポインターを使用して[**IWDFUsbTargetDevice:: CreateUsbTargetDevice**](https://msdn.microsoft.com/library/windows/hardware/ff560387_createusbtargetdevice)メソッドを呼び出します。 メソッドは、USB ターゲットデバイスオブジェクトを作成し、 [**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)インターフェイスへのポインターを返します。 また、メソッドは、既定 (最初) の構成と、その構成内の各インターフェイスの代替設定0を選択します。

テンプレートコードは、デバイスコールバッククラスのプライベートデータメンバーで ( [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)呼び出しを通じて受信された) USB ターゲットデバイスオブジェクトのアドレスを格納し、DriverSafeRelease を呼び出してその参照を解放します。 USB ターゲットデバイスオブジェクトの参照カウントは、フレームワークによって管理されます。 オブジェクトは、デバイスオブジェクトが生きている間は生きています。 クライアントドライバーは、 [**IPnpCallbackHardware:: OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)内の参照を解放する必要があります。

クライアントドライバーは、USB ターゲットデバイスオブジェクトを作成した後、次のタスクを実行する[**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)メソッドを呼び出します。

-   デバイス、構成、インターフェイス記述子、およびデバイス速度などのその他の情報を取得します。
-   書式設定し、i/o 制御要求を既定のエンドポイントに送信します。
-   USB デバイス全体の電源ポリシーを設定します。

詳細については、「 [UMDF での USB デバイスの操作](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices-in-umdf-1-x-drivers)」を参照してください。
次のコード例は、 [**IPnpCallbackHardware:: OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)の実装を示しています。

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

## <a name="queue-source-code"></a>キューのソースコード


*Framework queue オブジェクト*は、特定のフレームワークデバイスオブジェクトの i/o キューを表します。 Queue オブジェクトの完全なソースコードは、IoQueue. h と IoQueue .c にあります。

**IoQueue. h**

ヘッダーファイル IoQueue. h は、キューコールバッククラスを宣言します。

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

前のコード例では、クライアントドライバーがキューコールバッククラスを宣言しています。 インスタンス化されると、オブジェクトは、要求がクライアントドライバーにディスパッチされる方法を処理するフレームワークキューオブジェクトと提携します。 クラスは、フレームワークキューオブジェクトを作成および初期化する2つのメソッドを定義します。 静的メソッド CreateInstanceAndInitialize は、キューコールバッククラスをインスタンス化し、その後、フレームワークキューオブジェクトを作成および初期化する Initialize メソッドを呼び出します。 また、queue オブジェクトのディスパッチオプションも指定します。

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

Initialize メソッドの実装を次のコード例に示します。

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

前のコード例では、クライアントドライバーがフレームワークキューオブジェクトを作成します。 フレームワークには、クライアントドライバーへの要求フローを処理するキューオブジェクトが用意されています。

オブジェクトを作成するために、クライアントドライバーは、Iwdfdevice [ **:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を以前に呼び出したときに[**取得した**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)Iwdfdevice [ **:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)を呼び出します。

[**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)呼び出しでは、フレームワークがキューを作成する前に、クライアントドライバーが特定の構成オプションを指定します。 これらのオプションは、キューが電源管理されているかどうかを判断し、長さがゼロの要求を許可し、ドライバーの既定のキューとして機能します。 クライアントドライバーは、次の一連の情報を提供します。

-   キューコールバッククラスへの参照

    キューコールバッククラスへの[**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)ポインターを指定します。 これにより、フレームワークキューオブジェクトとクライアントドライバーのキューコールバックオブジェクトの間のパートナーシップが作成されます。 I/o マネージャーは、アプリケーションから新しい要求を受信すると、フレームワークに通知します。 次に、フレームワークは**IUnknown**ポインターを使用して、キューコールバックオブジェクトによって公開されているパブリックメソッドを呼び出します。

-   既定のキューまたはセカンダリキュー

    キューは、既定のキューまたはセカンダリキューのいずれかである必要があります。 フレームワークキューオブジェクトが既定のキューとして機能する場合は、すべての要求がキューに追加されます。 セカンダリキューは、特定の種類の要求専用です。 クライアントドライバーがセカンダリキューを要求する場合、ドライバーは[**Iwdfdevice:: ConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-configurerequestdispatching)メソッドを呼び出して、フレームワークが指定されたキューに配置する必要がある要求の種類を示す必要もあります。 テンプレートコードでは、クライアントドライバーは*Bdefaultqueue*パラメーターに FALSE を渡します。 これは、既定のキューではなく、セカンダリキューを作成するようにメソッドに指示します。 後で**Iwdfdevice:: ConfigureRequestDispatching**を呼び出して、キューにデバイス i/o 制御要求のみが必要であることを示します (このセクションのコード例を参照してください)。

-   ディスパッチの種類

    キューオブジェクトのディスパッチ型によって、フレームワークがクライアントドライバーに要求を配信する方法が決まります。 配信メカニズムは、順次、並列、またはクライアントドライバーによって定義されたカスタムメカニズムによって実現できます。 順次キューの場合、クライアントドライバーが前の要求を完了するまで、要求は配信されません。 並列ディスパッチモードでは、フレームワークは、i/o マネージャーから到着するとすぐに要求を転送します。 これは、クライアントドライバーが別の要求を処理している間に要求を受信できることを意味します。 カスタムメカニズムでは、クライアントは、ドライバーが処理できるようになったときに、フレームワークキューオブジェクトから次の要求を手動でプルします。 テンプレートコードでは、クライアントドライバーはパラレルディスパッチモードを要求します。

-   電源管理キュー

    フレームワークキューオブジェクトは、デバイスの PnP と電源の状態と同期する必要があります。 デバイスが動作状態でない場合、フレームワークキューオブジェクトはすべての要求のディスパッチを停止します。 デバイスが動作中の状態になると、キューオブジェクトがディスパッチを再開します。 電源管理キューでは、同期はフレームワークによって実行されます。それ以外の場合、クライアントドライブはそのタスクを処理する必要があります。 テンプレートコードでは、クライアントは電源管理キューを要求します。

-   長さ0の要求が許可されています

    クライアントドライバーは、バッファーをキューに配置するのではなく、長さが0のバッファーで i/o 要求を完了するようにフレームワークに指示できます。 テンプレートコードでは、クライアントは、このような要求を完了するようにフレームワークに要求します。

1つのフレームワークキューオブジェクトは、読み取り、書き込み、デバイス i/o 制御など、いくつかの種類の要求を処理できます。 テンプレートコードに基づくクライアントドライバーは、デバイスの i/o 制御要求のみを処理できます。 そのために、クライアントドライバーのキューコールバッククラスは、 [**IQueueCallbackDeviceIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)インターフェイスとその[**IQueueCallbackDeviceIoControl:: OnDeviceIoControl**](https://msdn.microsoft.com/library/windows/hardware/ff556852_ondeviceiocontrol)メソッドを実装します。 これにより、フレームワークがデバイス i/o 制御要求を処理するときに、フレームワークは**IQueueCallbackDeviceIoControl:: OnDeviceIoControl**のクライアントドライバーの実装を呼び出すことができます。

その他の種類の要求では、クライアントドライバーは対応する**Iqueuecallbackxxx**インターフェイスを実装する必要があります。 たとえば、クライアントドライバーが読み取り要求を処理する場合、キューコールバッククラスは[**iqueuecallbackread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackread)インターフェイスとその[**Iqueuecallbackread:: onread**](https://msdn.microsoft.com/library/windows/hardware/ff556872_onread)メソッドを実装する必要があります。 要求とコールバックインターフェイスの種類の詳細については、「 [I/o キューイベントコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/wdf/i-o-queue-event-callback-functions)」を参照してください。

次のコード例は、 [**IQueueCallbackDeviceIoControl:: OnDeviceIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)の実装を示しています。

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

キューメカニズムのしくみを見てみましょう。 アプリケーションは、USB デバイスと通信するために、まずデバイスへのハンドルを開き、特定の制御コードを使用して[**DeviceIoControl**](https://docs.microsoft.com/previous-versions/windows/desktop/api/deviceaccess/nn-deviceaccess-ideviceiocontrol)関数を呼び出すことによって、デバイスの i/o 制御要求を送信します。 コントロールコードの種類に応じて、アプリケーションはその呼び出しで入力バッファーと出力バッファーを指定できます。 この呼び出しは、最終的には、フレームワークに通知する i/o マネージャーによって受信されます。 フレームワークは、フレームワークの要求オブジェクトを作成し、フレームワークの queue オブジェクトに追加します。 テンプレートコードでは、キューオブジェクトは WdfIoQueueDispatchParallel フラグを使用して作成されているので、要求がキューに追加されるとすぐにコールバックが呼び出されます。

フレームワークは、クライアントドライバーのイベントコールバックを呼び出すときに、アプリケーションによって送信された要求 (およびその入力バッファーと出力バッファー) を保持するフレームワークの要求オブジェクトにハンドルを渡します。 さらに、その要求を含むフレームワークキューオブジェクトへのハンドルを送信します。 イベントコールバックでは、クライアントドライバーは必要に応じて要求を処理します。 テンプレートコードは単に要求を完了します。 クライアントドライバーは、さらに複雑なタスクを実行できます。 たとえば、アプリケーションが特定のデバイス情報を要求した場合、イベントコールバックでは、クライアントドライバーは USB コントロール要求を作成し、USB ドライバースタックに送信して、要求されたデバイス情報を取得できます。 Usb 制御の要求については、「 [Usb 制御転送](usb-control-transfer.md)」で説明します。

## <a name="driver-entry-source-code"></a>ドライバーエントリのソースコード


テンプレートコードでは、ドライバーエントリは Dllsup に実装されています。

**Dllsup .cpp**

Include セクションの後に、クライアントドライバーの GUID 定数が宣言されています。 この GUID は、ドライバーのインストールファイル (INF) の GUID と一致している必要があります。

```ManagedCPlusPlus
const CLSID CLSID_Driver =
{0x079e211c,0x8a82,0x4c16,{0x96,0xe2,0x2d,0x28,0xcf,0x23,0xb7,0xff}};
```

次のコードブロックでは、クライアントドライバーのクラスファクトリを宣言します。

```ManagedCPlusPlus
class CMyDriverModule :
    public CAtlDllModuleT< CMyDriverModule >
{
};

CMyDriverModule _AtlModule;
```

テンプレートコードは ATL サポートを使用して、複雑な COM コードをカプセル化します。 クラスファクトリは、クライアントドライバーを作成するために必要なすべてのコードを含む、テンプレートクラス CAtlDllModuleT を継承します。

次のコードスニペットは、DllMain の実装を示しています。

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

クライアントドライバーで[*dllmain*](https://docs.microsoft.com/windows/desktop/Dlls/dllmain)関数が実装されている場合、Windows は、 *dllmain*をクライアントドライバーモジュールのエントリポイントと見なします。 Windows は、WUDFHost .exe でクライアントドライバーモジュールを読み込んだ後に、 *DllMain*を呼び出します。 Windows は、Windows がクライアントドライバーをメモリにアンロードする直前に、 *DllMain*を再度呼び出します。 *DllMain*は、ドライバーレベルでグローバル変数を割り当てて解放できます。 テンプレートコードでは、クライアントドライバーは、WPP トレースに必要なリソースを初期化して解放し、ATL クラスの DllMain 実装を呼び出します。

[*Dllmain*](https://docs.microsoft.com/windows/desktop/Dlls/dllmain)の記述方法については、「 [dllmain の実装](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/implementing-dllmain)」を参照してください。

次のコードスニペットは、DllGetClassObject の実装を示しています。

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

テンプレートコードでは、クラスファクトリと[**DllGetClassObject**](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject)が ATL に実装されています。 上記のコードスニペットは、単純に ATL **DllGetClassObject**実装を呼び出します。 一般に、 **DllGetClassObject**では次のタスクを実行する必要があります。

1.  フレームワークによって渡される CLSID がクライアントドライバーの GUID であることを確認します。 フレームワークは、ドライバーの INF ファイルからクライアントドライバーの CLSID を取得します。 検証中に、指定した GUID が INF で指定した GUID と一致していることを確認します。
2.  クライアントドライバーによって実装されたクラスファクトリをインスタンス化します。 テンプレートコードでは、これは ATL クラスによってカプセル化されます。
3.  クラスファクトリの[**IClassFactory**](https://docs.microsoft.com/windows/desktop/api/unknwnbase/nn-unknwnbase-iclassfactory)インターフェイスへのポインターを取得し、取得したポインターをフレームワークに返します。

クライアントドライバーモジュールがメモリに読み込まれた後、フレームワークはドライバーによって提供された[**DllGetClassObject**](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject)関数を呼び出します。 フレームワークによる**DllGetClassObject**の呼び出しでは、クライアントドライバーを識別する CLSID を渡し、クラスファクトリの[**IClassFactory**](https://docs.microsoft.com/windows/desktop/api/unknwnbase/nn-unknwnbase-iclassfactory)インターフェイスへのポインターを要求します。 クライアントドライバーは、ドライバーコールバックの作成を容易にするクラスファクトリを実装します。 したがって、クライアントドライバーは、少なくとも1つのクラスファクトリを含んでいる必要があります。 次に、フレームワークは[**IClassFactory:: CreateInstance**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iclassfactory-createinstance)を呼び出し、ドライバーコールバッククラスへの[**Idriverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)ポインターを要求します。

**.Def をエクスポートします。**

フレームワークが[**DllGetClassObject**](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject)を呼び出すためには、クライアントドライバーが .def ファイルから関数をエクスポートする必要があります。 ファイルは既に Visual Studio プロジェクトに含まれています。

```ManagedCPlusPlus
; Exports.def : Declares the module parameters.

LIBRARY     "MyUSBDriver_UMDF_.DLL"

EXPORTS
        DllGetClassObject   PRIVATE
```

ドライバーのプロジェクトに含まれている Export.def から前のコード スニペットで、クライアントが、ライブラリとドライバーのモジュールの名前と[ **DllGetClassObject** ](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject)エクスポート します。 詳細については、「 [DEF ファイルを使用した DLL からのエクスポート](https://www.microsoft.com/download/details.aspx?id=55984)」を参照してください。








