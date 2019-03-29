---
title: 閉じるときに削除
description: 閉じるときに削除
ms.assetid: 340e470f-7791-4677-9369-75ed8fa9f8ad
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルは、WDK のファイル システム、閉じるときに削除を確認します。
- FILE_DELETE_ON_CLOSE
- 閉じる WDK ファイル システム上の削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9de3ae03f99ce02ed430250c73f66e3cfa4d388
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571392"
---
# <a name="delete-on-close"></a>閉じるときに削除


## <span id="ddk_delete_on_close_if"></span><span id="DDK_DELETE_ON_CLOSE_IF"></span>


呼び出し元を指定すると、**ファイル\_削除\_ON\_閉じる** オプションが、呼び出し元がファイルの削除権限を持っていることを確認するか、子権限を削除するファイル システムのチェックのために必要な親ディレクトリです。 いずれかのアクセス許可は、ファイルを削除するのには不十分です。 これは、処理するためにファイル システムの重要なケースです。 閉じているときに、ファイルを削除する操作のセマンティクスは、I/O マネージャーではなく、ファイル システムには適用されません。

ファイル システムは、ボリュームが書き込み禁止ではありませんし、この操作は、この操作が許可されていないディレクトリに適用されないことを確認する必要もあります。 FASTFAT ファイル システム コードの書き込みで保護されたボリュームのチェックはやファイルを使用して削除するルート ディレクトリを許可しないなどの\_削除\_ON\_閉じる。 これらのチェックの例が記載されて、 **FatCommonCreate** WDK を含む fastfat サンプルから Create.c ソース ファイル内の関数。

 

 




