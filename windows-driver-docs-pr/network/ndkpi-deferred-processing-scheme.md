---
title: NDKPI 遅延処理スキーム
description: このセクションでは、NDKPI で使用される遅延処理について説明します。
ms.assetid: DA2D0FCA-D84B-4599-A560-8F87A0918D99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 117a5a871fd87a5eb686a11c487fc5e80f8d01c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831902"
---
# <a name="ndkpi-deferred-processing-scheme"></a>NDKPI 遅延処理スキーム


NDK コンシューマーは多くの場合、イニシエーター要求のチェーンをキューペア (QP) に送信します。 たとえば、コンシューマーは、多数の高速レジスタ要求の後に送信要求をポストできます。 このような要求パターンのパフォーマンスは、要求のチェーンが QP のキューに登録され、ハードウェアに対して各要求を1つずつ示すのではなく、バッチとして処理するためにハードウェアに指示されると改善される可能性があります。

**NDK\_OP\_フラグ\_DEFER**フラグ値は、次の要求の種類を使用してこの目的に使用できます。

-   *Ndkbind* ([*NDK\_FN\_BIND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind))
-   *Ndkfastregister* ([*NDK\_FN\_FAST\_REGISTER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_fast_register))
-   *NdkInvalidate* ([*NDK\_FN\_無効化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate))
-   *Ndkread* ([*NDK\_FN\_読み取り*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_read))
-   *Ndksend* ([*NDK\_FN\_SEND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send))
-   *Ndksendandinvalidate* ([*NDK\_FN\_SEND\_および\_無効化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate))
-   *Ndkwrite* ([*NDK\_FN\_書き込み*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_write))

フラグが存在するかどうかは、ハードウェアへの要求を処理するように要求することを示す、NDK プロバイダーに対するヒントですが、プロバイダーはいつでも新しい要求を処理できます。

**Ndk\_OP\_フラグ\_遅延**フラグが設定されている場合、発信側の要求に対して、ndk プロバイダーの既存の役割は変更されません。 エラー状態を返す発信側要求への呼び出しでは、失敗した要求に対して CQ のキューに登録が完了しないようにする必要があります。 逆に、成功の状態を返す呼び出しでは、コンシューマーが以下に示す追加の要件に従う限り、最終的には CQ のキューに登録されます。

すべての既存の NDK 要件に加えて、 **ndk\_OP\_フラグを使用して要求が QP に正常に送信される状況を防ぐために、2つの追加要件 (プロバイダー用とコンシューマー用に1つ) を監視する必要があり\_DEFER**フラグは、ハードウェアに対して処理のために指定されることはありません。

-   発信側要求の呼び出しからエラー状態を返す場合、プロバイダーは、以前に**NDK\_OP\_フラグ\_DEFER**フラグを使用して送信されたすべての要求がハードウェアに処理のために示されていることを保証する必要があります。
-   コンシューマーは、インラインエラーがない場合に、すべてのイニシエーター要求チェーンが、 **NDK\_OP\_フラグ\_DEFER**フラグを設定していないイニシエーター要求によって終了されることを保証します。

たとえば、コンシューマーに2つの高速レジスタ要求のチェーンと、QP に post する必要がある送信がある場合を考えてみます。

1.  コンシューマーは、 **NDK\_OP\_フラグ\_DEFER**フラグと*NDKFASTREGISTER*が成功を返すステータス\_を使用して、ファーストレジスタをポストします。
2.  ここでも、2番目の高速レジスタは、 **NDK\_OP\_フラグ\_DEFER**フラグが設定された状態で投稿されますが、 *ndkfastregister*はエラー状態を返します。 この場合、コンシューマーは送信要求を送信しません。
3.  *Ndkfastregister*への2回目の呼び出しでインラインエラーが返されると、NDK プロバイダーは、以前に示されていないすべての要求 (この場合は最初の高速レジスタ) がハードウェアに対して処理のために示されることを確認します。
4.  *Ndkfastregister*の最初の呼び出しが成功したため、CQ に対して完了を生成する必要があります。
5.  *Ndkfastregister*への2回目の呼び出しはインラインで失敗したため、CQ に対して完了を生成することはできません。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






