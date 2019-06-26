---
title: レジストリ通知内の無効なキー オブジェクト ポインター
description: レジストリ通知内の無効なキー オブジェクト ポインター
ms.assetid: 96709c34-63a7-4b4e-8588-c7e8b41b5dea
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7598a0837c6666f8422e3779cbeefa2d737cdd01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381695"
---
# <a name="invalid-key-object-pointers-in-registry-notifications"></a>レジストリ通知内の無効なキー オブジェクト ポインター


致命的なエラーやメモリ破損の可能性を避けるため、無効なオブジェクト ポインターを使用して、キー オブジェクトへのアクセスにレジストリのフィルター ドライバーしないでください。 このトピックでは、状況、**オブジェクト**レジストリ コールバック通知構造体のメンバーを含む可能性があります、未定義以外**NULL**値。

ドライバーの 2 番目のパラメーターをフィルター処理、レジストリで、 [ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)ルーチンは、 [ **REG\_通知\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_reg_notify_class)列挙値。 この値は、構造体の 3 番目のパラメーターをレジストリ コールバック通知の種類を示します、 *RegistryCallback*ルーチンをポイントします。 通知の構造体には、レジストリの操作に関する情報が含まれています。 この構造体の型は、実行されているレジストリ操作によって異なります。

多くの通知の種類の構造を含む、**オブジェクト**キー オブジェクトを指すメンバー。 場合によってで、**オブジェクト**メンバー以外の値を含めることができます**NULL**が有効なキー オブジェクトへのポインターではありません。

### <a name="key-object-value-is-undefined"></a>キー オブジェクトの値は未定義

場合の呼び出しでは、2 番目のパラメーター、 *RegistryCallback*フィルター ドライバーのレジストリのルーチンは、 **REG\_通知\_クラス**列挙値の**RegNtPostCreateKeyEx**または**RegNtPostOpenKeyEx**、3 番目のパラメーターはへのポインターを[ **REG\_POST\_操作\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_post_operation_information)構造体。 **オブジェクト**この構造体のメンバーは有効な場合にのみ、**状態**構造体のメンバーの状態に設定されます\_成功します。 その他の**状態**を 0 以外のステータス コードを含め、値、 **NT\_成功**に評価されるマクロ**TRUE**、ことを示します、の値**オブジェクト**メンバーは定義されていません。

### <a name="key-object-value-is-not-in-a-valid-state"></a>キー オブジェクトの値が有効な状態にありません。

レジストリのコールバックでは、2 番目のパラメーターは、次のいずれかのかどうかは**REG\_通知\_クラス**列挙の値、**オブジェクト**レジストリ コールバック通知のメンバー構造体は、キー オブジェクトが破棄されると、参照カウントがゼロにポイントします。

-   **RegNtPreKeyHandleClose** ([**REG\_キー\_処理\_閉じる\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_key_handle_close_information)構造)

-   **RegNtPostKeyHandleClose** ([**REG\_POST\_操作\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_post_operation_information)構造)

-   **RegNtCallbackObjectContextCleanup** ([**REG\_コールバック\_コンテキスト\_クリーンアップ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_callback_context_cleanup_information)構造)

**オブジェクト**ドライバーをフィルター処理、レジストリ、有効な状態でないキー オブジェクトへのポインターをメンバーに渡す必要がありますいない、**オブジェクト**ポインター値をパラメーターとして、 [Windows ドライバールーチンをサポートして](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)(たとえば、 **ObReferenceObjectByPointer**)。

ただし、中に、 [ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)処理への呼び出しを**RegNtPreKeyHandleClose**または**RegNtPostKeyHandleClose**通知では、レジストリのフィルター ドライバーを呼び出すことができます、 [configuration manager のルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)(たとえば、 [ **CmGetBoundTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmgetboundtransaction)) を受け取ると、レジストリ オブジェクトとして、パラメーター。

 

 




