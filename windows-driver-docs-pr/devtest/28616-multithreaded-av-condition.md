---
title: C28616
description: 警告 C28616 マルチ スレッド AV 条件です。
ms.assetid: 77be6a23-18dc-420c-9359-ab91f216c73b
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28616
ms.openlocfilehash: 5b8809ce32ad3bfb3f88d46b9a627bf5a6f477f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347096"
---
# <a name="c28616"></a>C28616


C28616 を警告します。マルチ スレッド AV 条件

マルチ スレッド環境では、結果オブジェクトの参照カウントを減らすことの影響を及ぼさずはさらに、現在のスレッドの方が操作しなくても削除されることで、スレッドが割り込まれるタイミングを把握することはできません。 必要ない参照カウント オブジェクトへのアクセス、参照カウントの 0 である可能性が後です。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

この問題にさらされる可能性が時系列のスレッド処理の例を次に示します。

スレッド T1 は、行 1、2、および 3 をデクリメントを実行します。 **m\_cRef**を 1 に割り込まれるとします。

行 1、2、および 3 をデクリメントを実行する別のスレッド T2 **m\_cRef**を 0 にします。 行 4 と 5 を実行し、**この**が削除され、6 行目を最後に実行します。

T1 が再スケジュールされる場合は参照**m\_cref** 9 行目にします。 関連するこのポインターが削除された後にメンバー変数にアクセスしますので、オブジェクトのヒープが不明な状態の場合に、します。

```
  1 ULONG CObject::Release()
  2 {
  3     if ( 0 == InterlockedDecrement(&m_cRef) )
  4     {
  5         delete this;
  6         return NULL;
  7     }
  8     /* this.m_cRef isn't thread safe */
  9     return m_cRef;
 10 }
```

修正後の例では、オブジェクトが削除された後は、ヒープ メモリを参照しません。

```
ULONG CObject::Release()
{
 ASSERT( 0 != m_cRef );
 ULONG cRef = InterlockedDecrement(&m_cRef);
 if ( 0 == cRef )
 {
 delete this;
 }
 return cRef;
}
```

 

 





