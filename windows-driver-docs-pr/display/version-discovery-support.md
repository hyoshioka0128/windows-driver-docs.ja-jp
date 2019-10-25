---
title: バージョン検出のサポート
description: バージョン検出のサポート
ms.assetid: 9e37eaad-02b2-43a9-bd1a-4c5b2b02d1b6
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 display、バージョン検出サポート
- バージョン検出サポート WDK Windows 7 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e361febcc217d14d63aa2b8cc70a6d0d50f48ca0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825298"
---
# <a name="version-discovery-support"></a>バージョン検出のサポート


このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

Windows Vista 以降のバージョンおよび Windows Server 2008 以降のバージョンで実行されるユーザーモード表示ドライバーでは、ドライバーが明示的に指定していないバージョンの DDI に対して、アダプターの作成に失敗する (つまり、ドライバーの[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数への呼び出しが失敗する) 必要があります。ご.

Windows 7 は、ドライバーが明示的にサポートしている DDI バージョンとハードウェア機能を Direct3D アプリケーションが検出するための手段を提供します。 これにより、バージョンの検証が向上します。 Windows 7 では、バージョン管理を改善し、API とドライバーの初期化を最適化するための新しいアダプター固有の機能が導入されています。 Direct3d ランタイムがドライバーの新しいアダプター固有の関数を呼び出すことができるように、 [**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数を direct3d バージョン10.1 ドライバーに実装してエクスポートする必要があります。 代わりに、 [**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)を Direct3D バージョン10.1 ドライバーに実装する場合、ドライバーは**OpenAdapter10**の呼び出しを渡したり失敗したりすることによって、DDI バージョンをサポートしているかどうかのみを示すことができます。

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)は、 [**D3D10DDIARG\_openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)構造体の**padapterfuncs\_2**メンバーで、ドライバーのアダプター固有の関数のテーブルを返します。 **Padapterfuncs 2**は、 [**D3D10\_2DDI\_adapterの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)構造体を指します。 Direct3D ランタイムは、ドライバーのアダプター固有の[**Getsupportedversions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)関数を呼び出して、ドライバーがサポートする DDI バージョンとハードウェア機能を照会します。 **Getsupportedversions**は、64ビット値の配列に含まれる DDI バージョンとハードウェア機能を返します。 **Getsupportedversions**の実装のコード例を次に示します。

```cpp
// Array of 64-bit values that are defined in D3d10umddi.h
const UINT64 c_aSupportedVersions[] = {
    D3D10_0_7_DDI_SUPPORTED, // 10.0 on Windows 7
    D3D10_0_DDI_SUPPORTED, // 10.0 on Windows Vista
 D3D10_1_x_DDI_SUPPORTED, // 10.1 with all extended 
                           // format support (but not
                           // Windows 7 scheduling)
};

HRESULT APIENTRY GetSupportedVersions(
                 D3D10DDI_HADAPTER hAdapter, 
                 __inout UINT32* puEntries,
 __out_ecount_opt( *puEntries ) 
 UINT64* pSupportedDDIInterfaceVersions)
)
{
    const UINT32 uEntries = ARRAYSIZE( c_aSupportedVersions );
    if (pSupportedDDIInterfaceVersions &&
        *puEntries < uEntries)
    {
        return HRESULT_FROM_WIN32( ERROR_INSUFFICIENT_BUFFER );
    }

    // Determine concise hardware support from kernel, cache with hAdapter.
    // pfnQueryAdapterInfoCb( hAdapter, ... )

    *puEntries = uEntries;
    if (pSupportedDDIInterfaceVersions)
    {
        UINT64* pCurEntry = pSupportedDDIInterfaceVersions;
        memcpy( pCurEntry, c_aSupportedVersions, sizeof( c_aSupportedVersions ) );
        pCurEntry += ARRAYSIZE( c_aSupportedVersions );
        assert( pCurEntry - pSupportedDDIInterfaceVersions == uEntries );
    }
    return S_OK;
}
```

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数の呼び出しで[**D3D10DDIARG\_Openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)の**インターフェイス**および**バージョン**メンバーに渡される値を検証するために、Direct3D バージョン10.1 ドライバーは必要ありません。ただし、これらの値には、ドライバーの初期化に使用する DDI バージョン情報が含まれています。 ドライバーは、 [**Getsupportedversions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)関数の呼び出しによって、DDI バージョンとハードウェア機能を返すことができます。

Direct3D ランタイムは、 [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)の**インターフェイス**および**バージョン**のメンバーに、ランタイムによって指定された値とは異なるドライバーの[**CREATEDEVICE (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しで値を渡すことができます。[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)に渡されました。ランタイムは、D3D10DDIARG\_CREATEDEVICE の**インターフェイス**と**バージョン**のメンバーに、ドライバーの[**getsupportedversions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)によって返された DDI バージョンとハードウェア機能の情報に基づいて値を渡します。を実行します。 ドライバーは、D3D10DDIARG\_CREATEDEVICE の**インターフェイス**および**バージョン**メンバーに渡された値を検証する必要はありません。これは、ドライバーが getsupportedversions によってこれらの値のサポートを既に示しているためです。関数。

ドライバーを Direct3D バージョン10.0 から Direct3D バージョン10.1 に移植する場合は、OpenAdapter10 ではなく[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)に渡される**インターフェイス**と**バージョン**のメンバーのみを監視するようにドライバーを変換する必要があります。 [ **\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) [**CalcPrivateDeviceSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)と**CreateDevice (D3D10)** 関数の両方の実装を移植されたドライバーで分析し、の**インターフェイス**および**バージョン**メンバーの値についての*前提条件がないことを確認する必要があります。CreateDevice (D3D10)* は、 **OpenAdapter10\_2**の**インターフェイス**と**バージョン**メンバーの値に一致します。

**注**  [**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)には、 [**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) ( *D3d10umddi*ヘッダーで定義されている PFND3D10DDI\_openadapter) と同じ関数シグネチャがあります。 同じユーザーモードの表示ドライバー DLL で、両方の関数を実装できます。

 

 

 





