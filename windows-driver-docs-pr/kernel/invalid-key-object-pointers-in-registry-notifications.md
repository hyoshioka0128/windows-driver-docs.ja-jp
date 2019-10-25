---
title: レジストリ通知内の無効なキー オブジェクト ポインター
description: レジストリ通知内の無効なキー オブジェクト ポインター
ms.assetid: 96709c34-63a7-4b4e-8588-c7e8b41b5dea
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e27951dd07df2182492e3e72ff922367df229d74
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828164"
---
# <a name="invalid-key-object-pointers-in-registry-notifications"></a>レジストリ通知内の無効なキー オブジェクト ポインター


致命的なエラーやメモリ破損の可能性を回避するために、レジストリフィルタリングドライバーは、無効なオブジェクトポインターを使用してキーオブジェクトにアクセスしようとすることはできません。 このトピックでは、レジストリコールバックの通知構造体の**オブジェクト**メンバーに、未定義の**NULL**でない値が含まれている可能性がある状況を示します。

レジストリフィルタリングドライバーでは、 [*Registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンの2番目のパラメーターは、 [**REG\_NOTIFY\_CLASS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_reg_notify_class)列挙値です。 この値は、 *registrycallback*ルーチンの3番目のパラメーターが指しているレジストリコールバック通知構造の種類を示します。 通知構造体には、レジストリ操作に関する情報が含まれます。 この構造体の型は、実行されているレジストリ操作によって異なります。

多くの通知構造体の型には、キーオブジェクトを指す**オブジェクト**メンバーが含まれています。 場合によっては、**オブジェクト**メンバーに**NULL**以外の値を含めることができますが、有効なキーオブジェクトへのポインターではありません。

### <a name="key-object-value-is-undefined"></a>キーオブジェクトの値が定義されていません

レジストリフィルタードライバーの*Registrycallback*ルーチンの呼び出しの2番目のパラメーターが、 **REG\_NOTIFY\_CLASS**列挙値の**regntpostcreatekeyex**または**regntpostcreatekeyex**の場合、3番目のパラメーターになります。パラメーターは、 [**REG\_POST\_操作\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)構造体へのポインターです。 この構造体の**オブジェクト**メンバーは、構造体の**STATUS**メンバーが status\_SUCCESS に設定されている場合にのみ有効です。 **NT\_SUCCESS**マクロが**TRUE**と評価される0以外のステータスコードを含む、その他の**ステータス**値は、**オブジェクト**メンバーの値が未定義であることを示します。

### <a name="key-object-value-is-not-in-a-valid-state"></a>キーオブジェクトの値が有効な状態ではありません

レジストリコールバックの2番目のパラメーターが、次のいずれかの**REG\_通知\_クラス**列挙値の場合、レジストリコールバック通知構造の**オブジェクト**メンバーは、破棄されているキーオブジェクトを指します。参照カウントが0の場合:

-   **Regntprekeyhandleclose** ([**REG\_KEY\_ハンドル\_閉じ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_key_handle_close_information)構造)

-   **Regntpostkeyhandleclose** ([**REG\_POST\_操作\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)構造)

-   **Regntcallback Objectcontextcleanup** ([**REG\_コールバック\_コンテキスト\_クリーンアップ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_callback_context_cleanup_information)構造)

**オブジェクト**メンバーは、有効な状態ではないキーオブジェクトを指しているため、レジストリフィルタリングドライバーは、**オブジェクト**ポインター値をパラメーターとして[Windows ドライバーサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)に渡す必要があります (たとえば、 **ObReferenceObjectByPointer**)。

ただし、 [*Registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)呼び出しで**regntprekeyhandleclose**または**regntprekeyhandleclose**通知を処理するときに、レジストリフィルタドライバが[configuration manager ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すことができます (たとえば、 [**CmGetBoundTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetboundtransaction))。レジストリオブジェクトをパラメーターとして受け取ります。

 

 




