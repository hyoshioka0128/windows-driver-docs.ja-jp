---
title: セキュリティ チェック
description: セキュリティ チェック
ms.assetid: 2883910a-72f3-4be9-b1dd-6fb02abffe73
keywords:
- セキュリティの WDK ファイル システム、セキュリティ チェック
- セキュリティは、WDK のファイル システムを確認します。
- セキュリティに関するセキュリティ チェックの WDK ファイル システムを確認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fe72a499e4938a4a969eeae2071bd6bed9e519d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560736"
---
# <a name="security-checks"></a>セキュリティ チェック


## <span id="ddk_security_checks_if"></span><span id="DDK_SECURITY_CHECKS_IF"></span>


セキュリティに関して、ファイル システムの役割の大部分は、セキュリティ チェックの領域には。 これらは、実際にオブジェクトを「所有」する Windows の一部であるために、ファイル システム内で実装されます。 セキュリティの実装の目標は、そのオブジェクトでは、およびアクセス決定を行うためのメカニズム (セキュリティ参照モニターによって実装される) を保護するため (ファイル システムで実装) ポリシーを分離します。

つまり、ファイル システムの開発者は、ファイル システム リソースに適切なアクセスを検証する適切なタイミングでセキュリティ参照モニターへの呼び出しを行う責任を負います。 ファイル システムでは、セキュリティ参照モニターがこれらのセキュリティ上の決定を使用する方法の詳細を理解する必要がありますされません。 このセクションでは、ファイル システムがセキュリティ チェックを追加することを考慮がポイントについて説明します。

ここでは、次のトピックについて説明します。

[デバイス オブジェクトのセキュリティ記述子を適用します。](applying-security-descriptors-on-the-device-object.md)

[IRP\_MJ\_CREATE](irp-mj-create-dispatch-routine.md)

[IRP\_MJ\_クエリ\_セキュリティと IRP\_MJ\_設定\_セキュリティ](irp-mj-query-security-and-irp-mj-set-security.md)

[IRP\_MJ\_ディレクトリ\_コントロール](irp-mj-directory-control2.md)

[IRP\_MJ\_ファイル\_システム\_コントロール](https://msdn.microsoft.com/library/windows/hardware/ff548670)

[IRP\_MJ\_SET\_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff549366)

[権限借用](impersonation.md)

[プロセスおよびスレッドの終了に関する問題](process-and-thread-termination-issues.md)

 

 




