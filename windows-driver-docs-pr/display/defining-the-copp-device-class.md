---
title: COPP デバイス クラスの定義
description: COPP デバイス クラスの定義
ms.assetid: eb5e7269-fe4c-44d1-9024-f5b1a180e10b
keywords:
- WDK COPP、COPP デバイス保護をコピーします。
- ビデオのコピー防止 WDK COPP、COPP デバイス
- COPP WDK DirectX VA、COPP デバイス
- ビデオの WDK COPP COPP デバイスを保護
- COPP デバイス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d4f2fe1fd6e4e6ba783bb485ee2e75569837e2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578226"
---
# <a name="defining-the-copp-device-class"></a>COPP デバイス クラスの定義


## <span id="ddk_defining_the_copp_device_class_gg"></span><span id="DDK_DEFINING_THE_COPP_DEVICE_CLASS_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

COPP デバイス クラスを定義するのにには、次のコード例を使用します。

```cpp
// COPP device class.
struct DXVA_COPPDeviceClass : public DXVA_DeviceBaseClass
{
    VOID*   m_pThis;
};
```

 

 





