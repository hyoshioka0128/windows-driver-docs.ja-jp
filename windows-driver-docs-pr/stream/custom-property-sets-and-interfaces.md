---
title: カスタム プロパティ セットとインターフェイス
description: カスタム プロパティ セットとインターフェイス
ms.assetid: ea1337e4-c8e5-4971-b602-c066b5a6fd07
keywords:
- インターフェイスの WDK ビデオのキャプチャ
- カスタム プロパティは、WDK のビデオ キャプチャを設定します。
- WDK AVStream ビデオ キャプチャは、プロパティを設定します。
- ビデオの WDK AVStream をキャプチャするには、プロパティを設定します。
- プロパティは、WDK のビデオ キャプチャを設定します。
- カスタム インターフェイス WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24114469e8dcf501be497ed9310e838b1c16c01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571404"
---
# <a name="custom-property-sets-and-interfaces"></a>カスタム プロパティ セットとインターフェイス


ベンダーは、デバイスに固有またはストリームに固有のパラメーターを制御するためのカスタム プロパティのセットを実装できます。 一般に、これらのカーネル プロパティ セットはによって公開される COM インターフェイスとしてカスタム*KsProxy*プラグイン DLL。 同様に、カスタム プロパティ ページを実装して、カスタム プロパティのセットを制御するためのユーザー インターフェイスを提供できます。

**カスタム プロパティのセットを作成するには**

1.  設定を使用して、プロパティの一意の GUID を作成する*Guidgen.exe*します。 (このツールは、Microsoft Windows SDK に含まれます)。

2.  ミニドライバー設定プロパティを実装します。

**プロパティ セットのカスタム COM インターフェイスまたはプロパティ ページを作成するには**

1.  COM インターフェイスまたはプロパティ ページを実装するカスタム KsProxy プラグイン DLL を作成します。 プラグイン DLL のクラス ID (CLSID) は、プロパティ セット GUID と一致する必要があります。 リンク*ksproxy.lib*の実装を取得する **:: KsSynchronousDeviceControl**します。

2.  公開する標準の Microsoft DirectShow メカニズムを追加*CFactoryTemplateg\_テンプレート*DLL インターフェイスの自己登録を許可するからです。

3.  このサンプルで示すように、COM インターフェイスとプロパティ ページを公開する、ハードウェアのデバイス インストール ファイル (INF ファイル) に行を追加*MyINF.inf*以下。

次のコードでは、IAMCameraControl の実装を示しています。

**Camera.h**

```cpp
/*
Implements IAMCameraControl via KSPROPERTY_VIDCAP_CAMERACONTROL
*/

class CCameraControlInterfaceHandler :
    public CUnknown,
    public IAMCameraControl {

public:
    DECLARE_IUNKNOWN;

    static CUnknown* CALLBACK CreateInstance(
        LPUNKNOWN UnkOuter,
        HRESULT* hr);

    CCameraControlInterfaceHandler(
        LPUNKNOWN UnkOuter,
        TCHAR* Name,
        HRESULT* hr);

    STDMETHODIMP NonDelegatingQueryInterface(
        REFIID riid,
        PVOID* ppv);

    STDMETHODIMP Set( 
            IN long Property,
            IN long lValue,
            IN long Flags);

private:
    HANDLE m_ObjectHandle;
};
```

**Camera.cpp**

