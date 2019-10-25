---
title: IRP_MJ_SET_INFORMATION 操作の Oplock 状態を確認しています
description: IRP_MJ_SET_INFORMATION 操作の Oplock 状態を確認しています
ms.assetid: d164be8d-cf42-4b96-9883-e0f8223bfde4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caacea027897c13c5114b2d515636a232a452f39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841148"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_set_information-operation"></a>IRP_MJ_SET_INFORMATION 操作の Oplock 状態を確認しています


特定の IRP_MJ_SET_INFORMATION 操作で oplock 状態を確認します。 次の6つの操作でこのチェックが実行されます。

### <a name="span-idfileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformationspanspan-idfileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformationspanspan-idfileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformationspanfileendoffileinformation-fileallocationinformation-and-filevaliddatalengthinformation"></a><span id="FileEndOfFileInformation__FileAllocationInformation__and_FileValidDataLengthInformation"></span><span id="fileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformation"></span><span id="FILEENDOFFILEINFORMATION__FILEALLOCATIONINFORMATION__AND_FILEVALIDDATALENGTHINFORMATION"></span>FileEndOfFileInformation、FileFileValidDataLengthInformation Information、および

この情報は、ファイルまたはストリームに対して次の操作が実行されている場合に適用されます。

- 呼び出し元がストリームの論理サイズを変更しようとしています。 キャッシュマネージャーのレイジーライタースレッドが新しいファイルの終わりを設定しようとすると、oplock チェックは行われないことに注意してください。 これは、実際の書き込み要求を受信したときにチェックが行われたためです。

