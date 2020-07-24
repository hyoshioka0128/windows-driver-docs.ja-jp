---
title: ファイルシステムでの特権の管理
description: ファイルシステムで権限を管理する方法について説明します。
ms.assetid: a8df1a44-6fb7-4c16-a29d-785d06dd50e4
keywords:
- セキュリティ WDK ファイルシステム、特権
- 権限 WDK ファイルシステム
- 操作特権 WDK ファイルシステム
- SeBackupPrivilege
- SeRestorePrivilege
- SeChangeNotifyPrivilege
- SeManageVolumePrivilege
- ボリュームレベルの管理特権 WDK ファイルシステム
- 右の特権のスキャン WDK ファイルシステム
- バックアップ特権 WDK ファイルシステム
- 復元権限 WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21545cee9473a234b3c998460d28bc4dce5e2417
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949730"
---
# <a name="managing-privileges-in-a-file-system"></a>ファイルシステムでの特権の管理

特権は、特定の操作を制御するためにオペレーティングシステムによって使用される完全に独立したメカニズムです。 各特権は、呼び出し元によって特権が保持され、有効になった場合に実行される可能性のある特定の操作に関連付けられています。 ここでは、次の2つの条件に注意してください。

- 特権は、呼び出し元によって保持されている必要があります。

- 特権も有効にする必要があります。

ここでは、最小限の特権と呼ばれる原則で、意図していなかった操作をユーザーが意図せずに実行する可能性を最小限に抑えるために、単に想定するのではなく、使用する前に特権を有効にする必要があります。 たとえば、 **Serestoreprivilege**は通常、ファイルへの書き込みアクセスの通常のチェックを呼び出し元がバイパスできるようにします。 管理者は、ファイルをコピーするときに通常のセキュリティチェックを無効にしたくない場合がありますが、バックアップ/復元ユーティリティを使用して同じファイルを復元する場合には、この操作を行うことをお勧めします。

ファイルシステムの場合、システムの通常の動作 (特にセキュリティチェック) を変更するためによく使用される特権が多数あります。 これらの特権は次のとおりです。

- **Sebackupprivilege**は、ファイルのセキュリティ記述子がこのようなアクセスを許可しない場合でも、ファイルコンテンツの取得を許可します。 **Sebackupprivilege**が有効になっている呼び出し元は、ACL ベースのセキュリティチェックをなくなり必要があります。

- **Serestoreprivilege**では、ファイルのセキュリティ記述子によってアクセスが許可されない場合でも、ファイルの内容を変更できます。 この関数を使用して、所有者と保護を変更することもできます。

- **SeChangeNotifyPrivilege**では、走査権限を許可します。 パス内のすべてのディレクトリに対してセキュリティチェックを実行する場合のコストは、この特権を保持することによって除外されるため、この特権は Windows での重要な最適化です。

- **SeManageVolumePrivilege**を使用すると、ボリュームレベルの管理操作 (ボリュームのロック、デフラグ、ボリュームのマウント解除、Windows XP 以降での有効なデータの長さの設定など) を行うことができます。 この特定の特権は、主に FSCTL 操作に基づいてファイルシステムドライバーによって明示的に適用されることに注意してください。 この場合、ファイルシステムによって、この特権を適用するポリシーが決定されます。 この特権が呼び出し元によって保持されるかどうかは、通常の特権チェックの一部として、セキュリティ参照モニターによって決定されます。

他にも多くの特権がありますが、通常はファイルシステムに対して非透過的であるため、セキュリティ参照モニタによってのみ解釈されます。

ファイルシステム内の特権を管理するための主要な Windows ルーチンは次のとおりです。

- [**SePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seprivilegecheck)--このルーチンは、必要な特権の特定のセットのチェックを実行します。

- [**SeSinglePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-sesingleprivilegecheck)--このルーチンは、1つの特定の特権のチェックを実行します。これは、 [**SePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seprivilegecheck)の最適化されたバージョンです。

- [**Seaccesscheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)--このルーチンは、オブジェクト (通常はファイルシステムのファイルオブジェクト) に対する通常のアクセスチェックを実行します。

- [**Sefreeprivileges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sefreeprivileges)--このルーチンは、 [**seaccesscheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)の前の呼び出しで返された特権ブロックを解放します。

- [**Seappendprivileges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seappendprivileges)--このルーチンは、有効な特権を ACCESS_STATE 構造に追加します。 通常、ファイルシステムは、IRP_MJ_CREATE 処理中に渡された ACCESS_STATE を使用します。
