---
title: IRP_MJ_CREATE ディスパッチ ルーチン
description: IRP_MJ_CREATE ディスパッチ ルーチン
ms.assetid: 1ff7915a-0949-43fe-9cf4-c0ad9abf6592
keywords:
- IRP_MJ_CREATE
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティは、WDK のファイル システム、irp_mj_create 用を確認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274bd9078fc8cc514ba1231c72b5d1e32401148f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380027"
---
# <a name="irpmjcreate-dispatch-routine"></a>IRP\_MJ\_ディスパッチ ルーチンの作成


内の Windows セキュリティ チェックの主要な部分で発生した、 [ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)ルーチンをディスパッチします。 Windows のセキュリティ モデルの大部分が検証へのアクセスに関連するためです。 アクセスの検証結果は、この操作の結果として作成されたハンドルの一部として格納されます。 後続の操作は、この時点で計算権限に対して検証されます。

元がアクセス権を IRP の中に指定である場合は、アクセスは、ファイルまたはディレクトリを開いた後、ファイルの変更に対する権限、\_MJ\_を有効にする作成操作を続行します。 これらのアクセス権は、ハンドルに関連付けられた、後続の操作を管理、下で、アクセスが与えられたハンドルが解決しない限りためです。

ここでは、次のトピックについて説明します。

[IRP の走査の権限のチェック\_MJ\_を作成します。](checking-for-traverse-privilege-on-irp-mj-create.md)

[IRP の他の特殊なケースについてチェック\_MJ\_を作成します。](checking-for-other-special-cases--on-irp-mj-create.md)

[IRP の監査を追加する\_MJ\_を作成します。](adding-auditing-on-irp-mj-create.md)

[IRP 上へのアクセス制御の管理を一覧表示\_MJ\_を作成します。](management-of-access-control-lists-on-irp-mj-create.md)

[IRP 上の新しいファイルへのセキュリティの割り当て\_MJ\_を作成します。](assigning-security-to-a-new-file-on-irp-mj-create.md)

[IRP のクォータを処理\_MJ\_を作成します。](handling-quotas-on-irp-mj-create.md)

 

 




