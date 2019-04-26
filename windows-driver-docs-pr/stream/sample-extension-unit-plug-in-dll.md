---
title: サンプル拡張ユニット プラグイン DLL
description: サンプル拡張ユニット プラグイン DLL
ms.assetid: bd9ea70d-7bd0-494d-8d67-7a36a41d005b
keywords:
- プラグイン DLL WDK USB ビデオ クラス
- プラグイン DLL 単位数 WDK USB ビデオ クラス、サンプル、拡張機能
- サンプル コード WDK USB ビデオ クラスの拡張ユニット プラグイン DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bf245d4dac1ec8b886eca4ace2042950818b8e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360110"
---
# <a name="sample-extension-unit-plug-in-dll"></a>サンプル拡張ユニット プラグイン DLL


このトピックには、KS プロパティのセット上に COM API を公開する拡張ユニット プラグイン DLL のサンプル コードが含まれています。

サンプルと呼ばれるクラスを定義します。 **CExtension**、から派生した**CNodeControl**します。 実装、 **CNodeControl**クラスは後でも提供します。 **CNodeControl**から Microsoft が指定した派生**IKsNodeControl**インターフェイスで定義されている*Vidcap.h*します。

*Vidcap.ax*使用**IKsNodeControl**プラグイン拡張機能ノード ID の通知のインスタンスを備えた**IKsControl**します。 具体的には、プラグイン、この情報を受信呼び出しを通じて**CExtension::put\_NodeId**と**CExtension::put\_KsControl**します。 親クラスのこのトピックの「これらのメソッドの実装を見つけることができます**CNodeControl**します。

