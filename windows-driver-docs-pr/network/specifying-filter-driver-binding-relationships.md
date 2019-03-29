---
title: フィルター ドライバー バインド関係の指定
description: フィルター ドライバー バインド関係の指定
ms.assetid: 0f0b81f4-2ac1-456c-aef0-73f3bbb7ce0e
keywords:
- フィルター ドライバー WDK ネットワークは、バインディングの関係
- NDIS フィルター ドライバー WDK、バインドのリレーションシップ
- バインドのリレーションシップの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c5bf6bad865d6bc039f032f1dba208f9da0c8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579906"
---
# <a name="specifying-filter-driver-binding-relationships"></a>フィルター ドライバー バインド関係の指定





ネットワーク ドライバーの INF ファイルで、 **UpperRange**エントリには、可能な上限バインドが一覧表示されます、 **LowerRange**エントリには、可能な下位のバインドが一覧表示されます。 これらのエントリは、さまざまなシステム定義の値を含めることができます。

フィルター ドライバーの値を設定する必要があります、 **UpperRange**と**LowerRange**エントリ**noupper**と**nolower**、それぞれします。 次の例では、これらの INF ファイル エントリのフィルター ドライバーを示します。

```INF
HKR, Ndi\Interfaces,UpperRange,,"noupper"
HKR, Ndi\Interfaces,LowerRange,,"nolower"
```

フィルター ドライバー、 **FilterMediaTypes**フィルター INF ファイルのエントリは、他のドライバーをドライバーのバインドを定義します。 **FilterMediaTypes**メディアの種類を指定します。 ドライバー サービスのフィルター処理します。 可能なメディアの種類の一覧は、Microsoft 提供の一覧を参照してください。 **LowerRange**値[バインド インターフェイスを指定する](specifying-binding-interfaces.md)します。 次の例を示しています、 **FilterMediaTypes**フィルター ドライバーのエントリ。

```INF
HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
```

ドライバーがすべての既存のアダプターのプロトコルのバインドに挿入されます、種類によっては、メディア、コンピューターには、フィルター ドライバーが読み込まれたら、 **FilterMediaTypes**を一覧表示します。

 

 





