---
title: レジストリ通知内のキー オブジェクトが無効なポインター
description: レジストリ通知内のキー オブジェクトが無効なポインター
ms.assetid: 96709c34-63a7-4b4e-8588-c7e8b41b5dea
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3ad92e0663df7dc22756e05fea0c29d2a1c425e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535905"
---
# <a name="invalid-key-object-pointers-in-registry-notifications"></a>レジストリ通知内のキー オブジェクトが無効なポインター


致命的なエラーやメモリ破損の可能性を避けるため、無効なオブジェクト ポインターを使用して、キー オブジェクトへのアクセスにレジストリのフィルター ドライバーしないでください。 このトピックでは、状況、**オブジェクト**レジストリ コールバック通知構造体のメンバーを含む可能性があります、未定義以外**NULL**値。

ドライバーの 2 番目のパラメーターをフィルター処理、レジストリで、 [ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)ルーチンは、 [ **REG\_通知\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560950)列挙値。 この値は、構造体の 3 番目のパラメーターをレジストリ コールバック通知の種類を示します、 *RegistryCallback*ルーチンをポイントします。 通知の構造体には、レジストリの操作に関する情報が含まれています。 この構造体の型は、実行されているレジストリ操作によって異なります。

多くの通知の種類の構造を含む、**オブジェクト**キー オブジェクトを指すメンバー。 場合によってで、**オブジェクト**メンバー以外の値を含めることができます**NULL**が有効なキー オブジェクトへのポインターではありません。

### <a name="key-object-value-is-undefined"></a>キー オブジェクトの値は未定義

場合の呼び出しでは、2 番目のパラメーター、 *RegistryCallback*フィルター ドライバーのレジストリのルーチンは、 **REG\_通知\_クラス**列挙値の**RegNtPostCreateKeyEx**または**RegNtPostOpenKeyEx**、3 番目のパラメーターはへのポインターを[ **REG\_POST\_操作\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560971)構造体。 **オブジェクト**この構造体のメンバーは有効な場合にのみ、**状態**構造体のメンバーの状態に設定されます\_成功します。 その他の**状態**を 0 以外のステータス コードを含め、値、 **NT\_成功**に評価されるマクロ**TRUE**、ことを示します、の値**オブジェクト**メンバーは定義されていません。

### <a name="key-object-value-is-not-in-a-valid-state"></a>キー オブジェクトの値が有効な状態にありません。

レジストリのコールバックでは、2 番目のパラメーターは、次のいずれかのかどうかは**REG\_通知\_クラス**列挙の値、**オブジェクト**レジストリ コールバック通知のメンバー構造体は、キー オブジェクトが破棄されると、参照カウントがゼロにポイントします。

-   **RegNtPreKeyHandleClose** ([**REG\_キー\_処理\_閉じる\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560943)構造)

-   **RegNtPostKeyHandleClose** ([**REG\_POST\_操作\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560971)構造)

-   **RegNtCallbackObjectContextCleanup** ([**REG\_コールバック\_コンテキスト\_クリーンアップ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560919)構造)

**オブジェクト**ドライバーをフィルター処理、レジストリ、有効な状態でないキー オブジェクトへのポインターをメンバーに渡す必要がありますいない、**オブジェクト**ポインター値をパラメーターとして、 [Windows ドライバールーチンをサポートして](https://msdn.microsoft.com/library/windows/hardware/ff558686)(たとえば、 **ObReferenceObjectByPointer**)。

ただし、中に、 [ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)処理への呼び出しを**RegNtPreKeyHandleClose**または**RegNtPostKeyHandleClose**通知では、レジストリのフィルター ドライバーを呼び出すことができます、 [configuration manager のルーチン](https://msdn.microsoft.com/library/windows/hardware/ff542038)(たとえば、 [ **CmGetBoundTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff541905)) を受け取ると、レジストリ オブジェクトとして、パラメーター。

 

 




