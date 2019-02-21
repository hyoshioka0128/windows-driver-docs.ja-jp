---
title: C28129
description: ビットを設定およびクリアを使用してのみ変更する必要があります、オペランドへの割り当てが確立されて C28129 を警告します。
ms.assetid: b5afad45-6498-42f3-b1aa-9ba3cc8abb6d
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28129
ms.openlocfilehash: d62f0973b5f806675ea1a428d0b4388ec4a7e250
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537105"
---
# <a name="c28129"></a>C28129


C28129 を警告します。ビットを設定およびクリアを使用してのみ変更する必要があります、オペランドへの割り当てが確立されて

ドライバーは、オペランドを変更する代入を使用しています。 値を割り当てることが意図せず値を変更ビットを変更するために必要なもの以外の予期しない結果に。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
fdo->Flags = DO_BUFFERED_IO;
```

次のコード例は、この警告を回避できます。

```
fdo->Flags |= DO_BUFFERED_IO;
```

 

 





