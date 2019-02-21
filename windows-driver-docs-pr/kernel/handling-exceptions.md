---
title: 例外の処理
description: 例外の処理
ms.assetid: 20040d86-5088-48ec-a5b9-54760d143871
keywords:
- 構造化例外処理の WDK カーネル
- 例外の WDK カーネル
- アクセス違反の WDK カーネル
- ハードウェア定義の例外の WDK カーネル
- ソフトウェア定義の例外の WDK カーネル
- エラー WDK カーネル
- ガード ページ違反の WDK カーネル
- ページの読み込みエラー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a3fc196616a9d610349f7f3660d2f70576ad135
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535568"
---
# <a name="handling-exceptions"></a>例外の処理





オペレーティング システムでは、構造化例外処理を特定の種類のエラーの通知を使用します。 ドライバーによって呼び出されるルーチンでは、ドライバーが処理する必要がある例外を生成できます。

システムでは、次の一般的な種類の例外をトラップします。

1.  ハードウェア定義されたエラーまたはトラップ、次のように、

    -   アクセス違反 (下記参照)
    -   (奇数バイト境界に整列する 16 ビット エンティティ) などのデータ型のずれ
    -   無効なと特権命令
    -   無効なロックのシーケンス (手順については、インタロックされたセクションのコード内での無効なシーケンスを実行しようとしています)
    -   整数は 0 で除算し、オーバーフローしています
    -   0、オーバーフロー、アンダー フロー、および予約済みのオペランドで浮動小数点除算します。
    -   ブレークポイントとシングル ステップ実行 (デバッガーをサポート) する

2.  システム ソフトウェア定義の例外では、次のように、

    -   ガード ページ違反の (読み込みまたはまたはガード ページ内の場所からデータを格納しようとしています)
    -   ページの読み込みエラー (ページをメモリに読み込まれるしようと同時実行の I/O エラーが発生しました)

*アクセス違反*は現在のページ保護の設定で許可されていないページの操作を実行しようとします。 アクセス違反は、次の状況で発生します。

-   無効なの読み取りまたは書き込み操作は、読み取り専用ページへの書き込みなど。

-   (長さ違反と呼ばれます)、現在プログラムのアドレス空間の制限を超えるメモリにアクセスします。

-   現在常駐しているが、システムのコンポーネントを使用する専用ページにアクセスします。 たとえば、ユーザー モード コードが、カーネルを使用しているページへのアクセスを許可します。

操作は、例外を引き起こす可能性がある場合、ドライバーがで操作を囲む必要があります、**試用/を除く**ブロックします。 ユーザー モードでの場所のアクセスには、例外の一般的な原因です。 たとえば、 [ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)ルーチンは、ドライバーがユーザー モード バッファーに書き込むことが実際にことを確認します。 ルーチンが状態を生成できない場合は、\_アクセス\_違反例外が発生します。 ドライバーの呼び出しでは、次のコード例では、 **ProbeForWrite**で、**試用/を除く**いずれかが発生した場合、結果の例外を処理できるようにします。

```cpp
try {
    ...
    ProbeForWrite(Buffer, BufferSize, BufferAlignment);
 
    /* Note that any access (not just the probe, which must come first,
     * by the way) to Buffer must also be within a try-except.
     */
    ...
} except (EXCEPTION_EXECUTE_HANDLER) {
    /* Error handling code */
    ...
}
```

ドライバーが発生した例外を処理する必要があります。 処理されない例外はにより、システムのバグ チェックです。 発生する例外が発生したドライバーが処理する必要があります: 下位レベルのドライバーが例外を処理するより高度なドライバーに依存できません。

ドライバーを使用して、例外を発生できる直接、 [ **ExRaiseAccessViolation**](https://msdn.microsoft.com/library/windows/hardware/ff545509)、 [ **ExRaiseDatatypeMisalignment**](https://msdn.microsoft.com/library/windows/hardware/ff545524)、または[**ExRaiseStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff545529)ルーチン。 ドライバーは、これらのルーチンを発生させる例外を処理する必要があります。

次は、少なくとも特定の状況で例外が生成するルーチンの部分的な一覧です。

-   [**MmMapLockedPages**](https://msdn.microsoft.com/library/windows/hardware/ff554622)

-   [**MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)

-   [**ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)

-   [**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)

メモリ アクセスをユーザー モードのバッファーにもアクセス違反があります。 詳細については、次を参照してください。[ユーザー スペースのアドレスを参照するエラー](errors-in-referencing-user-space-addresses.md)します。

構造化例外処理が C++ 例外から個別であることに注意してください。 カーネルは、C++ 例外処理をサポートしていません。

構造化例外処理の詳細については、Microsoft Windows SDK、および Visual Studio のドキュメントを参照してください。

 

 




