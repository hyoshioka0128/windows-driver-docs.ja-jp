---
title: バージョン検出のサポート
description: バージョン検出のサポート
ms.assetid: 9e37eaad-02b2-43a9-bd1a-4c5b2b02d1b6
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、探索のバージョンのサポート
- バージョンの検出サポート Windows 7 の WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2340f21f5067cad774bf56a1e378227bb85a1e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374351"
---
# <a name="version-discovery-support"></a>バージョン検出のサポート


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

Windows Vista およびそれ以降のバージョンと Windows Server 2008 以降のバージョンで実行されるユーザー モードのディスプレイ ドライバーがアダプターの作成に失敗する必要があります (つまり、ドライバーへの呼び出しは失敗[ **OpenAdapter10** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)ドライバーが明示的にサポートされていない DDI バージョンに対しては機能)。

Windows 7 では、Direct3D アプリケーション DDI バージョンとドライバーが明示的にサポートするハードウェアの機能を検出するための手段を提供します。 これにより、バージョンの検証が向上します。 Windows 7 には、バージョン管理を向上させるために、API とドライバーの初期化を最適化する機会を提供する新しいアダプターに固有の機能が導入されています。 実装およびエクスポートする必要があります、 [ **OpenAdapter10\_2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) Direct3D ランタイムは、ドライバーの新しいアダプター固有の関数を呼び出すことができますので、Direct3D バージョン 10.1 ドライバー関数。 代わりに実装する場合[ **OpenAdapter10** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) 、Direct3D のバージョン 10.1 ドライバー、ドライバーを示すことしか合格または不合格の呼び出しによって DDI バージョンをサポートするかどうか**OpenAdapter10**します。

[**OpenAdapter10\_2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)でドライバーのアダプター固有の関数のテーブルを返します、 **pAdapterFuncs\_2**のメンバー、 [ **D3D10DDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)構造体。 **pAdapterFuncs\_2**を指す、 [ **D3D10\_2DDI\_ADAPTERFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)構造体。 Direct3D ランタイムが呼び出す、ドライバーのアダプター固有[ **GetSupportedVersions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions) DDI バージョンと、ドライバーがサポートするハードウェアの機能を照会する関数。 **GetSupportedVersions** DDI バージョンとハードウェアの機能を 64 ビット値の配列で返します。 次のコード例は、 **GetSupportedVersions**実装。

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

Direct3D のバージョン 10.1 ドライバーに渡される値を確認する必要はありません、**インターフェイス**と**バージョン**のメンバー [ **D3D10DDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)への呼び出しでその[ **OpenAdapter10\_2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)これらの値にする DDI バージョン情報が含まれているにもかかわらず関数ドライバーを初期化します。 ドライバーは DDI バージョンとハードウェアの機能を呼び出すことによって、返すことができます、 [ **GetSupportedVersions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)関数。

Direct3D の実行時に値を渡すことができます、**インターフェイス**と**バージョン**のメンバー [ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)ドライバーの呼び出しで[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数に、ランタイムが渡される値とは異なる[ **OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter); ランタイムは、値を渡します、**インターフェイス**と**バージョン**D3D10DDIARG のメンバー\_DDI に基づく CREATEDEVICEバージョンとハードウェアの機能情報をドライバーの[ **GetSupportedVersions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)ランタイムに返されます。 ドライバーに渡される値を検証する必要はありません、**インターフェイス**と**バージョン**D3D10DDIARG のメンバー\_CREATEDEVICE ドライバーのサポートをすでに示されているためこれらの値をその**GetSupportedVersions**関数。

Direct3D バージョン 10.1 Direct3D バージョン 10.0 からは、ドライバーを移植する場合は、のみを監視するドライバーを変換する必要があります、**インターフェイス**と**バージョン**メンバーに渡される[**CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)の代わりに[ **OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)します。 両方を分析する必要があります[ **CalcPrivateDeviceSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)と**CreateDevice(D3D10)** 関数インポートは、前提条件がないことを確認するドライバーの実装内の値に関する、**インターフェイス**と**バージョン**メンバーを*CreateDevice(D3D10)* 内の値に一致する、 **インターフェイス**と**バージョン**メンバーを**OpenAdapter10\_2**します。

**注**  [**OpenAdapter10\_2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)と同じ関数のシグネチャを持つ[ **OpenAdapter10** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) (つまり、PFND3D10DDI\_OPENADAPTER で定義されている、 *D3d10umddi.h*ヘッダー)。 どちらの関数は、同じユーザー モード ディスプレイ ドライバー DLL に実装できます。

 

 

 





