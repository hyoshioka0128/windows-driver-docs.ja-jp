---
title: OpenGL 拡張機能のサポート
description: OpenGL 拡張機能のサポート
ms.assetid: 5f8b7d96-7941-44ce-bd32-546ec0f32883
keywords:
- OpenGL の機能強化の WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f81cd62fba565a03252a41c7e9153981a7aabdf7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350221"
---
# <a name="supporting-opengl-enhancements"></a>OpenGL 拡張機能のサポート


## <a name="span-idwindows7enhancementsspanspan-idwindows7enhancementsspanspan-idwindows7enhancementsspanwindows7-enhancements"></a><span id="Windows_7_Enhancements"></span><span id="windows_7_enhancements"></span><span id="WINDOWS_7_ENHANCEMENTS"></span>Windows 7 の機能強化


このセクションで適用のみを Windows 7 以降、Windows Server 2008 R2 以降。

OpenGL インストール可能なクライアント ドライバーに付属する次の OpenGL 拡張機能を使用して、Windows 7 (ICD) を実装できます。

### <a name="span-idenhancingsynchronizationspanspan-idenhancingsynchronizationspanenhancing-synchronization"></a><span id="enhancing_synchronization"></span><span id="ENHANCING_SYNCHRONIZATION"></span>同期の強化

次の第 2 世代の OpenGL 同期関数を使用して、OpenGL ICD の同期機能を強化できます。

