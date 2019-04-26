---
title: COPP デバイスの定義テンプレート コード
description: COPP デバイスの定義テンプレート コード
ms.assetid: 86cafb33-f92a-4c5d-8a54-37aab5e79f37
keywords:
- COPP デバイス WDK DirectX VA
- WDK COPP、COPP デバイス保護をコピーします。
- COPP WDK DirectX VA、COPP デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3910502765c9a12daed1639d4c70b71de4b9424
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346926"
---
# <a name="copp-device-definition-template-code"></a>COPP デバイスの定義テンプレート コード


## <span id="ddk_copp_device_definition_template_code_gg"></span><span id="DDK_COPP_DEVICE_DEFINITION_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

COPP DirectX VA デバイス オブジェクトを定義するのにには、次のコード例を使用します。

```cpp
#define COPP_OPENED                 0
#define COPP_CERT_LENGTH_RETURNED   1
#define COPP_KEY_EXCHANGED          2
#define COPP_SESSION_ACTIVE         3
typedef struct {
    DWORD   m_LocalLevel[COPP_MAX_TYPES];
    GUID    m_KDI;
    DWORD   m_CmdSeqNumber;
    DWORD   m_StatusSeqNumber;
    DWORD   m_rGraphicsDriver;
    DWORD   m_COPPDevState;
    DWORD   m_DevID;

    AESHelper   m_AesHelper;

} COPP_DeviceData;
```

 

 





