---
title: "\"Hello World\" WIA ミニドライバー UI 拡張機能の作成"
description: "\"Hello World\" WIA ミニドライバー UI 拡張機能の作成"
ms.assetid: 8de1f8ca-f618-44d7-b6dd-c02cdee8a556
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: d1082eac8969fdaf51fedb6da972f5adc5bdde84
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223528"
---
# <a name="creating-a-hello-world-wia-minidriver-ui-extension"></a>"Hello World" WIA ミニドライバー UI 拡張機能の作成

WIA ミニドライバー UI 拡張機能は、いくつかの関数をエクスポートし、次の4つの COM インターフェイス識別子 (IID) の少なくとも1つを実装する単純な DLL です。

**IID \_ iwi# iextension**

**Iwiの**インターフェイス識別子 (IID) インターフェイス。 これは、マイコンピューターおよびコントロールパネルのミニドライバーデバイスアイコンを置き換えるために使用される標準的な WIA インターフェイスであり、Microsoft common ミニドライバー UI ダイアログを置き換えます。

**IID \_ ishellextinit**

**Ishellextinit**インターフェイスの IID。 これは、プロパティシート、ショートカットメニュー、およびドラッグアンドドロップハンドラー (既定以外のドラッグアンドドロップ操作中にショートカットメニューに項目を追加する拡張機能) のシェル拡張を初期化するために使用される標準の Windows シェルインターフェイスです。

**IID \_ IContextMenu**

**ContextMenu**インターフェイスの IID。 これは、シェルオブジェクトに関連付けられているショートカットメニューを作成または結合するために使用される標準の Windows シェルインターフェイスです (マイコンピューターおよびコントロールパネルの [WIA ミニドライバー] アイコン)。

**IID \_ ishellpropsheet**

**Ishellpropsheet**インターフェイスの IID。 これは、シェルオブジェクトに対して表示されるプロパティシート内のページを追加または置換するために使用される標準の Windows シェルインターフェイスです (マイコンピューターおよびコントロールパネルの WIA ミニドライバーアイコン)。

"Hello World" WIA ミニドライバー UI 拡張機能は、次のファイルで構成されています。

*/. .inf*

これはインストールファイルです (この UI 拡張機能*を元の*モジュールのサンプルと共にインストールするように変更されています)。

*hellowldui*

これは、 **DllGetClassObject**と**DllCanUnloadNow**という2つの COM エクスポートを含む定義ファイルです (どちらも Windows SDK のドキュメントで説明されています)。

*hellowldui*

これは、WIA UI 拡張の実装です。

## <a name="installing-wia-ui-extensions"></a>WIA UI 拡張機能のインストール

WIA UI 拡張 DLL をインストールするには、[ui**クラス ID =**] を追加し、 &lt; [ui 拡張機能の dll の CLSID] を、 &gt; [ **devicedata** ] セクションの下にある INF ファイルに追加します。 この CLSID を使用すると、クライアントは、(Microsoft Windows SDK のドキュメントで説明されている) **CoCreateInstance**を呼び出し、WIA UI 拡張機能でサポートされているインターフェイスを取得できます。

次の例の INF スニペットは、 [' Hello World ' Wia ミニドライバーを作成するとき](creating-a---hello-world---wia-minidriver.md)に、wia ミニドライバーサンプルから派生しています。 既定で使用される CLSID は、コモンダイアログ、アイコン、およびプロパティページに対して、Microsoft が提供する CLSID である必要があります。

インストールを容易にするために、すべての WIA UI 拡張 Dll が COM オブジェクトを自己登録することをお勧めします。 このサンプルには、自己登録 COM オブジェクトが含まれていません。

```INF
[WIADevice.DeviceData]
Server=local
UI DLL=sti.dll
UI Class ID={4DB1AD10-3391-11D2-9A33-00C04FA36145}
```

次のサンプルは、 **Ui クラス ID**サブキーを*Hellowldui* sample UI 拡張機能の CLSID に設定する完全な INF ファイルです。

