---
title: 例外処理
description: 例外処理
ms.assetid: 20040d86-5088-48ec-a5b9-54760d143871
keywords:
- 構造化例外処理 WDK カーネル
- 例外 (WDK カーネル)
- アクセス違反 WDK カーネル
- ハードウェアで定義された例外 (WDK カーネル)
- ソフトウェアで定義された例外の WDK カーネル
- エラー WDK カーネル
- ガード-ページ違反 WDK カーネル
- ページ読み取りエラー (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3038f0d5490ce44e1ab4ddcb99d140627548ca03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836551"
---
# <a name="handling-exceptions"></a>例外処理





オペレーティングシステムでは、構造化例外処理を使用して特定の種類のエラーを通知します。 ドライバーによって呼び出されるルーチンは、ドライバーが処理する必要がある例外を発生させることができます。

システムは、次の一般的な種類の例外をトラップします。

1.  ハードウェアで定義されたエラーまたはトラップ (など)

    -   アクセス違反 (下記を参照)
    -   データ型の間違った配置 (奇数バイトの境界に配置された16ビットエンティティなど)
    -   無効な特権のある命令
    -   無効なロックシーケンス (コードのインタロックされたセクション内の無効な命令シーケンスを実行しようとしています)
    -   0とオーバーフローで除算された整数
    -   0、オーバーフロー、アンダーフロー、および予約されたオペランドで除算された浮動小数点
    -   ブレークポイントとシングルステップ実行 (デバッガーをサポートするため)

2.  システムソフトウェアで定義された例外 (など)

    -   ガードページの違反 (ガードページ内の場所との間でデータの読み込みまたは保存を試行)
    -   ページ読み取りエラー (ページをメモリに読み込み、同時 i/o エラーが発生した場合)

*アクセス違反*は、現在のページ保護設定で許可されていないページに対して操作を実行しようとしています。 アクセス違反は、次の状況で発生します。

-   読み取り専用ページへの書き込みなど、無効な読み取りまたは書き込み操作です。

-   現在のプログラムのアドレス空間の制限を超えてメモリにアクセスする場合 (長さ違反と呼ばれます)。

-   現在常駐しているが、システムコンポーネントの使用専用のページにアクセスする場合。 たとえば、ユーザーモードコードは、カーネルが使用しているページへのアクセスを許可されていません。

操作によって例外が発生する可能性がある場合、ドライバーは**try/except**ブロックで操作を囲む必要があります。 ユーザーモードでの場所へのアクセスは、一般的な例外の原因です。 たとえば、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)ルーチンは、ドライバーが実際にユーザーモードバッファーに書き込むことができるかどうかをチェックします。 これができない場合、ルーチンは\_アクセス\_違反例外の状態を発生させます。 次のコード例では、ドライバーは**try/except**で**ProbeForWrite**を呼び出して、発生した例外を処理できるようにします。

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

ドライバーは、発生した例外を処理する必要があります。 処理されない例外が発生すると、システムはバグチェックを行います。 例外を発生させるドライバーは、例外を処理する必要があります。下位レベルのドライバーは、例外を処理するために上位レベルのドライバーに依存することはできません。

ドライバーは、 [**ExRaiseAccessViolation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)、 [**ExRaiseDatatypeMisalignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)、または[**ExRaiseStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)ルーチンを使用して、例外を直接発生させることができます。 ドライバーは、これらのルーチンによって発生する例外を処理する必要があります。

次に示すのは、少なくとも特定の状況で例外が発生する可能性があるルーチンの部分的な一覧です。

-   [**MmMapLockedPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)

-   [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

-   [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

-   [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

ユーザーモードのバッファーへのメモリアクセスは、アクセス違反の原因になる場合もあります。 詳細については、「[ユーザー領域の参照」の「エラー](errors-in-referencing-user-space-addresses.md)」を参照してください。

構造化例外処理はC++例外とは異なることに注意してください。 カーネルは例外をサポートC++していません。

構造化例外処理の詳細については、Microsoft Windows SDK、および Visual Studio のドキュメントを参照してください。

 

 




