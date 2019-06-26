---
title: グラフィックス メモリの数の取得
description: グラフィックス メモリの数の取得
ms.assetid: ec704093-ad9a-4717-8e9e-537a2848b1c7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef4b5c3755b6350888e2d2c93d4e0fe64482b8a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365667"
---
# <a name="retrieving-graphics-memory-numbers"></a>グラフィックス メモリの数の取得


グラフィックスのアプリケーションを作成するソフトウェア開発者は、以降 Windows Vista では Microsoft DirectX のバージョン 10 Api を使用して実行するコンピューターでのグラフィックス メモリの数値の正確なセットを取得できます[Windows Display Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)ドライバーを表示します。 次の手順では、グラフィックス メモリの番号を取得する方法を示します。

1.  新しいグラフィックス メモリ レポートは、ディスプレイ ドライバーを Windows 表示 Driver Model (WDDM) を実行しているコンピューターでのみ利用可能であるため、アプリケーションはまずドライバー モデルを確認する次の関数を呼び出す必要があります。
    ```cpp
    HasWDDMDriver()
    {
        LPDIRECT3DCREATE9EX pD3D9Create9Ex = NULL;
        HMODULE             hD3D9          = NULL;

        hD3D9 = LoadLibrary( L"d3d9.dll" );

        if ( NULL == hD3D9 ) {
            return false;
        }

        //
        //  Try to create a IDirect3D9Ex interface (also known as a DX9L 
        //  interface).
        //  This interface can only be created if the driver is written 
        //  according to the Windows Display Driver Model (WDDM).
        //
        pD3D9Create9Ex = (LPDIRECT3DCREATE9EX) GetProcAddress (
            hD3D9, "Direct3DCreate9Ex" );

        return pD3D9Create9Ex != NULL;
    }
    ```

2.  アプリケーションは新しい DirectX 10 のバージョンを使用した後、ディスプレイ ドライバー モデルが、WDDM があると判断した場合、アプリケーション、グラフィックス メモリの数値を取得する Api。 アプリケーションは、次のグラフィックス メモリの数値を取得[ **DXGI\_アダプター\_DESC** ](https://docs.microsoft.com/windows/desktop/api/dxgi/ns-dxgi-dxgi_adapter_desc) Dxgi.h に存在し、DirectX に含まれているデータ構造ソフトウェア開発キット (SDK)。
    ```cpp
    typedef struct DXGI_ADAPTER_DESC {
        WCHAR Description[ 128 ];
        UINT VendorId;
        UINT DeviceId;
        UINT SubSysId;
        UINT Revision;
        SIZE_T DedicatedVideoMemory;
        SIZE_T DedicatedSystemMemory;
        SIZE_T SharedSystemMemory;
        LUID AdapterLuid;
        } DXGI_ADAPTER_DESC;
    ```

Windows Vista 以降を実行しているソフトウェアは、Windows Vista およびそれ以降のデスクトップと DirectX ゲーム グラフィックスの広範な使用しているため使用可能なグラフィックス メモリの量を正確に判断できる必要があります。 WDDM はグラフィックス メモリ自体での仮想化を管理し、またグラフィックス メモリのさまざまな側面の正確なレポートを作成します。 アプリケーション開発者やソフトウェア ベンダーを活用して DirectX 10 のバージョンのドライバーを Windows Vista のコンピューター上のグラフィックス メモリ値の正確なセットを取得するための Api が表示されます。

