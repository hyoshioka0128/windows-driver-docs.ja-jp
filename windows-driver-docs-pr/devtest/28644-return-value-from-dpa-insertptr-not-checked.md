---
title: C28644
description: 警告のオフ DPA_InsertPtr から C28644 が返す値。
ms.assetid: F145330F-E597-405F-935E-B12D65F64DDB
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28644
ms.openlocfilehash: 268b8c835f58131a5250f218e39ba65af2ba51c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371473"
---
# <a name="c28644"></a>C28644


C28644 を警告します。DPA から値を返す\_InsertPtr チェックされません

この警告は、そのメモリを示します。 漏洩する可能性があります。

呼び出しの大部分は、 [ **DPA\_InsertPtr** ](https://docs.microsoft.com/windows/desktop/api/dpa_dsa/nf-dpa_dsa-dpa_insertptr)関数は、ヒープに割り当てられた変数を使用します。 関数は、DPA を使用し、DPA に格納されているすべてのオブジェクトを解放します。 ときに**DPA\_InsertPtr**失敗した場合、割り当てられたオブジェクトは、不要になったため、呼び出し元の DPA のクリーンアップ コードで解放**DPA\_InsertPtr**メモリを解放する必要があります。 呼び出しに注意してください**CleanupDPA**次の例です。 コードと同様の方法で割り当てられたオブジェクトを解放しないかどうかは**CleanupDPA**何も修正がありません。 この問題では、後で解放する必要があるすべてのオブジェクトを追跡する DPA に依存している前提としています。

次のコード例では、この警告が生成されます。

```
void Func()
{
    WCHAR*pszBuf=newWCHAR[MAX_PATH];
    DPA_InsertPtr(_hdpa, DA_LAST, pszBuf);
}

void CleanupDPA()
{
    int count = DPA_GetCount(_hdpa);
    for (int i = 0; i < count; i++)
{
    delete [] (LPWSTR)DPA_GetPtr(_hdpa, i);
}
}  
```

次のコード例は、この警告を回避できます。

```
void Func()
{
    WCHAR*pszBuf=newWCHAR[MAX_PATH];
    if (DPA_ERR == DPA_InsertPtr(_hdpa, DA_LAST, pszBuf))
    {
        delete [] pszBuf;
    }

}

void CleanupDPA()
{
    int count = DPA_GetCount(_hdpa);
    for (int i = 0; i < count; i++)
{
    delete [] (LPWSTR)DPA_GetPtr(_hdpa, i);
}
}  
```









