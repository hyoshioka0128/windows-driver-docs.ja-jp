---
title: UVC 拡張ユニットのサンプル アプリケーション
description: UVC 拡張ユニットのサンプル アプリケーション
ms.assetid: f900b0b1-3469-442f-8593-2094a0966d4a
keywords:
- 拡張機能ユニット WDK USB ビデオ クラス、サンプル、サンプル アプリケーション
- サンプル コード WDK USB ビデオ クラス、UVC 拡張ユニット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a661099f55e56e29e5802cd0f02c704f7ebc8c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581272"
---
# <a name="sample-application-for-uvc-extension-units"></a>UVC 拡張ユニットのサンプル アプリケーション


このトピックには、ユニットの拡張機能をサポートするために使用できるサンプル アプリケーションのコードが含まれています。

アプリケーションを使用して、インターフェイスにアクセスして**IKsTopologyInfo::CreateNodeInstance**への呼び出しに続く**QueryInterface**で必要な COM API を取得するノード オブジェクト。 **IKsTopologyInfo**にインターフェイスが記載されている、 [API とリファレンスのカタログ](https://go.microsoft.com/fwlink/p/?linkid=27252)web サイト。

任意 TestApp.cpp という名前のアプリケーションのソースで、次のコードを含めます。

コードを TestApp.cpp にも含める[単位の拡張機能で自動更新のイベントをサポートしている](supporting-autoupdate-events-with-extension-units.md)します。

```cpp
  // pUnkOuter is the unknown associated with the base filter
  hr = pUnkOuter->QueryInterface(__uuidof(IKsTopologyInfo), 
                               (void **) &pKsTopologyInfo);
  if (!SUCCEEDED(hr))
  {
        printf("Unable to obtain IKsTopologyInfo %x\n", hr);
 goto errExit;
  }

  hr = FindExtensionNode(pKsTopologyInfo,                                                                                                   
     GUID_EXTENSION_UNIT_DESCRIPTOR,
     &dwExtensionNode);
  if (FAILED(hr))
  {
        printf("Unable to find extension node : %x\n", hr);
 goto errExit;
  }

  hr = pKsTopologyInfo->CreateNodeInstance(
        dwExtensionNode, 
   __uuidof(IExtensionUnit), 
 (void **) &pExtensionUnit);
 if (FAILED(hr))
  {
        printf("Unable to create extension node instance : %x\n", hr);
 goto errExit;
  }

  hr = pExtensionUnit->get_PropertySize(1, &ulSize);
  if (FAILED(hr))
  {
        printf("Unable to find property size : %x\n", hr);
 goto errExit;
  }

  pbPropertyValue = new BYTE[ulSize];
  if (!pbPropertyValue)
  {
      printf("Unable to allocate memory for property value\n");
      goto errExit;
  }

  hr = pExtensionUnit->get_Property(1,ulSize, pbPropertyValue);
  if (FAILED(hr))
  {
      printf("Unable to get property value\n");
      goto errExit;
  }
 
  // assume the property value is an integer
  ASSERT(ulSize == 4);
  printf("The value of property 1 = %d\n", *((int *) 
     pbPropertyValue));
```

この場合、 **pUnkOuter** USB ビデオ クラス (UVC) デバイスを表すキャプチャ フィルターへのポインターにする必要があります。 フィルターのクエリを実行できるフィルター グラフをキャプチャ フィルターを追加した後、 **IKsTopologyInfo**インターフェイスのこのサンプル コードで示すようにします。

コードを記述、 **FindExtensionNode**関数では、その ID を返すと、必要な拡張ユニットのノードを検索する*dwExtensionNode*します。 このサンプル コードの後続の呼び出しでこの ID が使用される、 **IKsTopologyInfo::CreateNodeInstance**メソッド。

 

 




