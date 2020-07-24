---
title: ファイルシステムでのセキュリティチェック
description: セキュリティの検査
ms.assetid: 2883910a-72f3-4be9-b1dd-6fb02abffe73
keywords:
- セキュリティ WDK ファイルシステム、セキュリティチェック
- セキュリティチェック WDK ファイルシステム
- セキュリティチェック WDK ファイルシステム、セキュリティチェックについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187a4fe0515a39d813272bdbd5459189912a3c12
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949746"
---
# <a name="security-checks-in-file-systems"></a>ファイルシステムでのセキュリティチェック

ファイルシステムのセキュリティに関しての責任は、セキュリティチェックの領域にあります。 これらは、実際にオブジェクトを "所有" する Windows の一部であるため、ファイルシステム内に実装されます。 セキュリティを実装する目的は、オブジェクトを保護するために (ファイルシステムによって実装される) ポリシーと、アクセスを決定するための機構 (セキュリティ参照モニターによって実装される) を分離することです。

つまり、ファイルシステムの開発者は、ファイルシステムリソースへの正しいアクセスを検証するために、適切なタイミングでセキュリティ参照モニターを呼び出す必要があります。 ファイルシステムでは、セキュリティの参照の監視によってセキュリティの決定がどのように行われるかについて理解する必要はありません。 ここでは、ファイルシステムがセキュリティチェックの追加を検討する可能性がある点について説明します。

ここでは、次のトピックについて説明します。

[デバイス オブジェクトに対するセキュリティ記述子の摘要](applying-security-descriptors-on-the-device-object.md)

[IRP_MJ_CREATE のセキュリティチェック](irp-mj-create-dispatch-routine.md)

[IRP_MJ_QUERY_SECURITY と IRP_MJ_SET_SECURITY のセキュリティチェック](irp-mj-query-security-and-irp-mj-set-security.md)

[IRP_MJ_DIRECTORY_CONTROL のセキュリティチェック](irp-mj-directory-control2.md)

[IRP_MJ_FILE_SYSTEM_CONTROL のセキュリティチェック](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)

[IRP_MJ_SET_INFORMATION のセキュリティチェック](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information)

[権限借用](impersonation.md)

[処理とスレッド終了に関する問題](process-and-thread-termination-issues.md)
