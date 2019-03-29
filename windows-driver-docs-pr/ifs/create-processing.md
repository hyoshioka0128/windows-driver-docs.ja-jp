---
title: 作成処理
description: 作成処理
ms.assetid: c15a56d2-47db-4124-8250-f25f69d2d4e3
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルには WDK ファイル システムがチェックされ、処理の作成
- WDK ファイル システムの処理を作成します。
- WDK のセキュリティ参照モニター
- IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dbd45a5fbb4860c61116ee37519f085f7cf634f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349945"
---
# <a name="create-processing"></a>作成処理


## <span id="ddk_create_processing_if"></span><span id="DDK_CREATE_PROCESSING_IF"></span>


ファイル システムでは、興味深いセキュリティ作業のほとんどは中に発生します。 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)処理します。 これはこの手順、受信要求を分析、呼び出し元が、操作を実行を許可または拒否として適切な操作に必要な権限を持つかどうかを判断する必要があります。 幸いにも、ファイル システムの開発者は、決定メカニズムのほとんどはセキュリティ参照モニター内で実装されます。 そのため、ほとんどの場合、ファイル システムを呼び出すだけのアクセスを適切に決定するために適切なセキュリティ参照モニター ルーチン。 ファイル システムのリスクは、必要に応じて、これらのルーチンの呼び出しに失敗したときに発生し、呼び出し元に不適切なアクセスを許可します。

FAT ファイル システムの IRP の一部として行われたチェックなどの標準的なファイル システムの\_MJ\_作成は主にセマンティック チェックします。 たとえば、FAT ファイル システムにあることを確認するための多数のチェックを IRP\_MJ\_ファイルまたはディレクトリの状態に基づいて作成処理を許可します。 FAT ファイル システムによって行われたこれらのチェックが読み取り専用メディアのチェックが含まれます (たとえば、破壊的な実行を試みる「作成」操作を上書きするかを置き換えると読み取り専用メディアに可能な)、アクセス チェック、および oplock のチェックを共有します。 この分析の最も難しい部分の 1 つは 1 つのレベル (ファイル レベルなど) で操作がさまざまなレベルのリソースの状態であるため許可されません実際可能性がありますを実現する (ボリューム レベルなど)。 たとえば、ファイル可能性があります開くことができません別のプロセスが、ボリュームをロックして排他的場合。 チェックする一般的なケースを含めます。

-   ファイルは、ボリューム レベルの状態との互換性レベルを開きますか? ボリューム レベルのロックを obeyed する必要があります。 したがって、1 つのプロセスには、排他的なボリューム レベルのロックが保持している場合、そのプロセス内の唯一のスレッドは、ファイルを開けます。 スレッドを他のプロセスからはファイルを開くできません必要があります。

-   ファイルは、メディアの状態との互換性レベルを開きますか? 特定の「作成」操作では、「作成」操作の一部としてファイルを変更します。 上書きは、これを置き換えるし、ファイルの最終アクセス時刻のも更新。 読み取り専用メディアにこれらの操作を「作成」は許可されていませんし、最終アクセス時刻は更新されません。

-   ボリュームは、ファイル レベルの状態との互換性レベルを開きますか? ボリューム上に開かれたファイルが存在する場合、排他的なボリュームのオープンを許可されていませんが。 これは、ボリュームを開き、失敗したことを確認しようとするための新しい開発者向けの一般的な問題です。 これに失敗すると、FSCTL\_マウント解除\_ボリュームに使用できる開いているハンドルが無効になるし、強制的にマウントを解除するには、新たにマウントされたボリュームへの排他アクセスを許可します。

さらに、ファイル属性は、互換性のあるである必要があります。 書き込みアクセスのため読み取り専用属性を持つファイルを開くことができません。 一般的な権限の拡張が展開された後、必要なアクセスをチェックすることに注意してください。 FASTFAT ファイル システム内では、このチェックがであるなど、 **FatCheckFileAccess**関数 (WDK を含む fastfat サンプルから Acchksup.c ソース ファイルを参照してください)。

次のコード例では、FAT セマンティクスに固有です。 同様に、Dacl を実装するファイル システムのセキュリティ参照モニター ルーチンを使用して、追加のセキュリティ チェックを行う ([**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)など)。