```INF
; HELLOWLD.INF  -- Hello World WIA Minidriver setup file (with a WIA UI extension DLL)
; Copyright (c) 2002 Hello World Company
; Manufacturer:  Hello World Company

[Version]
Signature="$WINDOWS NT$"
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%Mfg%
DriverVer=06/26/2001,1.0
CatalogFile=wia.cat

[DestinationDirs]
DefaultDestDir=11

[Manufacturer]
%Mfg%=Models

[Models]
%WIADevice.DeviceDesc% = WIADevice.Scanner, HELLOWORLD_PNP_ID

[WIADevice.Scanner]
Include=sti.inf
Needs=STI.SerialSection
SubClass=StillImage
DeviceType=1
DeviceSubType=0x0
Capabilities=0x30
DeviceData=WIADevice.DeviceData
AddReg=WIADevice.AddReg
CopyFiles=WIADevice.CopyFiles
ICMProfiles="sRGB Color Space Profile.icm"

[WIADevice.Scanner.Services]
Include=sti.inf
Needs=STI.SerialSection.Services

[WIADevice.DeviceData]
Server=local
UI DLL=sti.dll
UI Class ID={7C1E2309-A535-45b1-94B3-9A020EE600C7}

[WIADevice.AddReg]
HKR,,HardwareConfig,1,1
HKR,,USDClass,,"{7C1E2309-A535-45b1-94B3-9A020EE600C6}"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6},,,"Hello World WIA Minidriver"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6}\InProcServer32,,,%11%\hellowld.dll
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6}\InProcServer32,ThreadingModel,,Both

HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7},,,"Hello World WIA Minidriver UI Extension"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7}\InProcServer32,,,%11%\hellowldui.dll
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7}\InProcServer32,ThreadingModel,,Both
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7}\shellex\WiaDialogExtensionHandlers\{7C1E2309-A535-45b1-94B3-9A020EE600C7}

[WIADevice.CopyFiles]
hellowld.dll
hellowldui.dll

[SourceDisksFiles.x86]
hellowld.dll=1
hellowldui.dll=1

[SourceDisksNames.x86]
1=%Location%,,,

[SourceDisksFiles.IA64]
hellowld.dll=1
hellowldui.dll=1
[SourceDisksNames.IA64]
1=%Location%,,,

[Strings]
Mfg="Hello World Company"
WIADevice.DeviceDesc="Hello World WIA Minidriver"
Location="Hello World WIA Minidriver Installation Source"
```

*Hellowldui*ファイルには、次のものが含まれている必要があります。

```make
LIBRARY HELLOWLDUI

EXPORTS
        DllGetClassObject   PRIVATE
        DllCanUnloadNow     PRIVATE
```

*Hellowldui*ファイルには、次のものが含まれている必要があります。

