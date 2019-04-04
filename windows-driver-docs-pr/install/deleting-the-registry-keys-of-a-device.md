---
title: デバイスのレジストリ キーの削除
description: デバイスのレジストリ キーの削除
ms.assetid: BA7AB3B4-9751-4e53-98AD-2B920F7223A1
keywords:
- レジストリ WDK デバイスのインストール、デバイスのレジストリ キーの削除
- レジストリ キーの WDK デバイスのインストールを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ef9e28fc56f907915eb6f88b8bebf6057b7bbb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529295"
---
# <a name="deleting-the-registry-keys-of-a-device"></a>デバイスのレジストリ キーの削除


使用しないようにする**SetupDiDeleteDevRegKey**または*ハードウェア キー*理由は次のデバイス。

-   [**SetupDiDeleteDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550991)レジストリ キー内のすべてのカスタム設定を削除します。 これには、次のデータが含まれます。

    -   インストール時に指定された設定。

    -   作成またはデバイス ドライバーによって変更された設定。

    -   作成されたアプリケーションまたはその他のコンポーネントによって変更する設定。

    [**SetupDiDeleteDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550991)不可欠なデバイス インストール状態も削除します。

-   ソフトウェアまたはハードウェアのキーを使用して開かれた[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079) DICS_FLAG_GLOBAL のスコープを持つデバイスのインストール状態に関するデータが含まれています。 DICS_FLAG_CONFIGSPECIFIC のスコープでアクセスされるソフトウェアまたはハードウェアのキーでは、デバイスのインストール状態は含まれません。

    いずれの場合も、これらのソフトウェアまたはハードウェア キーを削除するその他のデバイス インストールのコンポーネントに影響を及ぼすことができます。

デバイス レジストリ キーが存在するかどうかについて想定しないようにします。 デバイスがアンインストールされると、システムで、デバイスのすべてのソフトウェアとハードウェア キーが自動的に削除されます。

安全を作成し、標準レジストリ関数を使用して、ハードウェアまたはソフトウェア キーの下のレジストリ サブキーを削除することができます。 これらの関数を使用すると、名前のシステムとその他のコンポーネント間の競合を回避します。 また、これらの関数を使用してサブキーを作成する場合、サブキーは、親のレジストリ キーの既定のアクセス許可を継承します。 詳細については、[オープン、作成、および終了キー](https://go.microsoft.com/fwlink/p/?linkid=194541)を参照してください。

詳細については、標準レジストリ関数は、[レジストリ関数](https://go.microsoft.com/fwlink/p/?linkid=194529)を参照してください。

 

 