```cpp
    //
    //  check for a read-only Dirent
    //

    if (FlagOn(DirentAttributes, FAT_DIRENT_ATTR_READ_ONLY)) {

        //
        //  Check the desired access for a read-only Dirent
        // Don't allow 
        //  WRITE, FILE_APPEND_DATA, FILE_ADD_FILE,
        //  FILE_ADD_SUBDIRECTORY, and FILE_DELETE_CHILD
        //

        if (FlagOn(*DesiredAccess, ~(DELETE |
                                     READ_CONTROL |
                                     WRITE_OWNER |
                                     WRITE_DAC |
                                     SYNCHRONIZE |
                                     ACCESS_SYSTEM_SECURITY |
                                     FILE_READ_DATA |
                                     FILE_READ_EA |
                                     FILE_WRITE_EA |
                                     FILE_READ_ATTRIBUTES |
                                     FILE_WRITE_ATTRIBUTES |
                                     FILE_EXECUTE |
                                     FILE_LIST_DIRECTORY |
                                     FILE_TRAVERSE))) {

            DebugTrace(0, Dbg, "Cannot open readonly\n", 0);

            try_return( Result = FALSE );
        }
```

FASTFAT によって実装されるより複雑なチェックは、呼び出し元によって要求されたアクセスはどの FAT ファイル システムの認識が何かあることを確認する (で、 **FatCheckFileAccess** fastfat から Acchksup.c で関数のサンプルを WDK含まれています)。

次のコード例では、ファイル システムのセキュリティの重要な概念を示します。 期待どおりの境界の外側に、ファイル システムに何が渡されることを確認します。 が当てはまりませんでした。 セキュリティの観点から慎重かつ適切なアプローチは、アクセス要求を理解していない場合は、その要求を拒否する必要があります。

```cpp
    //
    // Check the desired access for the object. 
    // Reject what we do not understand.
    // The model of file systems using ACLs is that
    // they do not type the ACL to the object that the 
    // ACL is on. 
    // Permissions are not checked for consistency vs.
    // the object type - dir/file.
    //

    if (FlagOn(*DesiredAccess, ~(DELETE |
                                 READ_CONTROL |
                                 WRITE_OWNER |
                                 WRITE_DAC |
                                 SYNCHRONIZE |
                                 ACCESS_SYSTEM_SECURITY |
                                 FILE_WRITE_DATA |
                                 FILE_READ_EA |
                                 FILE_WRITE_EA |
                                 FILE_READ_ATTRIBUTES |
                                 FILE_WRITE_ATTRIBUTES |
                                 FILE_LIST_DIRECTORY |
                                 FILE_TRAVERSE |
                                 FILE_DELETE_CHILD |
                                 FILE_APPEND_DATA))) {

        DebugTrace(0, Dbg, "Cannot open object\n", 0);

        try_return( Result = FALSE );
    }
```

さいわいなことにファイル システムでは、初期中にセキュリティ チェックが完了したら作成処理、後続のセキュリティを I/O マネージャーでチェックされます。 したがって、たとえば、I/O マネージャーにより、ユーザー モード アプリケーションが読み取りアクセス用のみで開かれたファイルに対して書き込み操作を実行していないこと。 実際には、ファイル システムしないで、ファイル オブジェクトに対する読み取り専用のセマンティクスを適用する IRP の中に、読み取りアクセスに対してのみ開かれた場合でも\_MJ\_書き込みディスパッチ ルーチン。 これは、メモリ マネージャーが、指定したセクション オブジェクトを特定のファイル オブジェクトを関連付けます方法に起因します。 そのセクションから、後続の書き込みは IRP として送信されます\_MJ\_読み取り専用ファイルが開かれた場合でも、ファイル オブジェクトに対する操作を記述します。 つまり、アクセスの適用はファイル ハンドルが Nt システム サービスのエントリ ポイントである対応するファイル オブジェクトに変換される際に行われます[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)します。

セマンティック セキュリティ チェック行う必要がある処理を「作成」のような 2 つの追加場所ファイル システム内で。

-   名前の変更、またはハード リンクの処理中には

-   ときにファイル システムの処理は、操作を制御します。

名前の変更の処理とファイル システムのコントロールの処理については、後続のセクションで説明します。

「作成」の処理に関連するセマンティックの問題をすべて網羅ではないことに注意してください。 このセクションの目的は、ファイル システムの開発者向けのこれらの問題に注目です。 セマンティックのすべての問題の特定のファイル システムで特定された、特定のセマンティクスを満たすために実装およびテスト、実装がさまざまなケースを処理することを確認する必要があります。

 

 




