---
title: バグチェック 0x103 MUP_FILE_SYSTEM
description: MUP_FILE_SYSTEM バグチェックの値は0x00000103 です。
ms.assetid: 2756bdcc-5b10-481e-99ec-17b00c4f459d
keywords:
- バグチェック 0x103 MUP_FILE_SYSTEM
- MUP_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUP_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b1661c8512d0a99b59a1a110a77f1611462de9d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209096"
---
# <a name="bug-check-0x103-mup_file_system"></a>バグチェック 0x103: MUP\_ファイル\_システム


MUP\_ファイル\_システムのバグチェックには、0x00000103 の値が含まれています。 このバグチェックは、複数の UNC プロバイダー (MUP) で無効なデータまたは予期しないデータが検出されたことを示します。 その結果、MUP は、リモートファイルシステム要求をネットワークリダイレクター (汎用名前付け規則 (UNC) プロバイダー) にチャネルできません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="mup_file_system-parameters"></a>MUP\_ファイル\_システムパラメーター


パラメーター1は違反の種類を識別します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>保留中の IRP のアドレス。</p></td>
<td align="left"><p>ファイルコンテキストが見つからないファイルオブジェクトのアドレス。</p></td>
<td align="left"><p>デバイスオブジェクトのアドレス。</p></td>
<td align="left"><p>MUP は、ファイルオブジェクトに対応するファイルコンテキストを見つけることができませんでした。 これは、通常、mup が、対応する IRP_MJ_CREATE 要求を表示しないファイルオブジェクトの i/o 要求を参照していることを示しています。 このバグチェックの原因として、フィルタードライバーエラーが考えられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>予想されるファイルコンテキストのアドレス。</p></td>
<td align="left"><p>ファイルオブジェクトから実際に取得されたアドレス。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ファイルコンテキストがファイルオブジェクトに対して存在することがわかっていますが、予期されたものではありませんでした (たとえば、 <strong>NULL</strong>である可能性があります)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>IRP コンテキストのアドレス。</p></td>
<td align="left"><p>IRP 完了ステータスコード。</p></td>
<td align="left"><p>IRP を完了した UNC プロバイダーのドライバーオブジェクト ( <strong>NULL</strong>の場合もあります)。</p></td>
<td align="left"><p>IRP の完了状態が予期しないか無効です。</p>
<p>このバグチェックは、Windows のチェックされたビルドを使用しており、レガシネットワークリダイレクターに接続されているファイルシステムフィルタードライバーによってのみ発生します。 チェックされたビルドは、Windows 10 バージョン1803より前の以前のバージョンの Windows で使用できました。 従来のリダイレクターでは、 <strong>Fsrtlregisteruncprovider</strong>を使用して、MUP に登録します。 このバグチェックは、IRP_MJ_CLEANUP または IRP_MJ_CLOSE 要求で STATUS_SUCCESS されていない NTSTATUS を返すフィルタードライバーを検出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>IRP のアドレス</p></td>
<td align="left"><p>ファイルオブジェクトのアドレス</p></td>
<td align="left"><p>ファイルオブジェクトのファイルコンテキスト</p></td>
<td align="left"><p>ファイルオブジェクトの作成要求が完了する前に、ファイルオブジェクトに対して i/o 操作が開始されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

MUP は、処理するすべてのファイルオブジェクトについて、ファイルごとのオブジェクトごとにコンテキスト情報を保持します。

 

 




