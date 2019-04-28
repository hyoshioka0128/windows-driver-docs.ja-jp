---
title: C28135
description: 警告 C28135 場合 kewaitforsingleobject の 1 の最初の引数は、ローカル変数、モード パラメーターは kernelmode であるである必要があります。
ms.assetid: f42e41d7-240f-4de1-97b7-e50415aee14f
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28135
ms.openlocfilehash: 5ca20bf7553f43b6e8dfca9e5822c54ef45d65e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361398"
---
# <a name="c28135"></a>C28135


C28135 を警告します。Kewaitforsingleobject の 1 の最初の引数がローカル変数の場合は、モード パラメーターは kernelmode であるをする必要があります。

ドライバーは、ユーザー モードで待機しています。 そのため、カーネル スタックは、待機中に取り替えることができます。 ドライバーがスタック上のパラメーターを渡すしようとすると、システムのクラッシュが発生することができます。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
KeWaitForSingleObject(&MyMutex, UserRequest, UserMode, false, NULL);
```

次のコード例は、この警告を回避できます。

```
KeWaitForSingleObject(&MyMutex, UserRequest, KernelMode, false, NULL);
```

 

 





