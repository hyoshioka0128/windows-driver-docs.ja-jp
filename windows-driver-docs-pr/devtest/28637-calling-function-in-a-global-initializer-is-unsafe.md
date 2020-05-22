---
title: C28637
description: 警告 C28637 グローバル初期化子で関数を呼び出すことは安全ではありません。
ms.assetid: 9b392995-9583-4847-aded-f32e1daf28ed
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28637
ms.openlocfilehash: 71516b72d938fe9a65f978dff61f707da8dbe1bc
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769464"
---
# <a name="c28637"></a>C28637


警告 C28637: グローバル初期化子での関数の呼び出しは安全ではありません

DLL を使用する場合、多くの場合、静的コンストラクターは DllMain から呼び出されます。 DllMain から他の関数を呼び出すには、いくつかの制約が適用されます。 特に、DLL を動的に読み込んでアンロードする場合は、メモリリークを作成することができます。 詳細については、「 [DllMain コールバック関数](https://docs.microsoft.com/windows/win32/dlls/dllmain)」を参照してください。

 

 





