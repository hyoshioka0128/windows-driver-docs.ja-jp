---
title: オペレーティング システムがセーフ モードで実行されているかどうかの判断
description: オペレーティング システムがセーフ モードで実行されているかどうかの判断
ms.assetid: 5724a731-81a2-4c4e-a9e2-146859977e44
keywords:
- セーフ モードの WDK カーネル
- オペレーティング システムのセーフ モードの WDK カーネル
- InitSafeBootMode
- セーフ モードの WDK カーネルの防止
- セーフ モードの確認
- セーフ モードを確認しています
- セーフ モードの WDK カーネルの起動
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73420029be5b6649c4fd413888240137efbd167e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388169"
---
# <a name="determining-whether-the-operating-system-is-running-in-safe-mode"></a>オペレーティング システムがセーフ モードで実行されているかどうかの判断


このトピックでは、デバイス ドライバーを特定する方法で実行されているオペレーティング システムがセーフ モードで起動されたかどうかについて説明します。 このトピックでは、ドライバーがセーフ モードで動作しないようにする方法も説明します。

Microsoft Windows オペレーティング システムのカーネルがという名前のポインターをエクスポートします**InitSafeBootMode**します。 **InitSafeBootMode**現在有効になっているセーフ モードの設定を含む ULONG 変数を指しています。 デバイス ドライバーは、オペレーティング システムがセーフ モードで実行されているかどうかを判断するこれらの設定を確認できます。

次の表の値のモードの一覧、 **InitSafeBootMode**変数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>Mode</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>オペレーティング システムがセーフ モードではありません。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>SAFEBOOT_MINIMAL</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>SAFEBOOT_NETWORK</p></td>
</tr>
<tr class="even">
<td><p>3*</p></td>
<td><p>SAFEBOOT_DSREPAIR</p></td>
</tr>
</tbody>
</table>

 

**注**   \*値 3 は Windows ドメイン コント ローラーのみに適用されます。

 

使用する、 **InitSafeBootMode**変数、する必要がありますとして宣言する、ドライバーのコード例を次に示します。

```cpp
extern PULONG InitSafeBootMode;
```

宣言した後**InitSafeBootMode**、次のコード例を使用して、オペレーティング システムがセーフ モードで実行されているかどうかを判断することができます。

```cpp
if (*InitSafeBootMode > 0) {
    // The operating system is in Safe Mode.
    // Take appropriate action.
    //
}
```

ドライバーがセーフ モードで動作していることを防ぐためにドライバーの種類に一致する次の一覧で、この手法を使用します。

-   **関数のドライバー**

    関数には、ドライバー サービスの開始の種類のサービスがある場合\_ブート\_スタートの値をチェック**InitSafeBootMode** function ドライバーの*AddDevice*ルーチン。 システムがセーフ モードである場合は、エラー状態を返します。

    **注**  からエラーを返すことはありません必要があります、 **DriverEntry**ルーチン。

     

-   **フィルター ドライバー**

    フィルター ドライバーは、システムの起動時に起動する場合の値を確認してください。 **InitSafeBootMode**フィルター ドライバーの*AddDevice*ルーチン。 オペレーティング システムがセーフ モードである場合は、次の操作を行います。

    1.  デバイス スタックには、フィルター デバイス オブジェクトをアタッチできません。
    2.  フィルター ドライバーの成功を返す*AddDevice*ルーチン。
-   **その他のドライバー**

    関数またはフィルター ドライバー以外のドライバーの値をチェック**InitSafeBootMode**ドライバーの**DriverEntry**ルーチン。 オペレーティング システムがセーフ モードである場合は、エラー状態を返します。

 

 




