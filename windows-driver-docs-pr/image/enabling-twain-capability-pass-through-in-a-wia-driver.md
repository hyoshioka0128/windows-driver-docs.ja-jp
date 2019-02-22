---
title: WIA ドライバーでは、TWAIN 機能パススルーを有効にします。
description: WIA ドライバーでは、TWAIN 機能パススルーを有効にします。
ms.assetid: b2108109-9e41-481d-bc25-67327420faf9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49a79ddc3846d23fbc6e20da11e8c50144557c11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528850"
---
# <a name="enabling-twain-capability-pass-through-in-a-wia-driver"></a>WIA ドライバーでは、TWAIN 機能パススルーを有効にします。





TWAIN 機能パススルーのサポートを有効にするには追加、 **WiaItemTypeTwainCapabilityPassThrough**フラグを[ **WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)ルート項目のプロパティ。 このフラグがヘッダー ファイルで定義されている*wiatwcmp.h*します。

次の例がから取得した、 *wiascanr*サンプル (ドライバー開発キットに含まれている\[DDK\]) の使用方法と、 **WiaItemTypeTwainCapabilityPassThrough**フラグ)。

```cpp
// Initialize WIA_IPA_ITEM_FLAGS
  m_pszRootItemDefaults[PropIndex] = WIA_IPA_ITEM_FLAGS_STR;
  m_piRootItemDefaults[PropIndex] = WIA_IPA_ITEM_FLAGS;
// Next assignment adds the WiaItemTypeTwainCapabilityPassThrough flag.
  m_pvRootItemDefaults[PropIndex].lVal = 
     WiaItemTypeRoot|WiaItemTypeFolder | 
     WiaItemTypeDevice| WiaItemTypeTwainCapabilityPassThrough;
  m_pvRootItemDefaults[PropIndex].vt = VT_I4;
  m_psRootItemDefaults[PropIndex].ulKind = PRSPEC_PROPID;
  m_psRootItemDefaults[PropIndex].propid = 
     m_piRootItemDefaults[PropIndex];
  m_wpiRootItemDefaults[PropIndex].lAccessFlags = 
     WIA_PROP_READ | WIA_PROP_FLAG;
  m_wpiRootItemDefaults[PropIndex].vt = 
     m_pvRootItemDefaults [PropIndex].vt;
  m_wpiRootItemDefaults[PropIndex].ValidVal.Flag.Nom = 
     m_pvRootItemDefaults [PropIndex].lVal;
  m_wpiRootItemDefaults[PropIndex].ValidVal.Flag.ValidBits = 
     WiaItemTypeRoot | WiaItemTypeFolder|WiaItemTypeDevice;
```

 

 




