---
title: 遅延処理の NDKPI スキーム
description: このセクションには、NDKPI で使用される処理の遅延がについて説明します
ms.assetid: DA2D0FCA-D84B-4599-A560-8F87A0918D99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49365eafcb7d8b27aa033d67150e02c0242d2acf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353744"
---
# <a name="ndkpi-deferred-processing-scheme"></a>NDKPI 遅延処理スキーム


多くの場合、NDK コンシューマー キュー ペア (QP) にイニシエーターの要求のチェーンを投稿できる場所があります。 たとえば、コンシューマーは、後、送信要求の高速の登録要求数を投稿するでした。 このような要求パターンのパフォーマンスは、要求のチェーンが QP をキューに置かれた場合を改善され、ハードウェアをチェーン内の要求ごとに 1 つずつを示すのではなく、バッチとして処理用のハードウェアに示されている可能性があります。

**NDK\_OP\_フラグ\_DEFER**フラグの値は次の要求の種類では、この目的に使用できます。

-   *NdkBind* ([*NDK\_FN\_BIND*](https://msdn.microsoft.com/library/windows/hardware/hh439859))
-   *NdkFastRegister* ([*NDK\_FN\_FAST\_REGISTER*](https://msdn.microsoft.com/library/windows/hardware/hh439887))
-   *NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/hh439901))
-   *NdkRead* ([*NDK\_FN\_READ*](https://msdn.microsoft.com/library/windows/hardware/hh439906))
-   *NdkSend* ([*NDK\_FN\_SEND*](https://msdn.microsoft.com/library/windows/hardware/hh439914))
-   *NdkSendAndInvalidate* ([*NDK\_FN\_SEND\_AND\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/dn265507))
-   *NdkWrite* ([*NDK\_FN\_WRITE*](https://msdn.microsoft.com/library/windows/hardware/hh439917))

フラグのプレゼンスは、プロバイダーは、いつでも新しい要求を処理することがありますが、処理のためのハードウェアに要求を示すを遅らせることができますが、NDK プロバイダーへのヒントです。

有無、 **NDK\_OP\_フラグ\_DEFER**イニシエーターの要求でフラグには、入力候補の生成に関して、NDK プロバイダーの既存の責任は変わりません。 エラー状態を返すイニシエーター要求への呼び出しはする必要があります、失敗した要求の CQ をキューに登録される完了されることはありません。 逆に、成功状態を返す呼び出しとして、コンシューマーは、以下に示す追加の要件を次に、CQ をキューに登録される入力候補で最終的になる必要があります。

既存 NDK 要件をすべてに加えて追加の 2 つの要件 (プロバイダーの 1 つ) と、コンシューマーの 1 つを要求を正常にで QP にポストする状況を防ぐために従う必要があります、 **NDK\_OP\_フラグ\_DEFER**フラグが設定が、決して処理のためのハードウェアに示されます。

-   すべての要求で送信された以前ですが、プロバイダーを保証する必要があります、イニシエーターの要求への呼び出しからエラー状態を返すときに、 **NDK\_OP\_フラグ\_DEFER**フラグには処理のためのハードウェアに示されます。
-   コンシューマーは、インライン エラーのない場合は、すべてのイニシエーター要求チェーンによって終了されます、イニシエーターの要求が設定されていないことを保証、 **NDK\_OP\_フラグ\_DEFER**フラグ。

たとえば、コンシューマーが 2 つの高速の登録要求と QP に投稿する必要がある送信のチェーンを持つケースを考えてみます。

1.  コンシューマーで最初の高速レジスタの投稿、 **NDK\_OP\_フラグ\_DEFER**フラグと*NdkFastRegister*ステータスを返します\_成功します。
2.  含む、2 つ目の高速なレジスタが投稿された、もう一度、 **NDK\_OP\_フラグ\_DEFER**フラグの設定が*NdkFastRegister*エラー状態を返します。 この場合、コンシューマーは、送信要求を通知できません。
3.  2 番目の呼び出しのインライン エラーを返すときに*NdkFastRegister*、NDK プロバイダーは、すべて以前 unindicated (最初の高速をここで登録) 要求が処理するためのハードウェアに示されることを確認します。
4.  最初の呼び出しのため*NdkFastRegister*に成功したが完了する必要がありますが生成されること、CQ します。
5.  2 番目の呼び出しをするため、 *NdkFastRegister*インラインで失敗しました、完了する必要があります、CQ を生成できません。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