```cpp
#ifndef WIN32_LEAN_AND_MEAN
#define WIN32_LEAN_AND_MEAN
#endif

#include <windows.h>
#include <initguid.h>
#include <wiadevd.h>
#include <shobjidl.h>
#include <shlobj.h>

// {7C1E2309-A535-45b1-94B3-9A020EE600C7}
DEFINE_GUID(CLSID_HelloWorldWIAUIExtension, 0x7c1e2309, 0xa535, 0x45b1, 0x94, 0xb3, 0x9a, 0x2, 0xe, 0xe6, 0x0, 0xc7);

class CWIAUIExtension : public IWiaUIExtension,   // WIA UI Extension interface
                        public IShellExtInit,     // SHELL Extension interface
                        public IContextMenu,      // SHELL context menu Extension interface
                        public IShellPropSheetExt // SHELL property sheet interface
{
public:

    /////////////////////////////////////////////////////////////////////////
    // Construction/Destruction Section                                    //
    /////////////////////////////////////////////////////////////////////////

    CWIAUIExtension() : m_cRef(1) {
    }

    ~CWIAUIExtension() {
    }

private:
    LONG m_cRef; // object reference count.
public:

    /////////////////////////////////////////////////////////////////////////
    // Standard COM Section                                                //
    /////////////////////////////////////////////////////////////////////////

    STDMETHODIMP QueryInterface(REFIID  riid,LPVOID  *ppvObj)
    {
        if (!ppvObj) {
            return E_INVALIDARG;
        }

        *ppvObj = NULL;

        if (IsEqualIID( riid, IID_IUnknown )) {
            *ppvObj = reinterpret_cast<IUnknown*>(this);
        } else if (IsEqualIID( riid, IID_IWiaUIExtension )) {
            *ppvObj = static_cast<IWiaUIExtension*>(this);
        } else {
            return E_NOINTERFACE;
        }

        reinterpret_cast<IUnknown*>(*ppvObj)->AddRef();
        return S_OK;
    }

    STDMETHODIMP_(ULONG) AddRef()
    {
        return InterlockedIncrement(&m_cRef);
    }

    STDMETHODIMP_(ULONG) Release()
    {
        if(InterlockedDecrement(&m_cRef) == 0) {
        delete this;
            return 0;
        }
        return m_cRef;
    }

    /////////////////////////////////////////////////////////////////////////
    // IWiaUIExtension Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP DeviceDialog( PDEVICEDIALOGDATA pDeviceDialogData ) {return E_NOTIMPL;}
    STDMETHODIMP GetDeviceIcon( BSTR bstrDeviceId, HICON *phIcon, ULONG nSize ){
 HRESULT hr = E_NOTIMPL;
        HICON hIcon = reinterpret_cast<HICON>(LoadImage(NULL,
                                                        MAKEINTRESOURCE(IDI_APPLICATION),
                                                        IMAGE_ICON,
                                             nSize,
                                                        nSize,
                                                        LR_SHARED));
        if (hIcon) {
            *phIcon = CopyIcon(hIcon);
            hIcon = NULL;
            hr = S_OK;
        }
        return hr;
    }
    STDMETHODIMP GetDeviceBitmapLogo( BSTR bstrDeviceId, HBITMAP *phBitmap, ULONG nMaxWidth, ULONG nMaxHeight ){return E_NOTIMPL;}

    /////////////////////////////////////////////////////////////////////////
    // IShellExtInit Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP Initialize (LPCITEMIDLIST pidlFolder,LPDATAOBJECT lpdobj,HKEY hkeyProgID){return E_NOTIMPL;}

    /////////////////////////////////////////////////////////////////////////
    // IContextMenu Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP QueryContextMenu (HMENU hmenu,UINT indexMenu,UINT idCmdFirst,UINT idCmdLast,UINT uFlags) {return E_NOTIMPL;}
    STDMETHODIMP InvokeCommand    (LPCMINVOKECOMMANDINFO lpici){return E_NOTIMPL;}
    STDMETHODIMP GetCommandString (UINT_PTR idCmd, UINT uType,UINT* pwReserved,LPSTR pszName,UINT cchMax) {return E_NOTIMPL;}

    /////////////////////////////////////////////////////////////////////////
    // IShellPropSheetExt Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP AddPages (LPFNADDPROPSHEETPAGE lpfnAddPage,LPARAM lParam){return E_NOTIMPL;}
    STDMETHODIMP ReplacePage (UINT uPageID,LPFNADDPROPSHEETPAGE lpfnReplacePage,LPARAM lParam) {return E_NOTIMPL;}
};

/////////////////////////////////////////////////////////////////////////
// IClassFactory Interface Section (for all COM objects)               //
/////////////////////////////////////////////////////////////////////////

class CWIAUIClassFactory : public IClassFactory {
public:
    CWIAUIClassFactory() : m_cRef(1) {}
    ~CWIAUIClassFactory(){}
    STDMETHODIMP QueryInterface(REFIID riid, LPVOID *ppv)
    {
      if (!ppv) {
            return E_INVALIDARG;
        }

        *ppv = NULL;
        HRESULT hr = E_NOINTERFACE;
        if (IsEqualIID(riid, IID_IUnknown) || IsEqualIID(riid, IID_IClassFactory)) {
            *ppv = static_cast<IClassFactory*>(this);
            reinterpret_cast<IUnknown*>(*ppv)->AddRef();
            hr = S_OK;
        }
        return hr;
    }
    STDMETHODIMP_(ULONG) AddRef()
    {
        return InterlockedIncrement(&m_cRef);
    }
    STDMETHODIMP_(ULONG) Release()
    {
  if(InterlockedDecrement(&m_cRef) == 0) {
            delete this;
            return 0;
        }
        return m_cRef;
    }
    STDMETHODIMP CreateInstance(IUnknown __RPC_FAR *pUnkOuter,REFIID riid,void __RPC_FAR *__RPC_FAR *ppvObject)
    {
        if ((pUnkOuter)&&(!IsEqualIID(riid,IID_IUnknown))) {
            return CLASS_E_NOAGGREGATION;
        }

        HRESULT hr = E_NOINTERFACE;
        CWIAUIExtension *pUIExt = new CWIAUIExtension();
        if (pUIExt) {
            hr = pUIExt->QueryInterface(riid,ppvObject);
            pUIExt->Release();
        } else {
            hr = E_OUTOFMEMORY;
        }

        return hr;
    }
    STDMETHODIMP LockServer(BOOL fLock){return S_OK;}
private:
    LONG m_cRef;
};

/////////////////////////////////////////////////////////////////////////
// DLL Entry Point Section (for all COM objects, in a DLL)             //
/////////////////////////////////////////////////////////////////////////

extern "C" __declspec(dllexport) BOOL APIENTRY DllEntryPoint(HINSTANCE hinst,DWORD dwReason,LPVOID lpReserved)
{
    switch (dwReason) {
    case DLL_PROCESS_ATTACH:
        break;
    }
    return TRUE;
}

extern "C" STDMETHODIMP DllCanUnloadNow(void){return S_OK;}
extern "C" STDAPI DllGetClassObject(REFCLSID rclsid,REFIID riid,LPVOID *ppv)
{
    if (!ppv) {
        return E_INVALIDARG;
    }
    HRESULT hr = CLASS_E_CLASSNOTAVAILABLE;
    if (IsEqualCLSID(rclsid, CLSID_HelloWorldWIAUIExtension)) {
        CWIAUIClassFactory *pcf = new CWIAUIClassFactory;
        if (pcf) {
            hr = pcf->QueryInterface(riid,ppv);
            pcf->Release();
        } else {
            hr = E_OUTOFMEMORY;
        }
    }
    return hr;
}
```

## <a name="adding-a-custom-device-icon"></a>カスタムデバイスアイコンの追加

前のサンプルは、デバイスの既定のアイコンを置き換える方法の例です。 既定のアイコンを置き換えることは、複数のデバイスがインストールされている場合に、適切なデバイスを使用するようにユーザーに指示するのに最適な方法です。 アイコンが接続されているデバイスに似ている場合、ユーザーにとって直観的にわかりやすくなります。
