---
title: バグ チェック 0x9B UDFS_FILE_SYSTEM
description: UDFS_FILE_SYSTEM のバグ チェックでは、0x0000009B の値を持ちます。 このバグ チェックでは、UDF ファイル システムで問題が発生したことを示します。
ms.assetid: cf20429d-6007-47e7-9faa-db7e1489e96b
keywords:
- バグ チェック 0x9B UDFS_FILE_SYSTEM
- UDFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UDFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08c39decebbfd46f5db69b54a2ebea53ca5555a8
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519103"
---
# <a name="bug-check-0x9b-udfsfilesystem"></a>バグ チェック 0x9B:UDF\_ファイル\_システム


UDF\_ファイル\_システムのバグ チェックが 0x0000009B の値を持ちます。 このバグ チェックでは、UDF ファイル システムで問題が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="udfsfilesystem-parameters"></a>UDF\_ファイル\_システム パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>ソース ファイルと行番号の情報を実行します。 上位 16 ビット ("0 x"の後に最初の 4 つの 16 進数字) は、その識別子番号によってソース ファイルを特定します。 下位 16 ビットは、バグ チェックが発生したファイル内のソース行を特定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>場合<strong>UdfExceptionFilter</strong>はスタックで、このパラメーターは例外レコードのアドレスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>場合<strong>UdfExceptionFilter</strong>はスタックで、このパラメーターはコンテキスト レコードのアドレスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

UDF\_ファイル\_システムのバグ チェックはディスクの破損原因と考えられます。 ファイル システムまたはディスク上の不良ブロック (セクター) 内の破損には、このエラーを誘発できます。 SCSI と IDE のドライバの破損は、システムの能力を読み取り、ディスクに書き込むと、エラーが発生します悪影響を受けることができます。

このバグ チェックが、非ページ プール メモリがいっぱいの場合も発生します。 非ページ プールのメモリがいっぱいの場合、このエラーは、システムを停止できます。 ただし、インデックス作成のプロセス中に使用可能な非ページ プール メモリの量が非常に低い場合は別のカーネル モード ドライバーを非ページ プール メモリを必要とすることができますもこのエラーをトリガーします。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)パラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

**ディスク破損の問題を解決するには。** SCSI と FASTFAT (システム ログ)、またはデバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある Autochk (アプリケーション ログ) からのエラー メッセージをイベント ビューアを確認します。 任意のウイルス スキャナー、バックアップ アプリケーションは、またはディスク デフラグ ツール、システムを継続的に監視を無効にします。 システムの製造元が提供するハードウェアの診断を実行することもあります。 これらの手順の詳細については、コンピューターの製造元のマニュアルを参照してください。 実行**Chkdsk/f/r**を検出し、ファイル システム構造的な破損を解決します。 システム パーティションにディスクのスキャンが開始する前に、システムを再起動する必要があります。

**非ページ プール メモリの枯渇問題を解決するには。** コンピューターに新しい物理メモリを追加します。 このメモリはカーネルを使用可能な非ページ プール メモリの量を増加します。

 

 




