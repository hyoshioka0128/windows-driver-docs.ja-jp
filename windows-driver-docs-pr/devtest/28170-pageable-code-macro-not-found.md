---
title: C28170
description: 警告 C28170 関数として宣言されているページのセグメントであるが、PAGED_CODE も PAGED_CODE_LOCKED もが見つかりました。
ms.assetid: 9efffcc8-54b6-46f8-b037-53c66a8eace2
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28170
ms.openlocfilehash: 8831016dc62669b36096bbb4ed3093730a50100c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361320"
---
# <a name="c28170"></a>C28170


C28170 を警告します。ページのセグメントはどちらもページに、関数が宣言された\_コードもページング\_コード\_ロックが見つかりました

このエラーを報告するコード分析ツールと **\#プラグマ アロケーション\_テキスト**または **\#プラグマ コード\_seg**にはない関数を移動するために使用ページングを含む\_コードまたはページ\_コード\_ページング可能なコード セクションにマクロをロックします。 最初の中かっこにこのエラーが報告に対応する行番号 ( **{** ) 関数。

コード分析ツールでは、ページ セクション名の開始時にセクションではページング可能を推測します。 ページング可能なコード内の関数は、ページングを含める必要があります\_コードまたはページング\_コード\_最初の中かっこの間で関数の先頭にロック済みのマクロ ( **{** ) と、最初の条件付きステートメント。

これらのマクロは、コード分析ツールと管理者特権での IRQL でページング可能なコードを実行する可能性があるかどうかを確認する実行時チェックを許可します。 システムの管理者特権でのレベルで実行中に、ページ フォールトが発生した場合、システムがクラッシュします。

ページング セグメント内の関数は、その後メモリにロックされている場合は、ページを使用して\_コード\_ページではなくロック\_コード。 ページ\_コード\_ロック済みのマクロの許可: PREfast for Drivers を発生させることがなく、IRQL を発生させる呼び出しを行うドライバー警告します。

この条件は、多くの場合、テスト中に検索する非常に困難です (しない限り、ページング\_コードのマクロが、エラーをチェックするドライバーの検証に使用されます)、ページ フォールトが発生するのコードがページング実際にする必要がありますので。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
void func();
#pragma alloc_text("PAGED_CODE", func);

void func1()
{
   // paged, no PAGED_CODE: error
}
```

次のコード例は、この警告を回避できます。

```
void func();
#pragma alloc_text("PAGED_CODE", func);

void func2()
{
   PAGED_CODE(); // includes PAGED_CODE macro
}
```

 

 





