---
title: 処理の作成
description: 処理の作成
ms.assetid: c15a56d2-47db-4124-8250-f25f69d2d4e3
keywords:
- セキュリティ WDK ファイルシステム、セマンティックモデルチェック
- セマンティックモデルは、WDK ファイルシステムをチェックし、処理を作成します
- 処理 WDK ファイルシステムを作成する
- セキュリティリファレンスモニタ WDK
- IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b05170d556d47091a0d9d06986d16572ebf4f570
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841452"
---
# <a name="create-processing"></a>処理の作成


## <span id="ddk_create_processing_if"></span><span id="DDK_CREATE_PROCESSING_IF"></span>


ファイルシステムの場合、特に興味深いセキュリティ作業のほとんどは、 [**IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)処理中に行われます。 この手順では、受信要求を分析し、呼び出し元が操作を実行するための適切な権限を持っているかどうかを判断し、必要に応じて操作を許可または拒否する必要があります。 幸いなことに、ファイルシステムの開発者にとっては、ほとんどの決定メカニズムがセキュリティ参照モニター内に実装されています。 したがって、ほとんどの場合、ファイルシステムは適切なセキュリティ参照モニタールーチンを呼び出して、アクセスを適切に判断するだけで十分です。 ファイルシステムのリスクは、必要に応じてこれらのルーチンを呼び出すことができず、不適切に呼び出し元へのアクセスを許可しない場合に発生します。

FAT ファイルシステムなどの標準ファイルシステムの場合、IRP\_MJ\_CREATE の一部として実行されるチェックは、主にセマンティクスチェックです。 たとえば、FAT ファイルシステムには、ファイルまたはディレクトリの状態に基づいて、IRP\_MJ\_CREATE 処理が許可されていることを確認するための多くのチェックがあります。 FAT ファイルシステムによって実行されるこれらのチェックには、読み取り専用メディアのチェックが含まれます (たとえば、上書きや置き換える、読み取り専用メディアに対する "作成" 操作を実行しようとした場合など)、共有アクセスチェック、oplock チェックなどがあります。 この分析の最も難しい部分の1つは、別のレベルリソース (ボリュームレベルなど) の状態が原因で、1つのレベル (ファイルレベルなど) の操作が実際には許可されないことを認識することです。 たとえば、別のプロセスによってボリュームが排他的にロックされている場合、ファイルを開くことはできません。 一般的なチェックの例を次に示します。

-   ファイルレベルがボリュームレベルの状態と互換性があるかどうか。 ボリュームレベルのロックは cache-control である必要があります。 したがって、1つのプロセスが排他ボリュームレベルのロックを保持している場合、そのプロセス内のスレッドだけがファイルを開くことができます。 他のプロセスのスレッドでは、ファイルを開くことができません。

-   ファイルレベルがメディアの状態と互換性があるかどうか。 "作成" 操作によって、"作成" 操作の一部としてファイルが変更されます。 これには、ファイルに対する最後のアクセス時刻の上書き、置き換え、および更新が含まれます。 これらの "作成" 操作は読み取り専用メディアでは許可されておらず、最終アクセス時刻は更新されません。

-   ボリュームレベルは、ファイルレベルの状態と互換性があるかどうかを確認できます。 ボリュームで開かれている既存のファイルがある場合、排他ボリュームを開くことはできません。 これは、新しい開発者がボリュームを開こうとして失敗したことを検出するため、一般的な問題です。 このエラーが発生すると、FSCTL\_マウント解除\_ボリュームを使用して、開いているハンドルを無効にし、マウント解除を強制して、新しくマウントされたボリュームに排他的にアクセスできるようになります。

また、ファイル属性には互換性がある必要があります。 読み取り専用属性を持つファイルは、書き込みアクセス用に開くことができません。 一般的な権限を展開した後で、目的のアクセス権を確認する必要があることに注意してください。 たとえば、FASTFAT ファイルシステム内のこのチェックは**FatCheckFileAccess**関数内にあります (WDK に含まれる FASTFAT サンプルの Acchksup ソースファイルを参照してください)。

次のコード例は、FAT セマンティクスに固有のものです。 また、Dacl を実装するファイルシステムでは、セキュリティ参照モニタールーチン ([**Seaccesscheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)など) を使用した追加のセキュリティチェックが実行されます。

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

FASTFAT によって実装されるより微妙なチェックとして、呼び出し元によって要求されるアクセスが、FAT ファイルシステムが認識しているもの (Acchksup の**FatCheckFileAccess**関数で、WDK に含まれている FASTFAT サンプルから) があることを確認します。

次のコード例は、ファイルシステムのセキュリティに関する重要な概念を示しています。 ファイルシステムに渡された内容が予期した範囲外にならないことを確認します。 セキュリティの観点から見た控えめで適切なアプローチは、アクセス要求を把握していない場合、その要求を拒否する必要があることです。

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

幸いなことに、ファイルシステムでは、最初の作成処理中にセキュリティチェックが行われると、その後のセキュリティチェックが i/o マネージャーによって実行されます。 したがって、たとえば、i/o マネージャーを使用すると、ユーザーモードアプリケーションが読み取りアクセス専用で開かれたファイルに対して書き込み操作を実行しないようにすることができます。 実際、ファイルシステムでは、ファイルオブジェクトに対して読み取り専用のセマンティクスを強制しようとしないでください。これは、IRP\_MJ\_書き込みディスパッチルーチンの実行中に、読み取りアクセスのみで開かれた場合でも同様です。 これは、メモリマネージャーが特定のファイルオブジェクトを特定のセクションオブジェクトに関連付ける方法によるものです。 ファイルが読み取り専用で開かれている場合でも、そのセクションを使用した後続の書き込みは、ファイルオブジェクトに対する書き込み操作\_IRP\_MJ として送信されます。 つまり、ファイルハンドルが[**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)によって Nt システムサービスのエントリポイントで対応するファイルオブジェクトに変換されると、アクセスの適用が行われます。

ファイルシステム内には次の2つの場所があり、セマンティックセキュリティチェックは "作成" 処理と同様に行う必要があります。

-   名前変更またはハードリンクの処理中。

-   ファイルシステムの制御操作を処理する場合。

名前の変更処理とファイルシステムの制御処理については、以降のセクションで説明します。

これは、"作成" 処理に関連するセマンティック問題の完全な一覧ではないことに注意してください。 このセクションの目的は、ファイルシステムの開発者にとって、これらの問題に注意することです。 すべてのセマンティック問題は、特定のセマンティクスを満たすように実装されている特定のファイルシステムに対して特定し、実装がさまざまなケースを処理するようにテストする必要があります。

 

 




