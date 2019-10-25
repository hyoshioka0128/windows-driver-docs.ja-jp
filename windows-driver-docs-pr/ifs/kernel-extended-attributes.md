---
title: カーネル拡張属性
description: フィルター マネージャーとミニフィルター ドライバー アーキテクチャ
keywords:
- 拡張ファイル属性
- カーネル EA
- 拡張属性
- $Kernel
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16b9dbe69f85ba5c1561f920803ba1a8d151c8a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841142"
---
# <a name="kernel-extended-attributes"></a>カーネル拡張属性
カーネル拡張属性 (カーネル EA) は、イメージファイル署名の検証のパフォーマンスを向上させる方法として、Windows 8 の NTFS に追加された機能です。  画像署名を検証するためのコストが高い操作です。 したがって、以前に検証されたバイナリが変更されたかどうかに関する情報を格納すると、イメージが完全な署名チェックを行う必要があるインスタンスの数が減少します。


## <a name="overview"></a>概要
名前プレフィックス ``$Kernel`` を持つ EA は、カーネルモードからのみ変更できます。 この文字列で始まるすべての EA は、カーネル EA と見なされます。 必要な Update Sequence Number (USN) を取得する前に、最初に**FSCTL_WRITE_USN_CLOSE_RECORD**を発行することをお勧めします。これにより、前に発生した可能性があるファイルに対して保留中の USN ジャーナル更新がコミットされます。 これを行わないと、カーネル EA の設定直後に**Fileusn**値が変更される可能性があります。

カーネル EA には、少なくとも次の情報が含まれていることをお勧めします。
- USN UsnJournalID
  - **UsnJournalID**フィールドは、USN ジャーナルファイルの現在の部分を識別する GUID です。  USN ジャーナルは、ボリュームごとにユーザーモードから削除および作成できます。  USN ジャーナルが作成されるたびに、新しい**UsnJournalID** GUID が生成されます。  このフィールドでは、USN ジャーナルが無効になっていて再検証できる期間があるかどうかを確認できます。
    - この値は[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)を使用して取得できます。
- USN FileUSN
  - **Fileusn**値には、ファイルに対して行われた最後の変更の USN ID が含まれており、指定されたファイルのマスターファイルテーブル (MFT) レコード内で追跡されます。
    - USN ジャーナルが削除されると、 **Fileusn**は0にリセットされます。

この情報と、特定の使用量が必要になる場合があります。その後、ファイルにカーネル EA として設定します。


## <a name="setting-a-kernel-extended-attribute"></a>カーネル拡張属性の設定
カーネル EA を設定するには、まずプレフィックス ``"$Kernel."`` で開始し、有効な EA 名の文字列で trailed する必要があります。 ユーザーモードからカーネル EA を設定しようとすると、警告なしで無視されます。  要求は**STATUS_SUCCESS**を返しますが、EA の実際の変更は行われません。 カーネルモードから[Zwseteafile](https://msdn.microsoft.com/library/windows/hardware/ff961908)いる API を呼び出すカーネル EA を設定するには、カーネルモード[では十分](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltseteafile)ではありません。  これは、SMB がネットワーク経由での EA の設定をサポートし、これらの要求がサーバーのカーネルモードから発行されるためです。  

カーネル EA を設定するには、呼び出し元は、IRP (i/o 要求パケット) の MinorFunction フィールドで**IRP_MN_KERNEL_CALL**値も設定する必要があります。 このフィールドを設定する唯一の方法は、カスタムの IRP を生成することであるため、ルーチン[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)は、カーネル EA を設定するためのサポート関数として FsRtl パッケージからエクスポートされています。

[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)の同じ呼び出しで、normal と kernel EA の設定を混在させることはできません。  この操作を行うと、 **STATUS_INTERMIXED_KERNEL_EA_OPERATION**で操作が失敗します。    カーネル EA を設定しても、 **USN_REASON_EA_CHANGE**レコードは USN ジャーナルに生成されません。その結果、カーネル EA と通常の EA を同じ操作で使用することはできません。  


## <a name="querying-an-extended-attribute"></a>拡張属性のクエリ
ユーザーモードから EA のファイルを照会すると、通常の EA とカーネル EA の両方が返されます。 アプリケーションの互換性の問題を最小限に抑えるために、ユーザーモードに戻ります。 通常の[Zwquerの](https://msdn.microsoft.com/library/windows/hardware/ff961907)操作では、ユーザー[モードとカーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryeafile)モードの両方から、通常とカーネルの両方の EA が返されます。

使用できるのは、 **FileObject**だけである場合、 [FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)を使用すると、カーネル EA のカーネルモードのクエリを実行する方が便利な場合があります。


## <a name="querying-update-sequence-number-journal-information"></a>更新シーケンス番号のジャーナル情報を照会しています
[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)操作では、 **IRP_MN_KERNEL_CALL**値が IRP の minorfunction フィールドで設定されていない限り、カーネルモードから発行された場合でも**SE_MANAGE_VOLUME_PRIVILEGE**が必要です。 ルーチン**Fsrtlkernel Fscontrolfile**は、カーネルモードコンポーネントがこの USN 要求を簡単に発行できるように、カーネルの FsRtl パッケージからエクスポートされています。

**メモ**Windows 10 以降のバージョン1703以降では、この操作に SE_MANAGE_VOLUME_PRIVILEGE が不要になりました。  

## <a name="auto-deletion-of-kernel-extended-attributes"></a>カーネル拡張属性の自動削除
ファイルの USN ID が原因でファイルを再スキャンするだけで、問題が発生しているため、USN 更新プログラムがファイルに投稿される可能性が非常に高くなります。  これを簡単にするために、カーネル EA の機能の自動削除が NTFS に追加されました。

このシナリオでは、すべてのカーネル EA が削除されるとは限りません。そのため、拡張 EA プレフィックス名が使用されます。  カーネル EA が以下で始まる場合: ``"$Kernel.Purge."`` 次の USN の理由のいずれかが USN ジャーナルに書き込まれると、NTFS は、そのファイルに存在する、指定された名前付け構文に準拠しているすべてのカーネル EAs を削除します。  
- USN_REASON_DATA_OVERWRITE
- USN_REASON_DATA_EXTEND
- USN_REASON_DATA_TRUNCATION
- USN_REASON_REPARSE_POINT_CHANGE

このカーネル EA の削除は、メモリ不足の状況でも成功します。

## <a name="remarks"></a>注釈
- カーネル EA は、ユーザーモードのコンポーネントによって改ざんされることはありません。
- カーネル EA は、通常の EA と同じファイルに存在できます。


## <a name="see-also"></a>参照
[Fltquerごみ箱](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryeafile)  
[FltSetEaFile セット](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltseteafile)  
[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)  
[FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)      
[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)  
[Zwquerごみ箱](https://msdn.microsoft.com/library/windows/hardware/ff961907)  
[ZwSetEaFile セット](https://msdn.microsoft.com/library/windows/hardware/ff961908)  
