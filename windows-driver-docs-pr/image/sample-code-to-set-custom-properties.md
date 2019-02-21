---
title: カスタム プロパティを設定するサンプル コード
description: カスタム プロパティを設定するサンプル コード
ms.assetid: 726315eb-de5c-47b6-a35b-524ec1c97d52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 400c7f0f99334d8d6ea877b58249884648043ea1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531009"
---
# <a name="sample-code-to-set-custom-properties"></a>カスタム プロパティを設定するサンプル コード





カスタム プロパティを設定するには、アプリケーションやカスタム UI は、次のようなコードがあります。

```cpp
    IWiaPropertyStorage *pItemPropertyStorage = NULL;
 
    //
    //  Get the item's Property Storage
    //
    hr = pMyItem->QueryInterface(IID_IWiaPropertyStorage, (void**)&pItemPropertyStorage);
    if (SUCCEEDED(hr)) {

 
  //
  //  Variables to store the property value and identifier.
  //

  PROPVARIANT pvMyProperty;   // PropVariant to store property value.
  PROPSPEC    psMyProperty;   // PropSpec that identifies the property.
 
  psMyProperty.ulKind = PRSPEC_PROPID;
  psMyProperty.propid = myCustomPropID;   
  //  This should be the same value 
  //  that your driver has.  The
  //  best practice is to put a
  //  define in a header file
  //  that is common to driver
  //  and UI or the application components.
 
  //
  //  Initialize the PropVariant.
  //
  PropVariantInit(&pvMyProperty);
 
  //
  //  Fill in the property value.
  //  This example fills in the number 7 to a LONG type.
  //
  pvMyProperty.vt     = VT_I4;
  pvMyProperty.lVal   = 7;
 
  //
  //  Write the property value.
  //
  hr = pItemPropertyStorage->WriteMultiple(1,
                               &psMyProperty,
                               &pvMyProperty,
                                          0);
  //
  //  Etc.  
  //
  .
  .
  .
    }
```

 

 




