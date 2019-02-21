---
title: 実行可能イメージ
description: 実行可能イメージ
ms.assetid: ca279a74-5f30-4413-bf1c-4d5af12d294d
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルは、WDK のファイル システム、実行可能イメージを確認します。
- WDK のファイル システムの実行可能イメージ
- メモリ マップト ファイル WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac55025cb80e76c4f9a0acae0d2e53bd3ac74f93
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538017"
---
# <a name="executable-images"></a>実行可能イメージ


## <span id="ddk_executable_images_if"></span><span id="DDK_EXECUTABLE_IMAGES_IF"></span>


メモリの割り当て済みのイメージ ファイルを使用してプロセスのアドレス空間には、実行可能ファイルが読み込まれます。 ファイル自体を開く必要も、ハンドルはセクションを使用して、マッピングが行われるため、作成する必要があります。 メモリ マップ ファイルをサポートするいると仮定すると、これらの特殊なセマンティクスを適用するファイル システムを確認する必要があります。 たとえば、このケースを確認するには、FASTFAT ファイル システム コードで見つかる、 **FatOpenExistingFCB** WDK を含む fastfat サンプルから Create.c ソース ファイル内の関数。

```cpp
    //
    //  If the user wants write access to the file, make sure there
    //  is not a process mapping this file as an image. Any attempt to
    //  delete the file will be stopped in fileinfo.c
    //
    //  If the user wants to delete on close, check at this
    //  point though.
    //

    if (FlagOn(*DesiredAccess, FILE_WRITE_DATA) || DeleteOnClose) {

        Fcb->OpenCount += 1;
        DecrementFcbOpenCount = TRUE;

        if (!MmFlushImageSection( &Fcb->NonPaged->SectionObjectPointers,
                                  MmFlushForWrite )) {

            Iosb.Status = DeleteOnClose ? STATUS_CANNOT_DELETE :STATUS_SHARING_VIOLATION;
            try_return( Iosb );
        }
    }
```

そのため、ファイル システムにより、ファイルが開いていない場合でも、実行可能イメージを含む、メモリ マップ ファイルを削除することはできません。

 

 