*Vidcap.h*夏 2004 DirectX SDK を 2005 年 2 月に表示されます[DirectX SDK](https://go.microsoft.com/fwlink/p/?linkid=51990)します。 これらのパッケージをインストールするときに取得するその他の機能をインストールする必要があります*Vidcap.h*します。

Windows Vista およびそれ以降のリリースで*Vidcap.h*は、Microsoft Windows SDK の一部として含まれています。

任意という名前のクラス ヘッダー ファイルに次のコードを含める*Xuproxy.h*:

```cpp
#include <ks.h>
#include <ksproxy.h>
#include <C:\Program Files\Microsoft DirectX 9.0 SDK (February 2005)\Extras\DirectShow\Include\vidcap.h>
#include <C:\Program Files\Microsoft DirectX 9.0 SDK (February 2005)\Extras\DirectShow\Include\ksmedia.h>

DEFINE_GUID(CLSID_ExtensionUnit, 0xzzzzzzzz, 0xzzzz, 0xzzzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz);

class CNodeControl :
    public IKsNodeControl
{
public:
    STDMETHOD(put_NodeId) (DWORD dwNodeId);
    STDMETHOD(put_KsControl) (PVOID pKsControl);

    DWORD m_dwNodeId;
    CComPtr<IKsControl> m_pKsControl;
};

class CExtension :
   public IExtensionUnit,
   public CComObjectRootEx<CComObjectThreadModel>,
   public CComCoClass<CExtension, &CLSID_ExtensionUnit>,
   public CNodeControl
{
   public:

   CExtension();
   STDMETHOD(FinalConstruct)();

   BEGIN_COM_MAP(CExtension)
      COM_INTERFACE_ENTRY(IKsNodeControl)
      COM_INTERFACE_ENTRY(IExtensionUnit)
   END_COM_MAP()

   DECLARE_PROTECT_FINAL_CONSTRUCT()
   DECLARE_NO_REGISTRY()
   DECLARE_ONLY_AGGREGATABLE(CExtension)

   // IExtensionUnit
   public:
   STDMETHOD (get_Info)(
      ULONG ulSize,
      BYTE pInfo[]);
   STDMETHOD (get_InfoSize)(
      ULONG *pulSize);
   STDMETHOD (get_PropertySize)(
      ULONG PropertyId, 
      ULONG *pulSize);
   STDMETHOD (get_Property)(
      ULONG PropertyId, 
      ULONG ulSize, 
      BYTE pValue[]);
   STDMETHOD (put_Property)(
      ULONG PropertyId, 
      ULONG ulSize, 
      BYTE pValue[]);
   STDMETHOD (get_PropertyRange)(
      ULONG PropertyId, 
      ULONG ulSize,
      BYTE pMin[], 
      BYTE pMax[], 
      BYTE pSteppingDelta[], 
      BYTE pDefault[]);
};

#define STATIC_PROPSETID_VIDCAP_EXTENSION_UNIT \
   0xXXXXXXXX,0xXXXX,0xXXXX,0xXX,0xXX,0xXX,0xXX,0xXX,0xXX,0xXX,0xXX
DEFINE_GUIDSTRUCT("XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX", \ 
   PROPSETID_VIDCAP_EXTENSION_UNIT);
#define PROPSETID_VIDCAP_EXTENSION_UNIT \      
   DEFINE_GUIDNAMED(PROPSETID_VIDCAP_EXTENSION_UNIT)
```

2 つの仮想メソッドを実装**IKsNodeControl**で**CNodeControl**します。 これらのメソッドがのインスタンスで、継承、 **CExtension**クラス。

次のコードを任意にという名前のソース ファイルは*Xuproxy.cpp*:

```cpp
STDMETHODIMP
CNodeControl::put_NodeId(
   DWORD dwNodeId)
{
   m_dwNodeId = dwNodeId;
 return S_OK;
}

STDMETHODIMP
CNodeControl::put_KsControl(
   PVOID pKsControl)
{
   HRESULT hr = S_OK;
   IKsControl *pIKsControl;

 if (!pKsControl) return E_POINTER;
    pIKsControl = (IKsControl *) pKsControl;

    if (m_pKsControl) m_pKsControl.Release();
 hr = pIKsControl->QueryInterface(__uuidof(IKsControl),
       (void **) &m_pKsControl);        

    return hr;
}
```

実装を含んでも**CExtension**の同じメソッド*Xuproxy.cpp*ファイル。

```cpp
CExtension::CExtension()
{
    m_pKsControl = NULL;
}

STDMETHODIMP 
CExtension::FinalConstruct()
{
    if (m_pOuterUnknown == NULL ) return E_FAIL;
    return S_OK;
}

STDMETHODIMP 
CExtension::get_InfoSize(
    ULONG *pulSize)
{
    HRESULT hr = S_OK;
    ULONG ulBytesReturned;
    KSP_NODE ExtensionProp;

    if (!pulSize) return E_POINTER;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET | 
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

 hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
        sizeof(ExtensionProp),
        NULL,
        0,
        &ulBytesReturned);

    if (hr == HRESULT_FROM_WIN32(ERROR_MORE_DATA)) 
    {
        *pulSize = ulBytesReturned;
        hr = S_OK;
    }
 
 return hr;
}


STDMETHODIMP 
CExtension::get_Info(
    ULONG ulSize,
    BYTE pInfo[])
{
    HRESULT hr = S_OK;
    KSP_NODE ExtensionProp;
    ULONG ulBytesReturned;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET | 
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        (PVOID) pInfo,
        ulSize,
        &ulBytesReturned);

 return hr;
}


STDMETHODIMP 
CExtension::get_PropertySize(
    ULONG PropertyId, 
    ULONG *pulSize)
{
    HRESULT hr = S_OK;
    ULONG ulBytesReturned;
    KSP_NODE ExtensionProp;

 if (!pulSize) return E_POINTER;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = PropertyId;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET | 
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        NULL,
        0,
        &ulBytesReturned);

 if (hr == HRESULT_FROM_WIN32(ERROR_MORE_DATA)) 
    {
        *pulSize = ulBytesReturned;
        hr = S_OK;
    }
 
 return hr;
}

STDMETHODIMP 
CExtension::get_Property(
    ULONG PropertyId, 
    ULONG ulSize, 
    BYTE pValue[])
{
    HRESULT hr = S_OK;
    KSP_NODE ExtensionProp;
    ULONG ulBytesReturned;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = PropertyId;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET | 
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        (PVOID) pValue,
        ulSize,
        &ulBytesReturned);

    return hr;
}

STDMETHODIMP 
CExtension::put_Property(
    ULONG PropertyId, 
    ULONG ulSize, 
    BYTE pValue[])
{
    HRESULT hr = S_OK;
    KSP_NODE ExtensionProp;
    ULONG ulBytesReturned;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = PropertyId;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_SET | 
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        (PVOID) pValue,
        ulSize,
        &ulBytesReturned);

    return hr;
}

STDMETHODIMP
CExtension::get_PropertyRange( 
    ULONG PropertyId,
    ULONG ulSize,
    BYTE pMin[  ],
    BYTE pMax[  ],
    BYTE pSteppingDelta[  ],
    BYTE pDefault[  ])
{
    // IHV may add code here, current stub just returns S_OK
    HRESULT hr = S_OK;
    return hr;
}

CExtension::CExtension()
{
    m_pKsControl = NULL;
}
 
STDMETHODIMP 
CExtension::FinalConstruct()
{
    if (m_pOuterUnknown == NULL) return E_FAIL;
    return S_OK;
}
```

 

 




