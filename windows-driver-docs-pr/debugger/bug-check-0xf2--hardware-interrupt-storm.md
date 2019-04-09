---
title: Bug Check 0xF2 HARDWARE_INTERRUPT_STORM
description: HARDWARE_INTERRUPT_STORM のバグ チェックでは、0x000000F2 の値を持ちます。 これは、カーネルに大量の割り込みが検出されたことを示します。
ms.assetid: 04751AB2-E9B3-40AD-A872-8DDA9B96C6CA
keywords:
- Bug Check 0xF2 HARDWARE_INTERRUPT_STORM
- HARDWARE_INTERRUPT_STORM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HARDWARE_INTERRUPT_STORM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a77b400140811f6470c8b734dbd0ecff01f779ed
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239509"
---
# <a name="bug-check-0xf2-hardwareinterruptstorm"></a>バグ チェック 0xF2:ハードウェア\_INTERRUPT\_STORM


ハードウェア\_INTERRUPT\_STORM バグ チェックが 0x000000F2 の値を持ちます。 これは、カーネルに大量の割り込みが検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="hardwareinterruptstorm-parameters"></a>ハードウェア\_INTERRUPT\_STORM パラメーター


| パラメーター | 説明                                                                               |
|-----------|-------------------------------------------------------------------------------------------|
| 1         | ストームの割り込みのベクターに接続されている ISR (または、チェーンの最初の ISR) のアドレス |
| 2         | ISR コンテキストの値                                                                         |
| 3         | ストームの割り込みのベクターの割り込みのオブジェクトのアドレス                         |
| 4         | 0x1 の場合は、ISR がチェーンされている、0x2 ISR がチェーンされている場合                                  |

 

<a name="cause"></a>原因
-----

このバグチェックでは、カーネルによって、大量の割り込みが検出されたことを示します。 大量の割り込みは、状態は、常にレベルのトリガーされた割り込みシグナルとして定義されます。 これは、システムは、ハードの方法でシステムに致命的なハング、または「bus ロック」。

これは、次の理由により発生することができます。

-   ハードウェア デバイス ドライバーによって指示される後に、割り込みシグナルを解放しません。
-   デバイス ドライバーには考えません割り込みがそのハードウェアから開始されたため、割り込みシグナルを解放するには、そのハードウェアはされません。
-   デバイス ドライバーは、ハードウェアから割り込みが開始しない場合でも、割り込みを要求します。 複数のデバイスが同じ IRQ を共有するときに発生のみに注意してください。
-   ELCR (edge のレベルの制御の登録) が正しく設定されていません。
-   エッジおよび割り込みのレベルには、デバイス共有 IRQ がトリガーされます。

これらすべてのケースでは、システム ハードすぐにハングします。 代わりに、システムがハングするハードこのバグチェックが開始されますので、多くの場合、原因を特定することができます。

バグチェックが発生すると、画面上のストーム IRQ ISR (割り込みサービス ルーチン) を含むモジュールが表示されます。 これは、表示される内容の例を示します。

```console
*** STOP: 0x000000F2 (0xFCA7C55C, 0x817B9B28, 0x817D2AA0, 0x00000002)
An interrupt storm has caused the system to hang.
*** Address FCA7C55C base at FCA72000, Datestamp 3A72BDEF - ACPI.sys
```

4 番目のパラメーターは、0x00000001、イベントの指すモジュールがおそらく原因です。 ドライバーが壊れている、またはハードウェアの故障のいずれか。

イベント 4 番目のパラメーターには、0x00000002 が指すモジュールは、チェーンの最初の ISR は、し、原因があることが保証されません。

<a name="resolution"></a>解決方法
----------

繰り返しこのバグチェックが発生しているユーザーは必要があります、モジュールは、ドライバーは、(この例では、ACPI を使用している同じ IRQ) での 1 つとして同じ IRQ 上にあるデバイスを探すことによって、問題の分離しようとしています。

 

 




