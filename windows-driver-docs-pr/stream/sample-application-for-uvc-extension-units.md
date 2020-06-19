---
title: UVC 拡張ユニットのサンプル アプリケーション
description: UVC 拡張機能ユニットのサンプルアプリケーション
ms.assetid: f900b0b1-3469-442f-8593-2094a0966d4a
keywords:
- 拡張機能ユニット WDK USB ビデオクラス, サンプル, サンプルアプリケーション
- サンプルコード WDK USB ビデオクラス、UVC 拡張ユニット
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 68144abcaf7519e88f58a6e7461a30e5b4c0bcbc
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073423"
---
# <a name="sample-application-for-uvc-extension-units"></a>UVC 拡張機能ユニットのサンプルアプリケーション

このトピックには、拡張機能ユニットをサポートするために使用できるサンプルアプリケーションコードが含まれています。

アプリケーションは、 [**IKsTopologyInfo:: Creat Deinstance**](https://docs.microsoft.com/previous-versions/windows/desktop/api/Vidcap/nf-vidcap-ikstopologyinfo-createnodeinstance)の後に node オブジェクトで**QueryInterface**を呼び出して必要な COM API を取得することによって、インターフェイスにアクセスします。 詳細については、「 [**IKsTopologyInfo**](https://docs.microsoft.com/previous-versions/windows/desktop/api/Vidcap/nn-vidcap-ikstopologyinfo)」を参照してください。

次のコードをアプリケーションソースに追加します。これには、TestApp という名前を付けます。

また、「[拡張単位を使用した自動更新イベントのサポート](supporting-autoupdate-events-with-extension-units.md)」に示されているコードを TestApp に含めます。

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

この場合、 **pUnkOuter**は、USB ビデオクラス (uvc) デバイスを表すキャプチャフィルターへのポインターである必要があります。 キャプチャフィルターをフィルターグラフに追加した後、次のサンプルコードに示すように、 **IKsTopologyInfo**インターフェイスのフィルターに対してクエリを実行できます。

**FindExtensionNode**関数のコードを記述して、必要な拡張ユニットノードを特定し、その ID を*dwextensionnode*に返すようにします。 この ID は、 **IKsTopologyInfo:: Creat Deinstance**メソッドの後続の呼び出しで使用されます。
