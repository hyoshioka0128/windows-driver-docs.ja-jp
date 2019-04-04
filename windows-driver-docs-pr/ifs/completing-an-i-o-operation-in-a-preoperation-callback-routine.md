---
title: Preoperation コールバック ルーチン内の I/O 操作の完了
description: Preoperation コールバック ルーチン内の I/O 操作の完了
ms.assetid: 1f339779-dc88-4673-87d5-36cee0b27fc2
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、I/O 操作の完了
- WDK のファイル システムを要求する I/O の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0265d13001fa251b3a5ac769b5d1f25b8b7fa631
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530147"
---
# <a name="completing-an-io-operation-in-a-preoperation-callback-routine"></a>Preoperation コールバック ルーチン内の I/O 操作の完了


## <span id="ddk_completing_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_COMPLETING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


*完了*I/O 操作が操作の処理を停止、最後の NTSTATUS 値を割り当てます、フィルター マネージャーに戻すことを示します。

ミニフィルター ドライバーには、I/O 操作が完了すると、フィルター マネージャーは、次を行います。

-   以下の現在のミニフィルター ドライバー ミニフィルター ドライバー、レガシ フィルター、またはファイル システム操作を送信しません。

-   呼び出し、 [ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)ミニフィルター ドライバーのインスタンスのスタックでは、現在のミニフィルター ドライバー上ミニフィルター ドライバー。

-   存在する場合の操作で、現在のミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出しません。

ミニフィルター ドライバーの[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)次の手順を実行することによって、I/O 操作が完了するとします。

1.  コールバックのデータ構造体の設定**IoStatus.Status**フィールドの操作の最終的な NTSTATUS 値にします。

2.  返す FLT\_PREOP\_完了します。

I/O 操作を完了する preoperation コールバック ルーチンは、NULL 以外の入力候補のコンテキストを設定できません (で、 *CompletionContext*出力パラメーター)。

ミニフィルター ドライバーできますの作業ルーチン内の操作を完了しても、次の手順を実行することで I/O の保留操作以前。

1.  コールバックのデータ構造体の設定**IoStatus.Status**フィールドの操作の最終的な NTSTATUS 値にします。

2.  FLT を渡す\_PREOP\_で完了、 *CallbackStatus*作業ルーチンを呼び出すときにパラメーター [ **FltCompletePendedPreOperation**](https://msdn.microsoft.com/library/windows/hardware/ff541913)します。

ミニフィルター ドライバーがコールバックのデータ構造体を設定する必要があります、I/O 操作を完了したときに**IoStatus.Status** 、操作の最終的な NTSTATUS 値がこの NTSTATUS 値のフィールドが状態にすることはできません\_PENDING またはステータス\_FLT\_DISALLOW\_高速\_IO。 フィールド、クリーンアップまたは閉じる操作の状態でなければなりません\_成功します。 その他の NTSTATUS 値では、これらの操作を完了できません。

I/O 操作の完了は、成功または失敗した NTSTATUS 値に応じて、操作と呼ばれるに多くの場合。

-   *成功*、I/O 操作が成功または状態などの情報の NTSTATUS 値を使用することを意味\_成功します。

-   *失敗*、I/O 操作の状態など、エラーまたは警告 NTSTATUS 値で完了することを意味\_無効な\_デバイス\_要求または状態\_バッファー\_オーバーフローしました。

NTSTATUS の値は ntstatus.h に定義されます。 これらの値は 4 つのカテゴリに分類されます。 成功すると、情報、警告、およびエラー。 これらの値の詳細については、[NTSTATUS 値を使用して](https://msdn.microsoft.com/library/windows/hardware/ff565436)を参照してください。

 

 




