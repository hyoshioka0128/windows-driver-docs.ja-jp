---
title: 中間ドライバー UpperRange および LowerRange INF ファイル エントリ
description: 中間ドライバー UpperRange および LowerRange INF ファイル エントリ
ms.assetid: 12a8561c-d410-45d0-8e96-898af6343f89
keywords:
- 中間ドライバーの INF ファイル WDK ネットワーク
- UpperRange INF ファイルのエントリ
- LowerRange INF ファイルのエントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d9b4d6136adfda339cff0b4e1c4cb3910b37ce6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362920"
---
# <a name="intermediate-driver-upperrange-and-lowerrange-inf-file-entries"></a>中間ドライバー UpperRange および LowerRange INF ファイル エントリ





このトピックでは、使用する方法を説明します、 **UpperRange**と**LowerRange** NDIS を定義する INF ファイルのエントリは中間ドライバー バインドのリレーションシップ。

ネットワーク ドライバーの INF ファイルで、 **UpperRange**エントリには、可能な上限バインドが一覧表示されます、 **LowerRange**エントリには、可能な下位のバインドが一覧表示されます。 これらのリストをさまざまなシステム定義の値があります。

ドライバーの中間フィルターの値を設定する必要があります、 **UpperRange**と**LowerRange**エントリ**noupper**と**nolower**、それぞれします。 は、プロトコルの INF ファイルでのみこれらのエントリを定義する必要がありますミニポート ドライバーの INF ファイルにする必要はありません。 次のコード例では、これらのエントリのフィルターの中間ドライバーを示します。

```INF
HKR, Ndi\Interfaces, UpperRange, , noupper
HKR, Ndi\Interfaces, LowerRange, , nolower
```

フィルターの中間ドライバーで、 **FilterMediaTypes**プロトコル INF ファイルのエントリは、他のドライバーをドライバーのバインドを定義します。 **FilterMediaTypes**フィルターの中間ドライバーによって処理されたメディアの種類を指定します。 可能なメディアの種類の一覧は、Microsoft 提供の一覧を参照してください。 **LowerRange**値[バインド インターフェイスを指定する](specifying-binding-interfaces.md)します。 次のコード例は、フィルターの中間ドライバーのこのエントリを示しています。

```INF
HKR, Ndi\Interfaces, FilterMediaTypes, , "ethernet, tokenring, fddi, wan"
```

フィルターの中間ドライバーが初期化されるときに挿入します自体で表示されているメディアの種類に該当するすべての既存のプロトコルのミニポートにバインド**FilterMediaTypes**します。

MUX 中間ドライバーについて必ず設定して**UpperRange**プロトコル INF ファイルに**noupper**します。 設定**LowerRange**の許容された値から取得した値の一覧に**LowerRange、** で指定されている[バインド インターフェイスを指定する](specifying-binding-interfaces.md)します。 次のコード例は、MUX 中間ドライバーの下端のこれらのエントリを示しています。

```INF
HKR, Ndi\Interfaces, UpperRange, 0, "noupper"
HKR, Ndi\Interfaces, LowerRange, 0, "ndis5"
```

MUX 中間ドライバーについて必ず設定して**LowerRange**ミニポート ドライバーの INF ファイルに**nolower**します。 設定、 **UpperRange**の許容された値から取得した値の一覧に、 **UpperRange、** で指定されている[バインド インターフェイスを指定する](specifying-binding-interfaces.md)します。 次のコード例は、MUX の中間ドライバー仮想ミニポートのこれらのエントリを示しています。

```INF
HKR, Ndi\Interfaces, UpperRange, 0, "ndis5"
HKR, Ndi\Interfaces, LowerRange, 0, "nolower"
```

 

 





