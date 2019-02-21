---
title: 単一バイナリ オプトイン POOL_NX_OPTIN
description: Windows 8 と Windows の以前のバージョンの両方を実行している 1 つのドライバー バイナリをビルドするには、POOL_NX_OPTIN オプトイン メカニズムを使用します。
ms.assetid: BE9D3C85-0212-4206-A59B-4D53FB842C39
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 00366b375a953a585acadf52f8cca8331f6ad943
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529708"
---
# <a name="single-binary-opt-in-poolnxoptin"></a>単一バイナリにオプトインします。プール\_NX\_OPTIN


Windows 8 と Windows の以前のバージョンの両方を実行している 1 つのドライバー バイナリをビルドするには、プールを使用して\_NX\_OPTIN オプトイン メカニズム。 これは、複数の Windows バージョンをサポートするためにバイナリの 1 つのドライバーを提供するサード パーティ製ハードウェア ベンダーの移植の支援です。

をこのオプトイン メカニズムを使用するには、次の操作を行います。

-   プールを定義\_NX\_OPTIN = 1 すべてのソース ファイルにオプトインします。 これを行うには、ドライバー プロジェクトの適切なプロパティ ページで次のプリプロセッサの定義を含めます。

    `C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1`

-   [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) (または同等) ルーチンでは、次の関数呼び出しが含まれます。

    `ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

    この呼び出しは、ドライバーは、割り当てを使用する前に行う必要があります、 **NonPagedPool**プール型またはいずれかの呼び出しにより、 [ **ExInitializeNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545301)ルーチンです。 **ExInitializeDriverRuntime** force インライン関数は、Windows 8 または Windows の以降のバージョンを呼び出すことができます。

ほとんどのドライバーでは、これら 2 つのタスクはバイナリの 1 つのドライバーのオプトイン メカニズムを有効にするための十分です。

## <a name="implementation-details"></a>実装の詳細


プール\_NX\_OPTIN に置き換えることで、動作**NonPagedPool** 、グローバルな[**プール\_型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)変数`ExDefaultNonPagedPoolType`、いずれかに初期化される**NonPagedPoolNx** (Windows 8 以降のバージョンの Windows 用) または**NonPagedPoolExecute** (の Windows の以前のバージョン)。 NX のプールの強化された保護と、Windows 8 と NX プールがサポートされていない、Windows の以前のバージョンの両方を実行する、カーネル モード ドライバーをこのオプトイン メカニズムにできます。 インスタンスに変換するマクロ、 **NonPagedPool**定数名に**NonPagedPoolNx**のインスタンスの変換も行います**NonPagedPoolCacheAligned** に**NonPagedPoolNxCacheAligned**します。

## <a name="support-for-static-libraries-lib-projects"></a>スタティック ライブラリ (.lib プロジェクト) のサポート


プールを使用する\_NX\_OPTIN オプトイン メカニズム .lib プロジェクトは通常、.lib にリンクしているプロジェクトは、プールを使用する必要がありますも\_NX\_OPTIN します。 少なくとも、プロジェクトを実装する、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは、次の関数呼び出しを含める必要があります。

`ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

 

 