-   [**D3DKMTCreateSynchronizationObject2**](https://msdn.microsoft.com/library/windows/hardware/ff546879)

-   [**D3DKMTOpenSynchronizationObject**](https://msdn.microsoft.com/library/windows/hardware/ff547069)

-   [**D3DKMTWaitForSynchronizationObject2**](https://msdn.microsoft.com/library/windows/hardware/ff547262)

-   [**D3DKMTSignalSynchronizationObject2**](https://msdn.microsoft.com/library/windows/hardware/ff547227)

### <a name="span-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspancontrolling-resource-access-with-mutexes"></a><span id="controlling_resource_access_with_mutexes"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES"></span>ミュー テックス リソースへのアクセスを制御します。

リソースへのアクセスを制御するのには、次の OpenGL ミュー テックス関数を使用できます。

-   [**D3DKMTCreateKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff546845)

-   [**D3DKMTOpenKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff547054)

-   [**D3DKMTDestroyKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff546920)

-   [**D3DKMTAcquireKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff546732)

-   [**D3DKMTReleaseKeyedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff547129)

### <a name="span-idmanagingaccesstosharedresourcesspanspan-idmanagingaccesstosharedresourcesspanmanaging-access-to-shared-resources"></a><span id="managing_access_to_shared_resources"></span><span id="MANAGING_ACCESS_TO_SHARED_RESOURCES"></span>共有リソースへのアクセスを管理します。

共有リソースへのアクセスを管理するのには、次の OpenGL 関数を使用できます。

-   [**D3DKMTConfigureSharedResource**](https://msdn.microsoft.com/library/windows/hardware/ff546798)

-   [**D3DKMTCheckSharedResourceAccess**](https://msdn.microsoft.com/library/windows/hardware/ff546769)

### <a name="span-idmonitoringpresenthistoryspanspan-idmonitoringpresenthistoryspanmonitoring-present-history"></a><span id="monitoring_present_history"></span><span id="MONITORING_PRESENT_HISTORY"></span>現在の履歴を監視

次の OpenGL 関数を使用するには、存在する操作の履歴を監視します。

-   [**D3DKMTPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff547091)で[ **D3DKMT\_PRESENTHISTORYTOKEN** ](https://msdn.microsoft.com/library/windows/hardware/ff548188)に設定される構造体、 **PresentHistoryToken**メンバー、 [ **D3DKMT\_存在**](https://msdn.microsoft.com/library/windows/hardware/ff548168)構造体

-   [**D3DKMTGetPresentHistory**](https://msdn.microsoft.com/library/windows/hardware/ff546987)

### <a name="span-idmiscellaneousenhancementsspanspan-idmiscellaneousenhancementsspanmiscellaneous-enhancements"></a><span id="miscellaneous_enhancements"></span><span id="MISCELLANEOUS_ENHANCEMENTS"></span>その他の機能強化

次の OpenGL さまざまな拡張機能を使用できます。

-   [**D3DKMTCheckVidPnExclusiveOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff546779)

-   [**D3DKMTGetOverlayState**](https://msdn.microsoft.com/library/windows/hardware/ff546977)

-   [**D3DKMTSetDisplayMode** ](https://msdn.microsoft.com/library/windows/hardware/ff547169)で、 [ **D3DKMT\_SETDISPLAYMODE\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff548286)構造に設定される、 **フラグ**のメンバー、 [ **D3DKMT\_SETDISPLAYMODE** ](https://msdn.microsoft.com/library/windows/hardware/ff548275)構造体

-   [**D3DKMTPollDisplayChildren** ](https://msdn.microsoft.com/library/windows/hardware/ff547077)設定されている新しいフラグを[ **D3DKMT\_POLLDISPLAYCHILDREN** ](https://msdn.microsoft.com/library/windows/hardware/ff548161)構造体

## <a name="span-idwindows8enhancementsspanspan-idwindows8enhancementsspanwindows8-enhancements"></a><span id="windows_8_enhancements"></span><span id="WINDOWS_8_ENHANCEMENTS"></span>Windows 8 の機能強化


このセクションでは、Windows 8 以降および Windows Server 2012 以降にのみ適用されます。

OpenGL インストール可能なクライアント ドライバーに付属する次の OpenGL 拡張機能を使用して、Windows 8 では、(ICD) を実装できます。

### <a name="span-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspanspan-idcontrollingresourceaccesswithmutexesspancontrolling-resource-access-with-mutexes"></a><span id="Controlling_Resource_Access_with_Mutexes_"></span><span id="controlling_resource_access_with_mutexes_"></span><span id="CONTROLLING_RESOURCE_ACCESS_WITH_MUTEXES_"></span>ミュー テックス リソースへのアクセスを制御します。

OpenGL ミュー テックスのこれらの関数を使用することができ、関連する秘密キー付きのミュー テックスに関連付けるデータを指定するときにリソースへのアクセスを制御する構造。

-   [**D3DKMTAcquireKeyedMutex2**](https://msdn.microsoft.com/library/windows/hardware/hh439340)
-   [**D3DKMTCreateKeyedMutex2**](https://msdn.microsoft.com/library/windows/hardware/hh439345)
-   [**D3DKMT\_ACQUIREKEYEDMUTEX2**](https://msdn.microsoft.com/library/windows/hardware/hh439466)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://msdn.microsoft.com/library/windows/hardware/hh439474)

### <a name="span-idopenglhelperfunctionsspanspan-idopenglhelperfunctionsspanspan-idopenglhelperfunctionsspanopengl-helper-functions"></a><span id="OpenGL_Helper_Functions"></span><span id="opengl_helper_functions"></span><span id="OPENGL_HELPER_FUNCTIONS"></span>OpenGL のヘルパー関数

オブジェクトとそのハンドルへのアクセスには、これらの関数とそれらに関連付けられている構造体を使用できます。

-   [**D3DKMTGetSharedResourceAdapterLuid**](https://msdn.microsoft.com/library/windows/hardware/jj128339)
-   [**D3DKMTOpenAdapterFromLuid**](https://msdn.microsoft.com/library/windows/hardware/hh780247)
-   [**D3DKMTOpenNtHandleFromName**](https://msdn.microsoft.com/library/windows/hardware/hh439409)
-   [**D3DKMTOpenResourceFromNtHandle**](https://msdn.microsoft.com/library/windows/hardware/hh439413)
-   [**D3DKMTOpenSyncObjectFromNtHandle**](https://msdn.microsoft.com/library/windows/hardware/hh780248)
-   [**D3DKMT\_GETSHAREDRESOURCEADAPTERLUID**](https://msdn.microsoft.com/library/windows/hardware/jj128344)
-   [**D3DKMT\_OPENADAPTERFROMLUID**](https://msdn.microsoft.com/library/windows/hardware/hh780267)
-   [**D3DKMT\_OPENNTHANDLEFROMNAME**](https://msdn.microsoft.com/library/windows/hardware/hh406493)
-   [**D3DKMT\_OPENRESOURCEFROMNTHANDLE**](https://msdn.microsoft.com/library/windows/hardware/hh406496)
-   [**D3DKMT\_OPENSYNCOBJECTFROMNTHANDLE**](https://msdn.microsoft.com/library/windows/hardware/hh780268)

 

 





