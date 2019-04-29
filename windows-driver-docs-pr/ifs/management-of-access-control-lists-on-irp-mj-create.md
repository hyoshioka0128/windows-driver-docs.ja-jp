---
title: IRP_MJ_CREATE でのアクセス制御リストの確認
description: IRP_MJ_CREATE でのアクセス制御リストの確認
ms.assetid: 07b35931-8e20-4789-b2ef-14c6195b817f
keywords:
- IRP_MJ_CREATE
- アクセス制御リストの WDK ファイル システム
- セキュリティは、WDK のファイル システム、irp_mj_create 用を確認します。
- ACL の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42bca29a7bf3d44c9f148dc747e1410e91591782
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384353"
---
# <a name="management-of-access-control-lists-on-irpmjcreate"></a>IRP 上へのアクセス制御の管理を一覧表示\_MJ\_を作成します。


## <span id="ddk_management_of_access_control_lists_on_irp_mj_create_if"></span><span id="DDK_MANAGEMENT_OF_ACCESS_CONTROL_LISTS_ON_IRP_MJ_CREATE_IF"></span>


これは、さまざまなセキュリティに関連するその他の問題、ファイル システム内でアドレスを指定できます。 たとえば、ディスク上のアクセス制御リストの管理は、主要なセキュリティの問題です。 セキュリティ情報は、何千ものファイルのと同じである可能性があります、こと、セキュリティ記述子の共有のモデルを実装するために、ファイル システムと便利です。 したがって、同じセキュリティ記述子を使用するすべてのファイルは、セキュリティ記述子の 1 つのディスク上 (および場合によってメモリ内) のコピーを共有します。 NTFS ファイル システムでは、このモデルを使用します。

1 つのオプションは、ファイル システム キャッシュ結果になります。 セキュリティに関連が厳密は、セキュリティ操作がかなりのコストをファイルを開くなどの通常の操作に追加できることを認識する必要があります。 したがって、以前の操作からのセキュリティの結果をキャッシュは、以前の決定に依存するファイル システムを許可できます。 たとえば、同じファイルに同じユーザーに与えられていたアクセスのサブセットを要求する新しい呼び出しを閉じません付与する可能性があります。 もちろん、このような任意のメカニズムを追加するリスクとは、不適切なアクセスを許可するバグを追加する可能性があります。 任意のセキュリティの実装が期待どおりの方法で動作することを確認するを徹底的にテストすることを確認するのには重要です。

 

 




