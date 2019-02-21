---
title: 権限
description: 権限
ms.assetid: a8df1a44-6fb7-4c16-a29d-785d06dd50e4
keywords:
- セキュリティ WDK ファイル システム権限
- WDK のファイル システム権限
- 操作の WDK ファイル システムを権限します。
- SeBackupPrivilege
- SeRestorePrivilege
- SeChangeNotifyPrivilege
- SeManageVolumePrivilege
- ボリューム レベルの管理特権を WDK ファイル システム
- 適切な権限 WDK ファイル システムをスキャンします。
- バックアップ特権 WDK ファイル システム
- 特権 WDK ファイル システムを復元します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e39a8149f75a1de93d7f05854961196d9a87baa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549677"
---
# <a name="privileges"></a>権限


## <span id="ddk_privileges_if"></span><span id="DDK_PRIVILEGES_IF"></span>


特権は、特定の操作を制御する、オペレーティング システムによって使用される完全に別のメカニズムです。 各特権がそれに関連付けられている特定の操作、特権が保持され、呼び出し元が有効になっている場合に実行することがあります。 ここで、2 つの条件に注意してください。

-   特権は、呼び出し元によって保持されている必要があります。

-   特権も有効にする必要があります。

ここでの原則、最小限の特権と呼ばれること特権が、利用する前に有効になっているではなく、ユーザーが誤って意図しない操作を実行する場合があります可能性を最小限に抑えるためには、単に想定が必要です。 たとえば、 **SeRestorePrivilege**は通常は、ファイルへの書き込みアクセス用の通常のチェックをバイパスする呼び出し元を許可します。 管理者を実際には、ファイルをコピーするときに、通常のセキュリティ チェックをオーバーライドすることがありますしないはそのため、バックアップ/復元ユーティリティを使用して同じファイルを復元するときにするには。

ファイル システムでは、数を多くの場合、使用、システムの通常の動作 (特に、セキュリティ チェック) を変更する権限があります。 これらの権限は次のとおりです。

-   **SeBackupPrivilege**-ファイルのセキュリティ記述子は、このようなアクセスを許可しない場合がある場合でも、ファイル コンテンツの取得を許可します。 呼び出し元に**SeBackupPrivilege**有効になっているすべての ACL ベースのセキュリティ チェックの必要性がなくなります。

-   **SeRestorePrivilege**-ファイルのセキュリティ記述子は、このようなアクセスを許可しない場合がある場合でも、ファイル コンテンツの変更を許可します。 この関数は、所有者と保護を変更することも使用できます。

-   **SeChangeNotifyPrivilege**--走査権利を許可します。 この特権は、Windows での重要な最適化がパスに 1 つのすべてのディレクトリのセキュリティ チェックを実行するコストがこの特権を保持しているによって除外。

-   **SeManageVolumePrivilege**--ボリュームのロック、最適化、ボリュームのマウント解除、および Windows XP 以降の有効なデータ長の設定などの特定のボリューム レベルの管理操作を許可します。 この特定の特権が FSCTL 操作に基づいて、主に、ファイル システム ドライバーによって明示的に適用されるに注意してください。 この場合、ファイル システムでは、この権限を適用するポリシー決定を行います。 この権限が呼び出し元によって保持されているかどうかの決定、通常の権限チェックの一部としてセキュリティ参照モニター。

その他の多数の特権はありますが、通常、ファイル システムに不透明なされており、セキュリティ参照モニターでのみ解釈されるため。

ファイル システム内の特権を管理するためのキーの Windows ルーチンは次のとおりです。

-   [**SePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff556686)--このルーチンは、特定の必要な権限のセットに対してチェックを実行します。

-   [**SeSinglePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563740)--このルーチンは、1 つの特定の権限のチェックを実行します。 は、最適化されたバージョンの[ **SePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff556686)します。

-   [**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)--このルーチンは通常のアクセス オブジェクト (通常、ファイル システムのファイル オブジェクト) のチェックを実行します。

-   [**SeFreePrivileges**](https://msdn.microsoft.com/library/windows/hardware/ff556656)--このルーチンは、以前の呼び出しによって返される特権ブロックを解放[ **SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)します。

-   [**SeAppendPrivileges**](https://msdn.microsoft.com/library/windows/hardware/ff554762)--このルーチンは、アクセスに有効な権限を追加します。\_状態構造体。 通常、ファイル システムは、アクセスを使用して\_IRP 中に渡される状態\_MJ\_作成処理します。

 

 




