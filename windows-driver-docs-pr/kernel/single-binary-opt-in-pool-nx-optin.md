---
title: 単一バイナリ オプトイン POOL_NX_OPTIN
description: Windows 8 と Windows の以前のバージョンの両方を実行している 1 つのドライバー バイナリをビルドするには、POOL_NX_OPTIN オプトイン メカニズムを使用します。
ms.assetid: BE9D3C85-0212-4206-A59B-4D53FB842C39
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 102f973fe206540f3c15b9a6d3bff78d238bd031
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383027"
---
# <a name="single-binary-opt-in-poolnxoptin"></a>単一バイナリ オプトイン: プール\_NX\_OPTIN


Windows 8 と Windows の以前のバージョンの両方を実行している 1 つのドライバー バイナリをビルドするには、プールを使用して\_NX\_OPTIN オプトイン メカニズム。 これは、複数の Windows バージョンをサポートするためにバイナリの 1 つのドライバーを提供するサード パーティ製ハードウェア ベンダーの移植の支援です。

をこのオプトイン メカニズムを使用するには、次の操作を行います。

-   プールを定義\_NX\_OPTIN = 1 すべてのソース ファイルにオプトインします。 これを行うには、ドライバー プロジェクトの適切なプロパティ ページで次のプリプロセッサの定義を含めます。

    `C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1`

-   [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize) (または同等) ルーチンでは、次の関数呼び出しが含まれます。

    `ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

    この呼び出しは、ドライバーは、割り当てを使用する前に行う必要があります、 **NonPagedPool**プール型またはいずれかの呼び出しにより、 [ **ExInitializeNPagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)ルーチンです。 **ExInitializeDriverRuntime** force インライン関数は、Windows 8 または Windows の以降のバージョンを呼び出すことができます。

ほとんどのドライバーでは、これら 2 つのタスクはバイナリの 1 つのドライバーのオプトイン メカニズムを有効にするための十分です。

## <a name="implementation-details"></a>実装の詳細


プール\_NX\_OPTIN に置き換えることで、動作**NonPagedPool** 、グローバルな[**プール\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pool_type)変数`ExDefaultNonPagedPoolType`、いずれかに初期化される**NonPagedPoolNx** (Windows 8 以降のバージョンの Windows 用) または**NonPagedPoolExecute** (の Windows の以前のバージョン)。 NX のプールの強化された保護と、Windows 8 と NX プールがサポートされていない、Windows の以前のバージョンの両方を実行する、カーネル モード ドライバーをこのオプトイン メカニズムにできます。 インスタンスに変換するマクロ、 **NonPagedPool**定数名に**NonPagedPoolNx**のインスタンスの変換も行います**NonPagedPoolCacheAligned** に**NonPagedPoolNxCacheAligned**します。

## <a name="support-for-static-libraries-lib-projects"></a>スタティック ライブラリ (.lib プロジェクト) のサポート


プールを使用する\_NX\_OPTIN オプトイン メカニズム .lib プロジェクトは通常、.lib にリンクしているプロジェクトは、プールを使用する必要がありますも\_NX\_OPTIN します。 少なくとも、プロジェクトを実装する、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンは、次の関数呼び出しを含める必要があります。

`ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

 

 




