---
title: OpenGL 拡張機能のサポート
description: OpenGL 拡張機能のサポート
ms.assetid: 5f8b7d96-7941-44ce-bd32-546ec0f32883
keywords:
- OpenGL の機能強化 WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23776c9c9de2d5030bb700290786377ada5c05f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829387"
---
# <a name="supporting-opengl-enhancements"></a>OpenGL 拡張機能のサポート


## <a name="span-idwindows_7_enhancementsspanspan-idwindows_7_enhancementsspanspan-idwindows_7_enhancementsspanwindows7-enhancements"></a><span id="Windows_7_Enhancements"></span><span id="windows_7_enhancements"></span><span id="WINDOWS_7_ENHANCEMENTS"></span>Windows 7 の機能強化


このセクションは、Windows 7 以降、Windows Server 2008 R2 以降にのみ適用されます。

OpenGL のインストール可能なクライアントドライバー (ICD) を実装して、Windows 7 に付属する次の OpenGL 拡張機能を使用することができます。

### <a name="span-idenhancing_synchronizationspanspan-idenhancing_synchronizationspanenhancing-synchronization"></a><span id="enhancing_synchronization"></span><span id="ENHANCING_SYNCHRONIZATION"></span>同期の強化

次の第2世代の OpenGL 同期関数を使用すると、OpenGL ICD の同期機能を強化できます。

-   [**D3DKMTCreateSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatesynchronizationobject2)

-   [**D3DKMTOpenSynchronizationObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopensynchronizationobject)

-   [**D3DKMTWaitForSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforsynchronizationobject2)

-   [**D3DKMTSignalSynchronizationObject2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtsignalsynchronizationobject2)

### <a name="span-idcontrolling_resource_access_with_mutexesspanspan-idcontrolling_resource_access_with_mutexesspancontrolling-resource-access-with-mutexes"></a><span id="controlling_resource_access_with_mutexes"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES"></span>ミューテックスを使用したリソースアクセスの制御

リソースへのアクセスを制御するには、次の OpenGL ミューテックス関数を使用できます。

-   [**D3DKMTCreateKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex)

-   [**D3DKMTOpenKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenkeyedmutex)

-   [**D3DKMTDestroyKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtdestroykeyedmutex)

-   [**D3DKMTAcquireKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex)

-   [**D3DKMTReleaseKeyedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtreleasekeyedmutex)

### <a name="span-idmanaging_access_to_shared_resourcesspanspan-idmanaging_access_to_shared_resourcesspanmanaging-access-to-shared-resources"></a><span id="managing_access_to_shared_resources"></span><span id="MANAGING_ACCESS_TO_SHARED_RESOURCES"></span>共有リソースへのアクセスの管理

次の OpenGL 関数を使用すると、共有リソースへのアクセスを管理できます。

-   [**D3DKMTConfigureSharedResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtconfiguresharedresource)

-   [**D3DKMTCheckSharedResourceAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtchecksharedresourceaccess)

### <a name="span-idmonitoring_present_historyspanspan-idmonitoring_present_historyspanmonitoring-present-history"></a><span id="monitoring_present_history"></span><span id="MONITORING_PRESENT_HISTORY"></span>監視 (現在の履歴を)

次の OpenGL 関数を使用すると、現在の操作の履歴を監視できます。

-   [**D3DKMTPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtpresent) with [**D3DKMT\_PRESENTHISTORYTOKEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presenthistorytoken)構造体に**PRESENTHISTORYTOKEN** [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_present)メンバーが設定されています。

-   [**D3DKMTGetPresentHistory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetpresenthistory)

### <a name="span-idmiscellaneous_enhancementsspanspan-idmiscellaneous_enhancementsspanmiscellaneous-enhancements"></a><span id="miscellaneous_enhancements"></span><span id="MISCELLANEOUS_ENHANCEMENTS"></span>その他の機能強化

次の OpenGL その他の拡張機能を使用できます。

-   [**D3DKMTCheckVidPnExclusiveOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcheckvidpnexclusiveownership)

-   [**D3DKMTGetOverlayState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetoverlaystate)

-   [**D3DKMT\_setdisplaymode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode)構造体の**flags**メンバーに設定された[**D3DKMT\_setdisplaymode\_flags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_setdisplaymode_flags)構造を持つ[**D3DKMTSetDisplayMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtsetdisplaymode)

-   [**D3DKMT\_POLLDISPLAYCHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)構造[**体に新しいフラグが設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtpolldisplaychildren)された状態

## <a name="span-idwindows_8_enhancementsspanspan-idwindows_8_enhancementsspanwindows8-enhancements"></a><span id="windows_8_enhancements"></span><span id="WINDOWS_8_ENHANCEMENTS"></span>Windows 8 の機能強化


このセクションは、Windows 8 以降、および Windows Server 2012 以降にのみ適用されます。

OpenGL のインストール可能なクライアントドライバー (ICD) を実装すると、Windows 8 に付属している次の OpenGL 拡張機能を使用できます。

### <a name="span-idcontrolling_resource_access_with_mutexes_spanspan-idcontrolling_resource_access_with_mutexes_spanspan-idcontrolling_resource_access_with_mutexes_spancontrolling-resource-access-with-mutexes"></a><span id="Controlling_Resource_Access_with_Mutexes_"></span><span id="controlling_resource_access_with_mutexes_"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES_"></span>ミューテックスを使用したリソースアクセスの制御

これらの OpenGL ミューテックス関数と関連する構造体を使用して、キー付きミューテックスに関連付けるプライベートデータを指定しながら、リソースへのアクセスを制御することができます。

-   [**D3DKMTAcquireKeyedMutex2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtacquirekeyedmutex2)
-   [**D3DKMTCreateKeyedMutex2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtcreatekeyedmutex2)
-   [**D3DKMT\_ACQUIREKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_acquirekeyedmutex2)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)

### <a name="span-idopengl_helper_functionsspanspan-idopengl_helper_functionsspanspan-idopengl_helper_functionsspanopengl-helper-functions"></a><span id="OpenGL_Helper_Functions"></span><span id="opengl_helper_functions"></span><span id="OPENGL_HELPER_FUNCTIONS"></span>OpenGL ヘルパー関数

これらの関数とそれに関連付けられている構造体を使用して、オブジェクトとそのハンドルにアクセスできます。

-   [**D3DKMTGetSharedResourceAdapterLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtgetsharedresourceadapterluid)
-   [**D3DKMTOpenAdapterFromLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenadapterfromluid)
-   [**D3DKMTOpenNtHandleFromName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopennthandlefromname)
-   [**D3DKMTOpenResourceFromNtHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopenresourcefromnthandle)
-   [**D3DKMTOpenSyncObjectFromNtHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtopensyncobjectfromnthandle)
-   [**D3DKMT\_GETSHAREDRESOURCEADAPTERLUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_getsharedresourceadapterluid)
-   [**D3DKMT\_OPENADAPTERFROMLUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_openadapterfromluid)
-   [**D3DKMT\_OPENNTHANDLEFROMNAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_opennthandlefromname)
-   [**D3DKMT\_OPENRESOURCEFROMNTHANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_openresourcefromnthandle)
-   [**D3DKMT\_OPENSYNCOBJECTFROMNTHANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_opensyncobjectfromnthandle)

 

 





