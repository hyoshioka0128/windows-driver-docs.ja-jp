---
title: CCD のサンプル擬似コード
description: CCD Api を使用して複製ビューを設定するための擬似コード例
ms.assetid: 8ca2c7c4-8e6f-4e4f-9234-eb3e5dc164cc
keywords:
- 接続すると、WDK Windows 7 ディスプレイ、CCD Api、コード例が表示されます。
- 接続すると、WDK Windows Server 2008 R2 ディスプレイ、CCD Api、コード例が表示されます。
- 構成 (WDK Windows 7 ディスプレイ、CCD Api、コード例)
- '構成: WDK Windows Server 2008 R2 display、CCD Api、コード例'
- CCD Api WDK Windows 7 display, サンプルコード
- CCD Api WDK Windows Server 2008 R2 display、例コード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b984ccb50b880966892d681e31e76f6df0c27d3a
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459236"
---
# <a name="ccd-example-pseudocode"></a>CCD のサンプル擬似コード

このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

次の擬似コードは、接続および構成ディスプレイ (CCD) Api を使用して複製ビューを設定する方法を示しています。

```cpp
SetCloneView
{
    // Determine the size of the path and mode information arrays needed
    // to hold all valid paths by calling GetDisplayConfigBufferSizes
    // with flags=QDC_ALL_PATHS

    // Using the returned numPathArrayElements and numModeInfoArrayElements,
    // allocate memory for the path and mode information arrays as follows:
    // pathArray size is numPathArrayElements*sizeof(DISPLAYCONFIG_PATH_INFO)
    // modeInfoArray size is numModeInfoArrayElements*sizeof(DISPLAYCONFIG_MODE_INFO)

    // Obtain the path and mode information for all possible paths by
    // calling QueryDisplayConfig with flags=QDC_ALL_PATHS and pointers
    // to the allocated path and mode info arrays.

    // Find the primary path by searching the returned array of
    // DISPLAYCONFIG_PATH_INFO structs for an active path that is
    // located at desktop position (0, 0).

    // Determine the user friendly name of the current primary by
    // calling DisplayConfigGetDeviceInfo with a type of
    // DISPLAYCONFIG_DEVICE_INFO_GET_TARGET_NAME, and the
    // adapter ID and target ID from the DISPLAYCONFIG_PATH_TARGET_INFO
    // of the primary path.

    // DisplayConfigGetDeviceInfo can determine the user friendly names
    // for all of the paths that might be part of the clone.
    // Allow the user to pick which monitor the clone is enabled on.
    // Only provide the user options of the paths from the current primary
    // to targets with monitors that are connected or that are forceable.  
    // Store a newClonePath pointer to the DISPLAYCONFIG_PATH_INFO that
    // the user picked.

    // Mark the new clone path as active:
    // NewClonePath->flags |= DISPLAYCONFIG_PATH_ACTIVE;
    // NewClonePath->sourceInfo.modeInfoIdx = DISPLAYCONFIG_PATH_MODE_IDX_INVALID;
    // NewClonePath->targetInfo.modeInfoIdx = DISPLAYCONFIG_PATH_MODE_IDX_INVALID;

    // Set the new topology by calling SetDisplayConfig with flags =
    // (SDC_APPLY | SDC_SAVE_TO_DATABASE | SDC_ALLOW_CHANGES
    //  | SDC_USE_SUPPLIED_DISPLAY_CONFIG) to change to the clone topology.
}
```
