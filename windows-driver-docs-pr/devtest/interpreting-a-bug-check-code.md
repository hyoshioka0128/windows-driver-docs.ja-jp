---
title: バグ チェック コードの解釈
description: Microsoft Windows には、その妥協安全なシステム操作の条件が検出されると、システムを停止します。
ms.assetid: b5c8e18e-c2d3-47d9-b2bd-38aaaedcfde9
keywords:
- ツールを WDK バグ チェック コード
- ドライバーの開発ツールを WDK、バグの確認コード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ad601c2da8e67a4ae181e9f03e7bc2adad2ebf4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340478"
---
# <a name="interpreting-a-bug-check-code"></a>バグ チェック コードの解釈


Microsoft Windows には、その妥協安全なシステム操作の条件が検出されると、システムを停止します。 この条件と呼ばれる、*バグ チェック*します。 としても一般的に指す、*システム クラッシュ*、*カーネル エラー*、*停止エラー*、または*BSOD*します。 ハードウェア デバイス、そのドライバー、または関連するソフトウェアが、このエラーを引き起こしたがある可能性があります。

システムのクラッシュ ダンプが有効な場合は、クラッシュ ダンプ ファイルが作成されます。

カーネル デバッガーがアタッチされ、アクティブなシステム ブレークを発生させるため、クラッシュを調査するデバッガーを使用できます。

デバッガーがアタッチされていない場合、エラーに関する情報を青色のテキスト画面が表示されます。 この画面と呼ばれる、*ブルー スクリーン*、*バグ チェック画面*、*停止画面*、または*BSOD*します。

## <span id="ddk_interpreting_bug_check_codes_tools"></span><span id="DDK_INTERPRETING_BUG_CHECK_CODES_TOOLS"></span>


正確なバグの確認画面の外観は、エラーの原因によって異なります。 考えられるバグ チェックの 1 つの画面の例を次に示します。

```
STOP: 0x00000079 (0x00000002, 0x00000001, 0x00000002, 0x00000000)

Mismatched kernel and hal image.

Beginning dump of physical memory
Physical memory dump complete. Contact your system administrator or
technical support group.
```

その一方で、このようないくつかのブルー スクリーンになります。

```
STOP: c000021a {Fatal System Error}

The Windows Logon Process system process terminated unexpectedly with
a status of 0x00000001 (0x00000000 0x00000000).
The system has been shut down.
```

### <span id="ddk_blue_screen_data_tools"></span><span id="DDK_BLUE_SCREEN_DATA_TOOLS"></span>

16 進数の次の単語"STOP"と呼びます、*チェックのコードをバグ*または*停止コード*します。 これは、画面上の最も重要な項目です。

各バグ チェックのコードでは、次の 4 つの関連するパラメーターを持っています。 ここで示すように青の最初の画面でのバグがコードを確認後、4 つすべてのパラメーターが表示されます。 ただし、2 つ目の種類のブルー スクリーンでは、これらのパラメーターは、説明のテキスト内で再配置されたが。 再配置の量に関係なく常に表示されます順番にします。 4 つより少ないパラメーターが表示されない場合は、残りのパラメーターはことができますを 0 にすると見なされます。

ブルー スクリーン上のテキストの残りの部分では、追加の情報を提供します。 いくつかのバグ チェック用の変更点や問題に対処する方法の提案の説明があります。 カーネル モードのダンプ ファイルが書き込まれた場合、通常、示されるもします。

Windows では、いくつかの条件下でブルー スクリーンの最初の行のみが表示されます。 これは、表示のために必要な重要なサービスは、エラーによって影響を受けている場合に発生することができます。

### <a name="span-idbugchecksymbolicnamesspanspan-idbugchecksymbolicnamesspanbug-check-symbolic-names"></a><span id="bug_check_symbolic_names"></span><span id="BUG_CHECK_SYMBOLIC_NAMES"></span>バグ チェックのシンボル名

各バグ チェックのコードでは、関連付けられているシンボリック名もあります。 これらの名前は、通常、ブルー スクリーンには表示されません。 これらの例では、最初の画面が表示されます[**バグ チェック 0x79** ](https://msdn.microsoft.com/library/windows/hardware/ff559209) (不一致\_HAL)、2 つ目が表示されますが、 [**バグ チェック 0xC000021A**](https://msdn.microsoft.com/library/windows/hardware/ff560177) (ステータス\_システム\_プロセス\_終了)。

バグ チェックのシンボリック名を渡すことによってカーネル モード ドライバーからのバグ チェックが発生することが意図的に[ **KeBugCheck** ](https://msdn.microsoft.com/library/windows/hardware/ff551948)または[ **KeBugCheckEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551961). これは、その他のオプションが使用可能な状況でのみ実行する必要があります。

### <a name="span-idreadingbugcheckinformationfromthedebuggerspanspan-idreadingbugcheckinformationfromthedebuggerspanreading-bug-check-information-from-the-debugger"></a><span id="reading_bug_check_information_from_the_debugger"></span><span id="READING_BUG_CHECK_INFORMATION_FROM_THE_DEBUGGER"></span>デバッガーからのバグ チェック情報の読み取り

デバッガーがアタッチされているバグ チェックが、デバッガーを中断する対象のコンピュータに発生します。 ブルー スクリーンが表示されない、またはで以下のテキストが表示されるこの場合、このクラッシュの完全な詳細情報は、デバッガーに送信され、デバッガー ウィンドウに表示されます。 詳細については、次を参照してください。[デバッガーを使用して](using-a-debugger.md)します。

バグ チェックのコードの場合は、このリファレンス セクションの一部として存在[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。 参照してください[バグ チェック コード参照](https://msdn.microsoft.com/library/windows/hardware/hh994433)のバグ チェックおよびパラメーターの説明。 各リファレンス ページには、バグ チェックのコード、文字列、および 4 つの追加のパラメーターに表示される各バグ チェックが一覧表示します。 バグ チェック、およびエラーを処理する方法を引き起こしたエラーを診断する方法も説明します。

バグの完全な一覧については、コードを確認、Bugcodes.h ファイルを参照してください。 このファイルは、Microsoft Windows Driver Kit (WDK) の inc ディレクトリで確認できます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[バグチェック コード リファレンス](https://msdn.microsoft.com/library/windows/hardware/hh994433)

[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)

 

 






