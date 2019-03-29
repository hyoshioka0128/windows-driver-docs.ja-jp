---
title: OID_GEN_CO_HARDWARE_STATUS
description: このトピックでは、OID_GEN_CO_HARDWARE_STATUS オブジェクト識別子 (OID) について説明します。
ms.assetid: b846622a-a082-41e8-b32b-74c111b31f69
keywords:
- OID_GEN_CO_HARDWARE_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e66f46a34e7f8afc5ac138ac7dfa0a3fcd5f0b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574902"
---
# <a name="oidgencohardwarestatus"></a>OID_GEN_CO_HARDWARE_STATUS

OID_GEN_CO_HARDWARE_STATUS OID は NDIS_HARDWARE_STATUS 型の値は次の 1 つとして、基になる NIC の現在のハードウェアの状態を指定します。

**NdisHardwareStatusReady**  
使用できると、ネットワーク経由でデータを送受信できます。

**NdisHardwareStatusInitializing**  
初期化しています。

**NdisHardwareStatusReset**  
リセットしています。

**NdisHardwareStatusClosing**  
終了します。

**NdisHardwareStatusNotReady**  
準備ができていません。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

