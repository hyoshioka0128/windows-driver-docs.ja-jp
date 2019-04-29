---
title: IRP_MJ_SET_INFORMATION 操作の Oplock の状態を確認
description: IRP_MJ_SET_INFORMATION 操作の Oplock の状態を確認
ms.assetid: d164be8d-cf42-4b96-9883-e0f8223bfde4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d00b47675e9af7846e588c859278c8ecc5f6042
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324404"
---
# <a name="checking-the-oplock-state-of-an-irpmjsetinformation-operation"></a>IRP_MJ_SET_INFORMATION 操作の Oplock の状態を確認


IRP_MJ_SET_INFORMATION の特定の操作では、oplock の状態を確認します。 次の 6 つの操作では、このチェックを実行します。

### <a name="span-idfileendoffileinformationfileallocationinformationandfilevaliddatalengthinformationspanspan-idfileendoffileinformationfileallocationinformationandfilevaliddatalengthinformationspanspan-idfileendoffileinformationfileallocationinformationandfilevaliddatalengthinformationspanfileendoffileinformation-fileallocationinformation-and-filevaliddatalengthinformation"></a><span id="FileEndOfFileInformation__FileAllocationInformation__and_FileValidDataLengthInformation"></span><span id="fileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformation"></span><span id="FILEENDOFFILEINFORMATION__FILEALLOCATIONINFORMATION__AND_FILEVALIDDATALENGTHINFORMATION"></span>FileEndOfFileInformation、FileAllocationInformation、および FileValidDataLengthInformation

この情報は、次の操作は、ファイルまたはストリームで実行されているときに適用されます。

- 呼び出し元は、論理ストリームのサイズを変更しようとします。 キャッシュ マネージャーのレイジー ライター スレッドがファイルの新しい末尾を設定しようとすると、oplock のチェックが行われていないことに注意してください。 これは、ため、実際の書き込み要求を受け取ったときに、以前に行ったチェックです。

- 呼び出し元が割り当てられているストリームのサイズを変更しようとするとします。
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
  <p>書き込みハンドルの読み取り</p>
  </td>
  <td>
  <p>(FileEndOfFileInformtion、FileAllocationInformation、FileValidDataLengthInformation 用) と IRP_MJ_SET_INFORMATION に分かれます。</p>
  <ul>
  <li>
  <p> 操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が破損している場合。</p>
  <ul>
  <li>
  <p> [なし] に中断します。</p>
  </li>
  <li>
  <p>ハンドルの読み取り要求。操作がすぐに続行して、中断の受信確認が必要ですが (つまり、なし、受信確認を待機中)。</p>
  </li>
  <li>
  <p> 他のすべての要求タイプ。操作を続行する前に、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>Read</p>
  </td>
  <td>
  <p>(FileEndOfFileInformtion、FileAllocationInformation、FileValidDataLengthInformation 用) と IRP_MJ_SET_INFORMATION に分かれます。</p>
  <ul>
  <li>
  <p> 操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が破損している場合。</p>
  <ul>
  <li>
  <p> [なし] に中断します。</p>
  </li>
  <li>
  <p> 受信確認は必要ありません、すぐに、操作を続行します。</p>
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
  <p> [なし] に常に中断します。</p>
  </li>
  <li>
  <p> 受信確認は必要ありません、すぐに、操作を続行します。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileRenameInformation__FileShortNameInformation__and_FileLinkInformation"></a><a id="filerenameinformation__fileshortnameinformation__and_filelinkinformation"></a><a id="FILERENAMEINFORMATION__FILESHORTNAMEINFORMATION__AND_FILELINKINFORMATION"></a>FileRenameInformation、FileShortNameInformation、および FileLinkInformation</h3>
  <p>この情報は、次の操作は、ファイルまたはストリームで実行されているときに適用されます。</p>
  <ul>
  <li>
  <p> ファイルまたはストリームを変更する場合します。</p>
  </li>
  <li>
  <p> 短い名前は、ファイルの設定されています。</p>
  </li>
  <li>
  <p> ファイルのハード リンクを作成しています。 これは、新しいハード リンクを優先すると、別のファイルに既存のリンクとリンクの置き換えられる oplock が存在する場合で、oplock の状態に影響します。</p>
  </li>
  <li>
  <p> Oplock が存在するストリームの上位ディレクトリを変更する場合、または親ディレクトリの短い名前が設定されています。</p>
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
  <p>(FileRenameInformation、FileShortNameInformation、FileLinkInformation 用) と IRP_MJ_SET_INFORMATION に分かれます。</p>
  <ul>
  <li>
  <p>  操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> Oplock が破損している場合。</p>
  <ul>
  <li>
  <p>  [なし] に中断します。</p>
  </li>
  <li>
  <p> 操作を続行する前に、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>読み取りハンドル</p>
  </td>
  <td>
  <p>(FileRenameInformation、FileShortNameInformation、FileLinkInformation 用) と IRP_MJ_SET_INFORMATION に分かれます。</p>
  <ul>
  <li>
  <p>  操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> Oplock が破損している場合。</p>
  <ul>
  <li>
  <p>  読み取り専用に中断します。</p>
  </li>
  <li>
  <p> 操作を続行する前に、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>書き込みハンドルの読み取り</p>
  </td>
  <td>
  <p>(FileRenameInformation、FileShortNameInformation、FileLinkInformation 用) と IRP_MJ_SET_INFORMATION に分かれます。</p>
  <ul>
  <li>
  <p> 操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が破損している場合。</p>
  <ul>
  <li>
  <p> 読み取り/書き込みにブレークします。</p>
  </li>
  <li>
  <p> 操作を続行する前に、受信確認を受信する必要があります。</p>
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
  <p> Oplock は破損していない、受信確認は不要ですが、および、操作をすぐに続行します。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileDispositionInformation"></a><a id="filedispositioninformation"></a><a id="FILEDISPOSITIONINFORMATION"></a>FileDispositionInformation</h3>
  <p>この情報は、呼び出し元のファイルを削除しようとするときに適用されます。</p>
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
  <p>(FileDispositionInformation) をときに IRP_MJ_SET_INFORMATION に分かれます。</p>
  <ul>
  <li>
  <p>操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
  <p><b>AND</b></p>
  </li>
  <li>
  <p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545765"><b>FILE_DISPOSITION_INFORMATION</b></a>します。DeleteFile は<b>TRUE</b>します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が破損している場合。</p>
  <ul>
  <li>
  <p> 読み取り専用に中断します。</p>
  </li>
  <li>
  <p>操作を続行する前に、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>書き込みハンドルの読み取り</p>
  </td>
  <td>
  <p>(FileDispositionInformation) をときに IRP_MJ_SET_INFORMATION に分かれます。</p>
  <ul>
  <li>
  <p>操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</p>
  <p><b>AND</b></p>
  </li>
  <li>
  <p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545765"><b>FILE_DISPOSITION_INFORMATION</b></a>します。DeleteFile は<b>TRUE</b>します。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>Oplock が破損している場合。</p>
  <ul>
  <li>
  <p> 読み取り/書き込みにブレークします。</p>
  </li>
  <li>
  <p>操作を続行する前に、受信確認を受信する必要があります。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
 




