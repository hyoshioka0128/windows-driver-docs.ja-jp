---
title: CCD サンプル コード
description: CCD サンプル コード
ms.assetid: 8ca2c7c4-8e6f-4e4f-9234-eb3e5dc164cc
keywords:
- 接続するには、WDK Windows 7 の表示、CCD Api、コード例が表示されます。
- 接続するには、WDK の Windows Server 2008 R2 の表示、CCD Api、コード例が表示されます。
- 構成するには、WDK の Windows 7 の表示、CCD Api、コード例が表示されます。
- 構成するには、WDK の Windows Server 2008 R2 の表示、CCD Api、コード例が表示されます。
- CCD Api WDK Windows 7 の表示、コード例
- CCD Api WDK Windows Server 2008 R2 の表示、コード例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b9fe2c962e79f998d55b14bde271fd68daa4d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553610"
---
# <a name="ccd-example-code"></a>CCD サンプル コード


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次の疑似コードは、CCD Api を使用して、複製のビューを設定する方法を示しています。

```cpp
SetCloneView
{
    // Determine the size of the path array that is required to hold all valid paths.
  Call GetDisplayConfigBufferSizes(QDC_ALL_PATHS) to retrieve the sizes of
  the DISPLAYCONFIG_PATH_INFO and DISPLAYCONFIG_MODE_INFO buffers that are required.

    // Allocate memory for path and mode information arrays.
    Allocate PathArraySize*sizeof(DISPLAYCONFIG_PATH_INFO) for the path information array
    Allocate ModeArraySize*sizeof(DISPLAYCONFIG_MODE_INFO) for the mode information array.

    // Request all of the path information.
  Call QueryDisplayConfig(QDC_ALL_PATHS) to obtain the path and mode information for all posible paths.

    // Find and store the primary path.
    Search the DISPLAYCONFIG_PATH_INFO array for an active path that is located at desktop position (0, 0).

    // Determine the user friendly name of the current primary.
  Call DisplayConfigGetDeviceInfo() by using the
    DISPLAYCONFIG_DEVICE_INFO_GET_TARGET_NAME type and the adapter ID and target ID
  from the DISPLAYCONFIG_PATH_TARGET_INFO of the primary path.

    // DisplayConfigGetDeviceInfo can determine the user friendly names 
    // for all of the paths that might be part of the clone. 
    // Allow the user to pick which monitor the clone is enabled on.
    // Only provide the user options of the paths from the current primary 
    // to targets with monitors that are connected or that are forceable.  
    Store a pointer to the DISPLAYCONFIG_PATH_INFO that the user picked.

    // Mark the new path as active.
    Set the DISPLAYCONFIG_PATH_ACTIVE in the DISPLAYCONFIG_PATH_INFO.flags of the new clone path.
  NewClonePath->flags |= DISPLAYCONFIG_PATH_ACTIVE;
  NewClonePath->sourceInfo.modeInfoIdx = DISPLAYCONFIG_PATH_MODE_IDX_INVALID;
  NewClonePath->targetInfo.modeInfoIdx = DISPLAYCONFIG_PATH_MODE_IDX_INVALID;

    // Set the new topology.
  Call SetDisplayConfig
    (SDC_APPLY | SDC_SAVE_TO_DATABASE | SDC_ALLOW_CHANGES | SDC_USE_SUPPLIED_DISPLAY_CONFIG)
  to change to the clone topology.
}
```

 

 





