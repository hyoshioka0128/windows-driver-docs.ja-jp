---
title: OID_GEN_CO_HARDWARE_STATUS
description: このトピックでは、OID_GEN_CO_HARDWARE_STATUS オブジェクト識別子 (OID) について説明します。
ms.assetid: b846622a-a082-41e8-b32b-74c111b31f69
keywords:
- OID_GEN_CO_HARDWARE_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7241b2a9568c895298bf587ab1d2442714e1f36c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917964"
---
# <a name="oid_gen_co_hardware_status"></a>OID_GEN_CO_HARDWARE_STATUS

OID_GEN_CO_HARDWARE_STATUS OID は、基になる NIC の現在のハードウェアの状態を、次のいずれかの NDIS_HARDWARE_STATUS の種類の値として指定します。

**NdisHardwareStatusReady**  
ネットワーク経由でデータを送受信することができます。

**NdisHardwareStatusInitializing**  
初期化しています。

**NdisHardwareStatusReset**  
リセット。

**NdisHardwareStatusClosing**  
Closing.

**NdisHardwareStatusNotReady**  
準備ができていません。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

