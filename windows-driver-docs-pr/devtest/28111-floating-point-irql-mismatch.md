---
title: C28111
description: 浮動小数点状態が保存されている警告 C28111、IRQL が (この復元操作) の現在の IRQL と一致しません。
ms.assetid: 3573ebf0-5f5b-4b04-835a-7dba36e95e8c
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28111
ms.openlocfilehash: 1cc2af385b96e1177fce0c8e425eab5c19fcf1bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581390"
---
# <a name="c28111"></a>C28111


C28111 を警告します。浮動小数点状態が保存された IRQL (この復元操作) の現在の IRQL が一致しません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>浮動小数点の保存/復元機能では、IRQL 同じであること、保存時と対応する復元に必要です。</p></td>
</tr>
</tbody>
</table>

 

浮動小数点状態を復元するときに、ドライバーが実行して IRQL を実行していた浮動小数点状態を保存するときに IRQL と異なります。

保存し、浮動小数点状態を復元する関数を呼び出すときに、ドライバーが実行される IRQL が浮動小数点状態を保存する方法を決定しますので、同じ IRQL でドライバーを実行する必要があります。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
void driver_utility()
{
    // running at APC level
    KFLOATING_SAVE FloatBuf;
    if (KeSaveFloatingPointState(&FloatBuf))
    {
        KeLowerIrql(PASSIVE_LEVEL);
        ...
        KeRestoreFloatingPointState(&FloatBuf);
    }
}
```

次のコード例は、この警告を回避できます。

```
void driver_utility()
{
    // running at APC level
    KFLOATING_SAVE FloatBuf;
    if (KeSaveFloatingPointState(&FloatBuf))
    {
        KeLowerIrql(PASSIVE_LEVEL);
        ...
        KeRaiseIrql(APC_LEVEL, &old);
        KeRestoreFloatingPointState(&FloatBuf);
    }
}
```

 

 





