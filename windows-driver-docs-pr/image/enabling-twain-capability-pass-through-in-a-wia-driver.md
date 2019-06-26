---
title: WIA ドライバーでの TWAIN 機能のパススルーの有効化
description: WIA ドライバーでの TWAIN 機能のパススルーの有効化
ms.assetid: b2108109-9e41-481d-bc25-67327420faf9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1371c590edfce629bb67291d4bb486e54402d77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385028"
---
# <a name="enabling-twain-capability-pass-through-in-a-wia-driver"></a>WIA ドライバーでの TWAIN 機能のパススルーの有効化





TWAIN 機能パススルーのサポートを有効にするには追加、 **WiaItemTypeTwainCapabilityPassThrough**フラグを[ **WIA\_IPA\_項目\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)ルート項目のプロパティ。 このフラグがヘッダー ファイルで定義されている*wiatwcmp.h*します。

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

 

 




