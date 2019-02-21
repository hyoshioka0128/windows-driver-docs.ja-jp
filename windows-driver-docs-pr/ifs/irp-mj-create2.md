---
title: Irp_mj_create 用操作の Oplock の状態を確認
description: Irp_mj_create 用操作の Oplock の状態を確認
ms.assetid: 30684025-9da0-4f4c-a850-ab0390bef091
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a970302fe1bddae85e728615bf130994581e333
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553563"
---
# <a name="checking-the-oplock-state-of-an-irpmjcreate-operation"></a>Irp_mj_create 用操作の Oplock の状態を確認


次は、ファイルの既存のストリームが開いているときにのみ適用されます (つまり、新しく作成されたストリームでことはできませんの既存の各 oplock に)。

**注**  FILE_RESERVE_OPFILTER がない限り、必要なアクセスは何も FILE_READ_ATTRIBUTES、FILE_WRITE_ATTRIBUTES、または同期以外が含まれる場合は、任意の oplock の irp_mj_create 用を処理するとき、oplock は中断されません指定します。 作成が成功した場合、oplock の結果 FILE_RESERVE_OPFILTER を常に指定します。 簡潔にするため、わかりやすくするための次の表は、上記に oplock のすべてに適用するためを省略します。
<table>
<tr>
<th>要求の種類</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>レベル 1</p>
</td>
<td>
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>
<p> 関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p>[なし] に中断<b>場合</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER フラグを設定します。</p>
<p><b>OR</b></p>
</li>
<li>次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>その他。</b></p>
<ul>
<li>レベル 2 にブレークします。</li>
</ul>
</li>
<li>
<p>操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>レベル 2</p>
</td>
<td>
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</li>
<li><b>そして：</b><ul>
<li>
<p>FILE_RESERVE_OPFILTER フラグを設定します。</p>
<p><b>OR</b></p>
</li>
<li> 次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
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
<td rowspan="2">
<p>Batch (バッチ)</p>
</td>
<td>
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>
<p> 関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p>[なし] に中断<b>場合</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER フラグが設定されます。</p>
<p><b>OR</b></p>
</li>
<li>次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>その他。</b></p>
<ul>
<li>レベル 2 にブレークします。</li>
</ul>
</li>
<li>
<p>操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>フィルター</p>
</td>
<td>
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>
<p> 関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</p>
</li>
<li><b>そして：</b><ul>
<li>
<p>A&quot;書き込み可能な&quot;FILE_SHARE_READ アクセス用に開かれませんでしたが、ストリームで要求されたアクセスが必要です。  なお&quot;書き込み可能な&quot;へのアクセスが以外の任意の属性として定義されます。</p>
<ul>
<li>FILE_READ_ATTRIBUTES</li>
<li>FILE_WRITE_ATTRIBUTES</li>
<li>FILE_READ_DATA</li>
<li>FILE_READ_EA</li>
<li>FILE_EXECUTE</li>
<li>同期</li>
<li>READ_CONTROL</li>
</ul>
</li>
</ul>
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
<p> 操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Read</p>
</td>
<td>
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>
<p>関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</p>
</li>
<li><b>そして：</b><ul>
<li>
<p>FILE_RESERVE_OPFILTER フラグを設定します。</p>
<p><b>OR</b></p>
</li>
<li> 次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
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
<td rowspan="2">
<p>読み取りハンドル</p>
</td>
<td>
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>
<p>既存の現在開いている競合は、共有違反が発生するように開きます。</p>
<p><b>OR</b></p>
</li>
<li>
<p>FILE_RESERVE_OPFILTER フラグが設定されます。</p>
<p><b>OR</b></p>
</li>
<li>
<p>次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</p>
<p><b></b> (の上記の 3 つの条件のいずれか)</p>
</li>
<li>
<p> 関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p>[なし] に中断<b>場合</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER フラグが設定されます。</p>
<p><b>OR</b></p>
</li>
<li>次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>その他。</b></p>
<ul>
<li>読み取り専用に中断します。</li>
</ul>
</li>
<li>共有違反が発生するように、既存の現在開いている競合が開くために oplock が破損した場合は、操作を続行する前に受信確認が受信する必要があります。
      </li>
<li>中断の受信確認は必須ですが、その他の何らかの理由で、oplock が破損した場合は、すぐに (受信確認を待機することがなくなど) の操作が続行されます。</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>読み取り/書き込み</p>
</td>
<td>
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>
<p>関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p>[なし] に中断<b>場合</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER フラグが設定されます。</p>
<p><b>OR</b></p>
</li>
<li>次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>その他。</b></p>
<ul>
<li>読み取り専用に中断します。</li>
</ul>
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
<p>Irp_mj_create 用に壊れている場合。</p>
<ul>
<li>
<p> 関連付けられた open が発生している FILE_OBJECT oplock キーは、oplock を所有している FILE_OBJECT に関連付けられている oplock キーと異なる。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>Oplock が破損している場合。</p>
<ul>
<li>
<p>[なし] に中断<b>場合</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER フラグが設定されます。</p>
<p><b>OR</b></p>
</li>
<li>次のいずれかは、値が指定された処理を作成します。<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>その他。</b></p>
<ul>
<li>
<p>共有違反が発生するように、現在のオープンが既存のオープンと競合する場合は、読み取り/書き込みを中断します。  それ以外の場合、読み取りハンドルを中断します。</p>
</li>
</ul>
</li>
<li>
<p>操作を続行する前に、受信確認を受信する必要があります。</p>
</li>
</ul>
</td>
</tr>
</table>
 

ファイル システムは、バッチとフィルターの各 oplock (なく oplock パッケージ自体) の追加チェックを実行、ファイル システム oplock 中断処理を実行するための oplock のパッケージを確認するかどうかに影響を与える irp_mj_create 用の操作を処理するときにします。 これは、同じファイル (つまり、次の条件の一覧の最後の 2 つのリスト項目) の場合は、他のデータ ストリームの各 oplock を 1 つのデータ ストリームでの操作が影響する場合。 1 つ以上の次の条件が満たされた場合、ファイル システムは、oplock 中断処理を実行するための oplock のパッケージに要求を送信します。

-   これは、ネットワークのクエリを開くと、中断を要求[KTM](https://go.microsoft.com/fwlink/p/?linkid=124745)トランザクションがある場合。 それ以外の場合、区切りをネットワークのクエリを開く要求しないをしないでください。

-   優先的、上書きされたり OVERWRITE_IF 操作は、代替データ ストリームに対して FILE_SHARE_DELETE が指定されていないと、プライマリ データ ストリームにバッチまたはフィルター oplock が、プライマリ データ ストリームのバッチまたはフィルターの oplock の中断を要求します.

-   プライマリ データ ストリームで優先的、上書きされたり OVERWRITE_IF 操作が実行され、削除のアクセス許可が要求されている任意の代替データ ストリームのバッチまたはフィルターの各 oplock がある、代替のすべてのデータのバッチまたはフィルターの各 oplock の中断を要求します。設定されているストリーム。

Oplock 中断処理を実行するための oplock のパッケージを確認するファイル システムが決定したらは、上記の表にレイアウトされる規則が適用されます。

バッチとフィルターの oplock のチェックは、共有のアクセス チェックが行われる前に発生します。 つまり、オープン要求は最終的には共有違反のため失敗した場合でも、バッチまたはフィルター oplock が壊れています。

 

 




