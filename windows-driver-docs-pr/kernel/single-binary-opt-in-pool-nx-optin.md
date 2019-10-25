---
title: シングルバイナリオプトイン POOL_NX_OPTIN
description: Windows 8 と以前のバージョンの Windows の両方で実行される単一のドライバーバイナリをビルドするには、POOL_NX_OPTIN オプトイン機構を使用します。
ms.assetid: BE9D3C85-0212-4206-A59B-4D53FB842C39
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1a8fd9b15bda28ae3e78d9b5aea08c72d349a724
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838420"
---
# <a name="single-binary-opt-in-pool_nx_optin"></a>シングルバイナリオプトイン: プール\_NX\_OPTIN


Windows 8 と以前のバージョンの Windows の両方で実行される単一のドライバーバイナリを構築するには、プール\_NX\_OPTIN オプトイン機構を使用します。 これは、複数の Windows バージョンをサポートするために1つのドライバーバイナリを提供するサードパーティ製ハードウェアベンダー向けの移植支援です。

このオプトインメカニズムを使用するには、次の手順を実行します。

-   オプトインするすべてのソースファイルに対して、プール\_NX\_OPTIN = 1 を定義します。 これを行うには、ドライバープロジェクトの適切なプロパティページに次のプリプロセッサ定義を追加します。

    `C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1`

-   [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) (または同等の) ルーチンで、次の関数呼び出しを含めます。

    `ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

    この呼び出しは、ドライバーが**NonPagedPool**プール型を使用する割り当てを作成するか、 [**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)ルーチンを呼び出す前に行う必要があります。 **Exinitializedriverruntime**は強制インライン関数であり、windows 8 以降のバージョンの windows で呼び出すことができます。

ほとんどのドライバーでは、この2つのタスクで1つのドライバーバイナリに対してオプトイン機構を有効にするだけで十分です。

## <a name="implementation-details"></a>実装の詳細


プール\_NX\_OPTIN は、 **NonPagedPool**をグローバル[**プール\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)`ExDefaultNonPagedPoolType`変数に置き換えることによって機能します。これは、 **NonPagedPoolNx** (Windows 8 以降のバージョンの windows の場合) またはに**初期化されます。NonPagedPoolExecute** (以前のバージョンの Windows の場合)。 このオプトインメカニズムを使用すると、カーネルモードドライバーが Windows 8 上で実行され、NX プールの保護が強化され、以前のバージョンの Windows では NX プールがサポートされません。 **NonPagedPool**定数名のインスタンスを**NonPagedPoolNx**に変換するマクロでは、 **NonPagedPoolCacheAligned**のインスタンスも**NonPagedPoolNxCacheAligned**に変換されます。

## <a name="support-for-static-libraries-lib-projects"></a>スタティックライブラリ (.lib プロジェクト) のサポート


プール\_NX\_OPTIN プロジェクトに対して使用できますが、.lib にリンクするプロジェクトは通常、プール\_NX\_OPTIN も使用する必要があります。 少なくとも、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを実装するプロジェクトには、次の関数呼び出しが含まれている必要があります。

`ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

 

 




