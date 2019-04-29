---
title: "\"Hello World\"WIA ミニドライバー UI 拡張機能の作成"
description: "\"Hello World\"WIA ミニドライバー UI 拡張機能の作成"
ms.assetid: 8de1f8ca-f618-44d7-b6dd-c02cdee8a556
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d164e80fab69b0333ba190cf033c3f32437405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386321"
---
# <a name="creating-a-hello-world-wia-minidriver-ui-extension"></a>"Hello World"WIA ミニドライバー UI 拡張機能の作成





WIA ミニドライバー UI 拡張機能は、いくつかの関数をエクスポートし、4 つ以下 COM インターフェイス識別子 (IID) の少なくとも 1 つを実装する単純な DLL を示します。

<a href="" id="iid-iwiauiextension"></a>IID\_IWiaUIExtension  
インターフェイス id (IID)、 **IWiaUIExtension**インターフェイス。 これは、Microsoft の一般的なミニドライバー UI ダイアログをミニドライバー デバイスのアイコンとコントロール パネルで、マイ コンピューターを置き換えるために使用標準 WIA インターフェイスです。

<a href="" id="iid-ishellextinit"></a>IID\_IShellExtInit  
IID、 **IShellExtInit**インターフェイス。 これは、標準の Windows シェルがプロパティ シート、ショートカット メニューのおよびドラッグ アンド ドロップ ハンドラー (既定以外のドラッグ アンド ドロップ操作中に、ショートカット メニューに項目を追加する拡張) のシェル拡張を初期化するために使用されるインターフェイスです。

<a href="" id="iid-icontextmenu"></a>IID\_IContextMenu  
IID、 **ContextMenu**インターフェイス。 これは、シェル オブジェクト (WIA ミニドライバーのアイコンとコントロール パネルの マイ コンピューター) に関連付けられたショートカット メニューのマージを作成または使用される標準の Windows シェル インターフェイスです。

<a href="" id="iid-ishellpropsheet"></a>IID\_IShellPropSheet  
IID、 **IShellPropSheet**インターフェイス。 これは、追加または置換するシェル オブジェクト (マイ コンピューター] と [コントロール パネルの WIA ミニドライバーのアイコン) の表示プロパティ シート内のページに使用される標準の Windows シェル インターフェイスです。

"Hello World"WIA ミニドライバー UI 拡張機能は、次のファイルで構成されます。

<a href="" id="hellowld-inf"></a>*hellowld.inf*  
これは、インストール ファイル (元のこの UI 拡張機能をインストールするように変更*hellowld*サンプル)。

<a href="" id="hellowldui-def"></a>*hellowldui.def*  
これは、定義ファイルを格納している 2 つの COM エクスポート**DllGetClassObject**と**DllCanUnloadNow** (両方が、Windows SDK のドキュメントで説明)。

<a href="" id="hellowldui-cpp"></a>*hellowldui.cpp*  
これは、WIA UI 拡張機能の実装です。

### <a name="installing-wia-ui-extensions"></a>WIA UI 拡張機能のインストール

WIA UI 拡張 DLL をインストールする追加**UI クラス ID =**{&lt;UI 拡張機能の DLL の CLSID&gt;} INF ファイルを**DeviceData**セクション。 クライアントの呼び出しにより、この CLSID **CoCreateInstance** (Microsoft Windows SDK のドキュメントで説明)、および、WIA UI 拡張機能のサポートされているインターフェイスを取得します。

次のスニペットの例の INF に WIA ミニドライバー サンプルから派生["Hello World"WIA のミニドライバーを作成する](creating-a---hello-world---wia-minidriver.md)します。 既定で使用される CLSID は、コモン ダイアログ ボックス、アイコン、およびプロパティ ページの CLSID は Microsoft が提供必要があります。

すべて WIA UI 拡張 Dll する必要があります自己登録をより簡単にインストールの昇格の COM オブジェクトをお勧めします。 このサンプルでは、自動登録の COM オブジェクトは含まれません。

```INF
[WIADevice.DeviceData]
Server=local
UI DLL=sti.dll
UI Class ID={4DB1AD10-3391-11D2-9A33-00C04FA36145}
```

次のサンプルは、完全な INF ファイルを設定する、 **UI クラス ID**サブキーの clsid、 *hellowldui* UI 拡張機能のサンプルです。

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

*Hellowldui.def*ファイルは、次を含める必要があります。

```make
LIBRARY HELLOWLDUI

EXPORTS
        DllGetClassObject   PRIVATE
        DllCanUnloadNow     PRIVATE
```

*Hellowldui.cpp*ファイルは、次を含める必要があります。

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

### <a name="adding-a-custom-device-icon"></a>カスタム デバイス アイコンの追加

上記のサンプルでは、デバイスの既定のアイコンを交換する方法の例を示します。 既定のアイコンを置き換えると、インストールされている 1 つ以上のデバイスがある場合に、適切なデバイスを使用してユーザーをガイドする理想的な方法を指定できます。 アイコンに接続しているデバイスが似ている場合は、ユーザーにとって直感的になります。

 

 




