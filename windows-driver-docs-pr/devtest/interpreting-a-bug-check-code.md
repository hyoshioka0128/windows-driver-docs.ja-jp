---
title: バグチェックコードの解釈
description: Microsoft Windows が安全なシステム操作を侵害する状態を検出すると、システムは停止します。
ms.assetid: b5c8e18e-c2d3-47d9-b2bd-38aaaedcfde9
keywords:
- ツール WDK、バグチェックコード
- ドライバー開発ツール WDK、バグチェックコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab2b9e76d74cefd3761461a8627077ee004c7524
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840259"
---
# <a name="interpreting-a-bug-check-code"></a>バグチェックコードの解釈


Microsoft Windows が安全なシステム操作を侵害する状態を検出すると、システムは停止します。 この状態は*バグチェック*と呼ばれます。 また、一般に、*システムクラッシュ*、*カーネルエラー*、 *Stop エラー*、または*BSOD*と呼ばれます。 ハードウェアデバイス、そのドライバー、または関連するソフトウェアが原因でこのエラーが発生した可能性があります。

クラッシュダンプがシステムで有効になっている場合は、クラッシュダンプファイルが作成されます。

カーネルデバッガーがアタッチされ、アクティブになっている場合は、デバッガーを使用してクラッシュを調査できるように、システムによって中断が発生します。

デバッガーがアタッチされていない場合は、エラーに関する情報を含む青いテキスト画面が表示されます。 この画面は、*青い画面*、*バグチェック画面*、*ストップスクリーン*、または*BSOD*と呼ばれます。

## <span id="ddk_interpreting_bug_check_codes_tools"></span><span id="DDK_INTERPRETING_BUG_CHECK_CODES_TOOLS"></span>


バグチェック画面の正確な外観は、エラーの原因によって異なります。 次に、考えられる1つのバグチェック画面の例を示します。

```
STOP: 0x00000079 (0x00000002, 0x00000001, 0x00000002, 0x00000000)

Mismatched kernel and hal image.

Beginning dump of physical memory
Physical memory dump complete. Contact your system administrator or
technical support group.
```

一方、ブルースクリーンは次のようになります。

```
STOP: c000021a {Fatal System Error}

The Windows Logon Process system process terminated unexpectedly with
a status of 0x00000001 (0x00000000 0x00000000).
The system has been shut down.
```

### <span id="ddk_blue_screen_data_tools"></span><span id="DDK_BLUE_SCREEN_DATA_TOOLS"></span>

"STOP" という単語の後に続く16進数は、*バグチェックコード*または*停止コード*と呼ばれます。 これは、画面上で最も重要な項目です。

各バグチェックコードには、4つのパラメーターが関連付けられています。 ここに表示されている最初の青い画面では、バグチェックコードの後に4つのパラメーターがすべて表示されます。 ただし、2番目の種類のブルースクリーンでは、これらのパラメーターは説明テキスト内で再配置されています。 再配置の量に関係なく、常に順番に表示されます。 4つ未満のパラメーターが指定されている場合、残りのパラメーターは0であると見なすことができます。

青い画面の残りのテキストは、追加情報を提供します。 いくつかのバグチェックでは、この問題を解決する方法について説明します。 カーネルモードのダンプファイルが作成されている場合は、通常、これも示されます。

条件によっては、ブルースクリーンの最初の行のみが表示されます。 これは、表示に必要な重要なサービスがエラーの影響を受けた場合に発生する可能性があります。

### <a name="span-idbug_check_symbolic_namesspanspan-idbug_check_symbolic_namesspanbug-check-symbolic-names"></a><span id="bug_check_symbolic_names"></span><span id="BUG_CHECK_SYMBOLIC_NAMES"></span>バグチェックのシンボル名

各バグチェックコードには、関連付けられたシンボル名もあります。 これらの名前は、通常、青い画面には表示されません。 これらの例では、最初の画面に[**バグチェック 0x79**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x79--mismatched-hal) (一致しない\_HAL) が表示され、2番目の画面には[**バグチェック 0xc000021a**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc000021a--status-system-process-terminated) (ステータス\_システム\_プロセス\_終了) が表示されます。

バグチェックのシンボリック名を[**Kebugcheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kebugcheck)チェックまたは[**Kebugcheck checkex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kebugcheckex)に渡すことによって、カーネルモードドライバーから意図的にバグチェックを行うことができます。 これは、他のオプションが使用できない場合にのみ実行してください。

### <a name="span-idreading_bug_check_information_from_the_debuggerspanspan-idreading_bug_check_information_from_the_debuggerspanreading-bug-check-information-from-the-debugger"></a><span id="reading_bug_check_information_from_the_debugger"></span><span id="READING_BUG_CHECK_INFORMATION_FROM_THE_DEBUGGER"></span>デバッガーからバグチェック情報を読み取っています

デバッガーがアタッチされている場合は、バグチェックによって対象のコンピューターがデバッガーによって中断されます。 この場合、青い画面が表示されないか、または表示されるテキストが少なくなることがあります。このクラッシュの詳細はデバッガーに送信され、デバッガーウィンドウに表示されます。 詳細については、「[デバッガーの使用](using-a-debugger.md)」を参照してください。

バグチェックコードのこのリファレンスセクションは、 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)の一部として見つかります。 バグチェックとパラメーターの説明については、「[バグチェックコードリファレンス](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)」を参照してください。 各参照ページには、バグチェックコード、テキスト文字列、および各バグチェックと共に表示される4つの追加パラメーターが一覧表示されます。 また、バグチェックにつながるエラーを診断する方法、およびエラーに対処するための方法についても説明します。

バグチェックコードの完全な一覧については、「バグコード .h ファイル」を参照してください。 このファイルは、Microsoft Windows Driver Kit (WDK) の inc. のディレクトリにあります。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連項目


[バグチェック コード リファレンス](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)

[Windows のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)

 

 






