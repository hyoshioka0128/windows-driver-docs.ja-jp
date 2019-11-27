---
title: IRP_MJ_SET_INFORMATION 操作の Oplock 状態を確認しています
description: IRP_MJ_SET_INFORMATION 操作の Oplock 状態を確認しています
ms.assetid: d164be8d-cf42-4b96-9883-e0f8223bfde4
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4dcf0d3fb97b4db7947861c330dc063f18bb2bef
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543047"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_set_information-operation"></a>IRP_MJ_SET_INFORMATION 操作の Oplock 状態を確認しています

次の IRP_MJ_SET_INFORMATION 操作の oplock の状態を確認します。

- FileEndOfFileInformation
- Fileの情報
- FileValidDataLengthInformation
- FileRenameInformation
- FileShortNameInformation
- FileLinkInformation
- FileDispositionInformation

## <a name="checking-oplock-state-for-fileendoffileinformation-fileallocationinformation-and-filevaliddatalengthinformation-operations"></a>FileEndOfFileInformation、FileFileValidDataLengthInformation Information、および操作の oplock 状態を確認しています

この情報は、ファイルまたはストリームに対して次の操作が実行されている場合に適用されます。

- 呼び出し元がストリームの論理サイズを変更しようとしています。 キャッシュマネージャーのレイジーライタースレッドが新しいファイルの終わりを設定しようとすると、oplock チェックは行われないことに注意してください。 これは、実際の書き込み要求を受信したときにチェックが行われたためです。

- 呼び出し元は、割り当てられたストリームのサイズを変更しようとします。

### <a name="conditions-for-a-level-2-request-type"></a>レベル2の要求の種類の条件

- 常に [なし] になります。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-all-other-request-types"></a>その他すべての要求の種類の条件

- Oplock を所有する FILE_OBJECT のキーとは異なる oplock キーを持つ FILE_OBJECT で操作が行われた場合、IRP_MJ_SET_INFORMATION (FileEndOfFileInformation、FileFileValidDataLengthInformation Information、および) で中断します。 Oplock が解除されている場合は、None に中断します。

- 確認の要件は次のとおりです。

  - 読み取り要求: 確認は必要ありません。操作は直ちに続行されます。

  - 読み取りハンドル要求: 中断の確認が必要ですが、操作はすぐに (つまり、受信確認を待たずに) 続行されます。

  - レベル1、バッチ、フィルター、読み取り/書き込み、および読み取り/書き込みハンドル要求: 操作を続行する前に受信確認を受信する必要があります。

## <a name="checking-oplock-state-for-filerenameinformation-fileshortnameinformation-and-filelinkinformation-operations"></a>FileRenameInformation、FileShortNameInformation、および FileLinkInformation 操作の oplock 状態を確認しています

この情報は、ファイルまたはストリームに対して次の操作が実行されている場合に適用されます。

- ファイルまたはストリームの名前が変更されています。

- ファイルに短い名前が設定されています。

- ファイルのハードリンクが作成されています。 これは、新しいハードリンクが別のファイルへの既存のリンクを置き換えるときに、置き換えられるリンクに oplock が存在する場合に、oplock 状態に影響します。

- Oplock が存在するストリームの先祖ディレクトリの名前が変更されたか、または先祖ディレクトリの短い名前が設定されています。

### <a name="conditions-for-level-1-level-2-read-and-read-write-operations"></a>レベル1、レベル2、読み取り、および読み取り/書き込み操作の条件

- Oplock が破損していません。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-batch-filter-read-handle-and-read-write-handle-operations"></a>バッチ、フィルター、読み取りハンドル、および読み取り/書き込みの各操作の条件

- Oplock を所有する FILE_OBJECT のキーとは異なる oplock キーを持つ FILE_OBJECT で操作が発生した場合に、IRP_MJ_SET_INFORMATION (FileRenameInformation、FileShortNameInformation、および FileLinkInformation) で中断します。 Oplock が解除された場合は、次のようになります。

  - バッチおよびフィルター要求が None に分割されます。

  - 読み取りハンドル要求が読み取りを中断します。

  - 読み取り/書き込みハンドルの要求は、読み取り/書き込みを中断します。

- 操作を続行するには、受信確認を受信する必要があります。
  
## <a name="checking-oplock-state-for-filedispositioninformation-operations"></a>FileDispositionInformation 操作の oplock 状態を確認しています

この情報は、呼び出し元がファイルを削除しようとしたときに適用されます。

- Oplock を所有している FILE_OBJECT のキー [FILE_DISPOSITION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)とは異なる oplock キーを持つ FILE_OBJECT で操作が発生した場合は、IRP_MJ_SET_INFORMATION (FileDispositionInformation) を中断**し**ます。DeleteFile は * * TRUE * * * * です。 Oplock が解除された場合は、次のようになります。

  - 読み取りハンドル要求が読み取りを中断します。

  - 読み取り/書き込みハンドルの要求は、読み取り/書き込みを中断します。

- 操作を続行するには、受信確認を受信する必要があります。
