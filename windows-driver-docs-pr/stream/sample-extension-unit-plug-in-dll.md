---
title: サンプル拡張ユニット プラグイン DLL
description: サンプル拡張機能単体プラグイン DLL
ms.assetid: bd9ea70d-7bd0-494d-8d67-7a36a41d005b
keywords:
- プラグイン DLL WDK USB ビデオクラス
- 拡張機能ユニット WDK USB ビデオクラス、サンプル、プラグイン DLL
- サンプルコード WDK USB ビデオクラス、拡張機能単体プラグイン DLL
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0429260e9268cbea78517c667b04404f6c2ba53a
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111239"
---
# <a name="sample-extension-unit-plug-in-dll"></a>サンプル拡張機能単体プラグイン DLL

このトピックには、KS プロパティセットの上に COM API を公開する拡張機能単体プラグイン DLL のサンプルコードが含まれています。

このサンプルでは、 **CNodeControl**から派生する**cextension**というクラスを定義します。 **CNodeControl**クラスの実装は、後でも提供されます。 **CNodeControl**は、 *Vidcap*で定義されている、Microsoft が提供する**IKsNodeControl**インターフェイスから派生しています。

*Vidcap.ax*は**IKsNodeControl**を使用して拡張ノード ID のプラグインを通知し、 **iksk コントロール**のインスタンスを提供します。 具体的には、プラグインは**Cextension::p ut \_ NodeId**および**cextension::p ut \_ kscontrol**の呼び出しを通じてこの情報を受け取ります。 これらのメソッドの実装可能な実装については、このトピックの後の方で、親クラス**CNodeControl**を参照してください。

*Vidcap*は、2004年2月 2005 [directx](https://docs.microsoft.com/previous-versions/dn629515(v=msdn.10))sdk を通じて、夏 directx sdk に表示されます。 これらのパッケージをインストールする場合は、 *Vidcap*を取得するために、エクストラをインストールする必要があります。

Windows Vista 以降のリリースでは、 *Vidcap*が Microsoft Windows SDK の一部として含まれています。

クラスヘッダーファイルには、次のコードを追加します *。*

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

**CNodeControl**の**IKsNodeControl**から2つの仮想メソッドを実装します。 これらのメソッドは、 **Cextension**クラスのインスタンスによって継承されます。

次のコードは、任意の名前で*Xuproxy .cpp*という名前のソースファイルにあります。

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

また、同じ*Xuproxy*ファイルに**cextension**のメソッドの実装を含めます。

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