- 呼び出し元は、割り当てられたストリームのサイズを変更しようとします。
  <table>
  <tr>
  <th>要求の種類</th>
  <th>条件</th>
  </tr>
  <tr>
  <td rowspan="2">
  <p>レベル 1</p>
  <p>Batch (バッチ)</p>
  <p>フィルター</p>
  <p>読み取りハンドル</p>
  <p>読み取り/書き込み</p>
  <p>読み取り/書き込み-ハンドル</p>
  </td>
  <td>
  <p>次の場合に、IRP_MJ_SET_INFORMATION (FileendoffileFileValidDataLengthInformation、Fileて INFORMATION、および) で破損しています。</p>
  <ul>
  <li>
  <p> この操作は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT に対して発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が解除された場合は、次のようになります。</p>
  <ul>
  <li>
  <p> [なし] に分割します。</p>
  </li>
  <li>
  <p>読み取りハンドル要求の場合: 中断の確認が必要ですが、操作はすぐに (つまり、受信確認を待たずに) 続行されます。</p>
  </li>
  <li>
  <p> 他のすべての要求の種類: 操作が続行される前に受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>Read</p>
  </td>
  <td>
  <p>次の場合に、IRP_MJ_SET_INFORMATION (FileendoffileFileValidDataLengthInformation、Fileて INFORMATION、および) で破損しています。</p>
  <ul>
  <li>
  <p> この操作は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT に対して発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が解除された場合は、次のようになります。</p>
  <ul>
  <li>
  <p> [なし] に分割します。</p>
  </li>
  <li>
  <p> 確認は必要ありません。操作は直ちに続行されます。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>レベル 2</p>
  </td>
  <td>
  <ul>
  <li>
  <p> 常に [なし] になります。</p>
  </li>
  <li>
  <p> 確認は必要ありません。操作は直ちに続行されます。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileRenameInformation__FileShortNameInformation__and_FileLinkInformation"></a><a id="filerenameinformation__fileshortnameinformation__and_filelinkinformation"></a><a id="FILERENAMEINFORMATION__FILESHORTNAMEINFORMATION__AND_FILELINKINFORMATION"></a>FileRenameInformation、FileShortNameInformation、FileLinkInformation</h3>
  <p>この情報は、ファイルまたはストリームに対して次の操作が実行されている場合に適用されます。</p>
  <ul>
  <li>
  <p> ファイルまたはストリームの名前が変更されています。</p>
  </li>
  <li>
  <p> ファイルに短い名前が設定されています。</p>
  </li>
  <li>
  <p> ファイルのハードリンクが作成されています。 これは、新しいハードリンクが別のファイルへの既存のリンクを置き換えるときに、置き換えられるリンクに oplock が存在する場合に、oplock 状態に影響します。</p>
  </li>
  <li>
  <p> Oplock が存在するストリームの先祖ディレクトリの名前が変更されたか、または先祖ディレクトリの短い名前が設定されています。</p>
  </li>
  </ul>
  <table>
  <tr>
  <th>要求の種類</th>
  <th>条件</th>
  </tr>
  <tr>
  <td rowspan="2">
  <p>Batch (バッチ)</p>
  <p>フィルター</p>
  </td>
  <td>
  <p>次の場合に、IRP_MJ_SET_INFORMATION (FileRenameInformation、FileShortNameInformation、および FileLinkInformation) で破損しています。</p>
  <ul>
  <li>
  <p>  この操作は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT に対して発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> Oplock が解除された場合は、次のようになります。</p>
  <ul>
  <li>
  <p>  [なし] に分割します。</p>
  </li>
  <li>
  <p> 操作を続行するには、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>読み取りハンドル</p>
  </td>
  <td>
  <p>次の場合に、IRP_MJ_SET_INFORMATION (FileRenameInformation、FileShortNameInformation、および FileLinkInformation) で破損しています。</p>
  <ul>
  <li>
  <p>  この操作は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT に対して発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> Oplock が解除された場合は、次のようになります。</p>
  <ul>
  <li>
  <p>  読み取りに中断します。</p>
  </li>
  <li>
  <p> 操作を続行するには、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>読み取り/書き込み-ハンドル</p>
  </td>
  <td>
  <p>次の場合に、IRP_MJ_SET_INFORMATION (FileRenameInformation、FileShortNameInformation、および FileLinkInformation) で破損しています。</p>
  <ul>
  <li>
  <p> この操作は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT に対して発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が解除された場合は、次のようになります。</p>
  <ul>
  <li>
  <p> 読み取り/書き込みに中断します。</p>
  </li>
  <li>
  <p> 操作を続行するには、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>レベル 1</p>
  <p>レベル 2</p>
  <p>Read</p>
  <p>読み取り/書き込み</p>
  </td>
  <td>
  <ul>
  <li>
  <p> Oplock は解除されず、確認は必要ありません。操作は直ちに続行されます。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileDispositionInformation"></a><a id="filedispositioninformation"></a><a id="FILEDISPOSITIONINFORMATION"></a>FileDispositionInformation</h3>
  <p>この情報は、呼び出し元がファイルを削除しようとしたときに適用されます。</p>
  <table>
  <tr>
  <th>要求の種類</th>
  <th>条件</th>
  </tr>
  <tr>
  <td rowspan="2">
  <p>読み取りハンドル</p>
  </td>
  <td>
  <p>次の場合に IRP_MJ_SET_INFORMATION (FileDispositionInformation) で破損します。</p>
  <ul>
  <li>
  <p>この操作は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT に対して発生します。</p>
  <p><b>そして</b></p>
  </li>
  <li>
  <p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information"><b>FILE_DISPOSITION_INFORMATION</b></a>。DeleteFile は<b>TRUE</b>です。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が解除された場合は、次のようになります。</p>
  <ul>
  <li>
  <p> 読み取りに中断します。</p>
  </li>
  <li>
  <p>操作を続行するには、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>読み取り/書き込み-ハンドル</p>
  </td>
  <td>
  <p>次の場合に IRP_MJ_SET_INFORMATION (FileDispositionInformation) で破損します。</p>
  <ul>
  <li>
  <p>この操作は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT に対して発生します。</p>
  <p><b>そして</b></p>
  </li>
  <li>
  <p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information"><b>FILE_DISPOSITION_INFORMATION</b></a>。DeleteFile は<b>TRUE</b>です。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が解除された場合は、次のようになります。</p>
  <ul>
  <li>
  <p> 読み取り/書き込みに中断します。</p>
  </li>
  <li>
  <p>操作を続行するには、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
 




