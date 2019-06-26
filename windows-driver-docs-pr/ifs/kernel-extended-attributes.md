---
title: カーネル拡張属性
description: フィルター マネージャーとミニフィルター ドライバー アーキテクチャ
keywords:
- ファイル属性を拡張します。
- EA のカーネル
- 拡張属性
- $Kernel
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac76e5a893ce4742578315333b2710b14d882f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375988"
---
# <a name="kernel-extended-attributes"></a>カーネル拡張属性
拡張属性のカーネル (カーネル EA) 様は、イメージ ファイルの署名の検証のパフォーマンスを向上する手段として、Windows 8 で NTFS に追加機能です。  負荷の高い操作、イメージの署名を確認することをお勧めします。 そのため、バイナリは、まだ検証されていたが変更されている、またはいないイメージが、完全署名のチェックを行う必要があるインスタンスの数を減らすかどうかについて情報を保存します。


## <a name="overview"></a>概要
名前プレフィックスを持つ EA``$Kernel``カーネル モードからのみ変更できます。 この文字列で始まる任意の EA は、カーネル EA と見なされます。 必要な更新シーケンス番号 (USN) を取得する前にお勧めする**FSCTL_WRITE_USN_CLOSE_RECORD**これはコミット保留中の USN ジャーナル更新前に発生した場合、ファイルのいずれかと、1 つ目を発行します。 これを行わない、 **FileUSN**カーネル EA の設定のすぐ後の値を変更する可能性があります。

カーネル EA が含まれている、少なくとも次の情報にはお勧めします。
- USN UsnJournalID
  - **UsnJournalID**フィールドは、USN ジャーナル ファイルの現在のバージョンを識別する GUID。  USN ジャーナルを削除し、ボリュームごとのユーザー モードから作成することができます。  新しい USN ジャーナルが作成されるたびに**UsnJournalID** GUID が生成されます。  このフィールドがあったかどうか、一定期間、USN ジャーナルが無効になっているかがわかり、再検証できます。
    - 使用してこの値を取得できる[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)します。
- USN FileUSN
  - **FileUSN**値には、最後に変更をファイルにしましたが、指定されたファイルのマスター ファイル テーブル (MFT) レコード内の追跡の USN ID が含まれています。
    - USN ジャーナルが削除されると、 **FileUSN**ゼロにリセットされます。

その他の特定の使用は、必要なと共に、この情報は、カーネル EA としてファイルに設定されます。


## <a name="setting-a-kernel-extended-attribute"></a>拡張属性のカーネルの設定
カーネル EA を設定するには、プレフィックスで始まる必要があります``"$Kernel."``する有効な EA 名前文字列が最後とします。 ユーザー モードからカーネル EA を設定しようとすると、自動的に無視されます。  要求が返されます**STATUS_SUCCESS**が EA の実際の変更は加えられません。 ように API を呼び出すカーネル EA を設定する[ZwSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961908)または[FltSetEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltseteafile)のカーネル モードは不十分です。  これは、SMB、ネットワーク経由で EA の設定をサポートするサーバー上のカーネル モードからそれらの要求が発行するためです。  

カーネル EA、呼び出し元の設定を設定する必要がありますも、 **IRP_MN_KERNEL_CALL** (I/O 要求パケット) IRP の MinorFunction フィールドの値。 このフィールドを設定する唯一の方法は、カスタムの IRP、ルーチンを生成することですので[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)カーネル EA を設定するサポート機能として FsRtl パッケージからエクスポートされました。

通常と同じ呼び出しでカーネルの EA の設定を混在させることがありますいないを[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)します。  操作に失敗しましたが、これを行う場合**STATUS_INTERMIXED_KERNEL_EA_OPERATION**します。    カーネルの EA は生成されません設定、 **USN_REASON_EA_CHANGE**レコードの USN ジャーナルには、その結果、カーネルの EA と標準の EA では使用できません、同じ操作。  


## <a name="querying-an-extended-attribute"></a>拡張属性のクエリを実行します。
EA のユーザー モードのファイルにクエリを実行すると、両方の標準が返されますおよびカーネル EA の。 ユーザー モード アプリケーションの互換性問題を最小限に抑えるには、これらが返されます。 通常の[ZwQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961907)と[FltQueryEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryeafile)操作はユーザーとカーネル モードから標準と EA のカーネルの両方が返すされます。

ときにのみ、 **FileObject**を使用して、利用[FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)カーネル モードからカーネル ea のクエリを使用するために都合があります。


## <a name="querying-update-sequence-number-journal-information"></a>更新シーケンス番号の履歴情報のクエリを実行します。
[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)操作が必要です**SE_MANAGE_VOLUME_PRIVILEGE**しない限り、カーネル モードから発行された場合でも、 **IRP_MN_KERNEL_CALL**値で設定されましたIRP の MinorFunction フィールドです。 ルーチン**FsRtlKernelFsControlFile**カーネル モード コンポーネントでこの USN 要求を発行するカーネルを簡単にできるように FsRtl パッケージからエクスポートされました。

**注**SE_MANAGE_VOLUME_PRIVILEGE を必要と不要になった Windows 10 バージョン 1703 以降でこの操作を開始します。  

## <a name="auto-deletion-of-kernel-extended-attributes"></a>カーネルの自動削除属性の拡張
多くの問題のない理由がある変更されたファイルの USN ID は高価なできるので単純にファイルを再スキャン USN の更新プログラムは、ファイルにポスト可能性があります。  これを簡素化するには、NTFS、自動削除のカーネル EA の機能が追加されました。

すべてのカーネル EA は、このシナリオで削除する必要があるために、拡張の EA プレフィックス名が使用されます。  カーネル EA が始まる場合: ``"$Kernel.Purge."`` USN ジャーナルには、次の USN 理由のいずれかが書き込まれる、NTFS が特定の名前付け構文に準拠したそのファイルに存在するすべてのカーネル EAs 削除されます。  
- USN_REASON_DATA_OVERWRITE
- USN_REASON_DATA_EXTEND
- USN_REASON_DATA_TRUNCATION
- USN_REASON_REPARSE_POINT_CHANGE

カーネル EA のこの削除は、メモリ不足の状況であっても正常になります。

## <a name="remarks"></a>注釈
- EA をカーネルは、ユーザー モード コンポーネントによって改ざんされることはできません。
- EA をカーネルは、標準の EA と同じファイルに存在できます。


## <a name="see-also"></a>関連項目
[FltQueryEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryeafile)  
[FltSetEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltseteafile)  
[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)  
[FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)      
[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)  
[ZwQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961907)  
[ZwSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961908)  