```cpp
/*
Implements IAMCameraControl via KSPROPERTY_VIDCAP_CAMERACONTROL
*/

#include "pch.h"
#include "camera.h"

CUnknown*
CALLBACK
CCameraControlInterfaceHandler::CreateInstance(
    LPUNKNOWN   UnkOuter,
    HRESULT*    hr
    )
{
    CUnknown *Unknown;

    Unknown = new CCameraControlInterfaceHandler(UnkOuter, NAME("IAMCameraControl"), hr);
    if (!Unknown) {
        *hr = E_OUTOFMEMORY;
    }
    return Unknown;
} 

CCameraControlInterfaceHandler::CCameraControlInterfaceHandler(
    LPUNKNOWN   UnkOuter,
    TCHAR*      Name,
    HRESULT*    hr
    ) :
    CUnknown(Name, UnkOuter, hr)
{
    if (SUCCEEDED(*hr)) {
        if (UnkOuter) {
            IKsObject*  Object;
            *hr =  UnkOuter->QueryInterface(uuidof(IKsObject), reinterpret_cast<PVOID*>(&Object));
            if (SUCCEEDED(*hr)) {
                m_ObjectHandle = Object->KsGetObjectHandle();
                // m_Object handle is file handle of the driver
                if (!m_ObjectHandle) {
                    *hr = E_UNEXPECTED;
                }
                Object->Release();
            }
        } else {
            *hr = VFW_E_NEED_OWNER;
        }
    }
}

STDMETHODIMP
CCameraControlInterfaceHandler::Set(
     IN long Property,
     IN long lValue,
     IN long lFlags
     )
{
    KSPROPERTY_CAMERACONTROL_S  CameraControl;
    ULONG       BytesReturned;

 CameraControl.Property.Set = PROPSETID_VIDCAP_CAMERACONTROL;
 CameraControl.Property.Id = Property;
    CameraControl.Property.Flags = KSPROPERTY_TYPE_SET;
    CameraControl.Value = lValue;
 CameraControl.Flags = lFlags;
    CameraControl.Capabilities = 0;

 return ::KsSynchronousDeviceControl(
                m_ObjectHandle,
                IOCTL_KS_PROPERTY,
                &CameraControl,
                sizeof(CameraControl),
                &CameraControl,
                sizeof(CameraControl),
                &BytesReturned);
}

STDMETHODIMP
CCameraControlInterfaceHandler::NonDelegatingQueryInterface(
    REFIID  riid,
    PVOID*  ppv
    )
{
    if (riid == uuidof(IAMCameraControl)) {
        return GetInterface(static_cast<IAMCameraControl*>(this), ppv);
    }
    return CUnknown::NonDelegatingQueryInterface(riid, ppv);
}
```

**MyINF.inf**

```INF
;IAMCameraControl
HKCR,CLSID\{C6E13370-30AC-11d0-A18C-00A0C9118956},,,%PlugIn_IAMCameraControl%
HKCR,CLSID\{C6E13370-30AC-11d0-A18C-00A0C9118956}\InprocServer32,,,kswdmcap.ax
HKCR,CLSID\{C6E13370-30AC-11d0-A18C-00A0C9118956}\InprocServer32,ThreadingModel,,Both
; This IID is aggregated for the filter given the CLSID of the property set
HKLM,System\CurrentControlSet\Control\MediaInterfaces\{C6E13370-30AC-11d0-A18C-00A0C9118956},,,%PlugIn_IAMCameraControl%
HKLM,System\CurrentControlSet\Control\MediaInterfaces\{C6E13370-30AC-11d0-A18C-00A0C9118956},IID,1,70,33,E1,C6,AC,30,d0,11,A1,8C,00,A0,C9,11,89,56

; CameraControl Property Page
HKCR,CLSID\{71F96465-78F3-11d0-A18C-00A0C9118956},,,%PropPage_CameraControl%
HKCR,CLSID\{71F96465-78F3-11d0-A18C-00A0C9118956}\InprocServer32,,,kswdmcap.ax
HKCR,CLSID\{71F96465-78F3-11d0-A18C-00A0C9118956}\InprocServer32,ThreadingModel,,Both
; Associate the property set with the above property page
HKLM,System\CurrentControlSet\Control\MediaSets\{C6E13370-30AC-11d0-A18C-00A0C9118956}\PropertyPages\{71F96465-78F3-11d0-A18C-00A0C9118956},,,%PropPage_CameraControl%
```








