---
title: C28615
description: _ _Try ブロックで _alloca を呼び出すときに、_ _except() ブロックで _resetstkoflw を呼び出す警告 C28615 する必要があります。 Catch() ブロック内から _resetstkoflw を呼び出さないでください。
ms.assetid: bccfc846-58b9-4c20-bbe7-383ecf836165
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28615
ms.openlocfilehash: e16ac49d93310cd045eda6d9acd43c977c06e76f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384129"
---
# <a name="c28615"></a>C28615


C28615 を警告します。呼び出す必要があります\_で resetstkoflw、 \_\_except() のブロックを呼び出すときに\_での alloca、 \_\_ブロックを実行してください。 呼び出さない\_catch() ブロック内から resetstkoflw

コード分析ツールは、アプリケーションを呼び出すときに、この警告を報告、  **\_resetstkoflw**関数は、catch ブロック内、またはアプリケーションを呼び出す**alloca**呼び出さずに try ブロックで **\_resetstkoflw**で、ブロックを除く。

スレッドが 1 つだけのスタック オーバーフロー例外をキャッチできます (への呼び出しで発生した **\_alloca**) スタックを修復しない限り、(たとえば、  **\_resetstkoflw**) 各例外の後に. スタックがから最初の例外が発生した後に固定していないかどうか **\_alloca**、サイレント モードでの即時プロセス終了に 2 つ目の例外が発生します。

呼び出す必要があります **\_resetstkoflw**現在のスタック ポインターがスタック上の 3 番目のページを超えるアドレスを指す場合。 ガード ページのスタック ポインターが指している現在のページから意味をなさない (または後で) ためにです。

**\_Resetstkoflw**構造化例外ハンドラーのフィルター式とは構造化例外ハンドラーのフィルター式から呼び出される関数から、関数を呼び出すことはできません。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

コード分析ツールは、フィルター式は、スタック アンワインドが発生する前に呼び出されるために、次の例では、この警告を報告します。 スタック オーバーフローがある場合は、フィルター式は、スタックの一番下から 3 番目のページに現在のスタック ポインターでポイントしたとき呼び出されます。

```
__try 
{
    /* The following could cause stack overflow */
    char *x = _alloca (i);
}
__except ((GetExceptionCode () == EXCEPTION_STACK_OVERFLOW) 
    ? (_resetstkoflw (), EXCEPTION_EXECUTE_HANDLER) 
    : EXCEPTION_CONTINUE_SEARCH)
{
}
```

次の例は、同様の理由でも失敗します。

```

__try 
{
 char *x = _alloca (i);
}
__except (SEHFilter (GetExceptionCode ()))
{
}

int SEHFilter (DWORD dwExceptionCode)
{
 if (dwExceptionCode == EXCEPTION_STACK_OVERFLOW)
 {
 _resetstkoflw ();
 return EXCEPTION_EXECUTE_HANDLER;
 }
 else
 {
 return EXCEPTION_CONTINUE_SEARCH;
 }
}
```

次の例では、正常にエラーを回避できます。

```
__try
{
    char *x = _alloca (i);
}
__except ((GetExceptionCode () == EXCEPTION_STACK_OVERFLOW) ? EXCEPTION_EXECUTE_HANDLER : EXCEPTION_CONTINUE_SEARCH)
{
    // In this block the stack has already been unwound,
    // so this call will succeed.
_resetstkoflw ();
}
```









