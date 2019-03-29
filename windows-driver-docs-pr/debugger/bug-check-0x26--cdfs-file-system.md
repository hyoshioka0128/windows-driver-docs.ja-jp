---
title: バグ チェック 0x26 CDFS_FILE_SYSTEM
description: CDFS_FILE_SYSTEM のバグ チェックでは、0x00000026 の値を持ちます。 これは、CD ファイル システムで問題が発生したことを示します。
ms.assetid: f427c262-f750-4719-a52b-2f00094d2a4e
keywords:
- バグ チェック 0x26 CDFS_FILE_SYSTEM
- CDFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CDFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9adc9a7e6c65122f55b409deb4dcc267929cf15c
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464296"
---
# <a name="bug-check-0x26-cdfsfilesystem"></a>バグ チェック 0x26:CDFS\_ファイル\_システム


CDFS\_ファイル\_システムのバグ チェックが 0x00000026 の値を持ちます。 これは、CD ファイル システムで問題が発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="cdfsfilesystem-parameters"></a>CDFS\_ファイル\_システム パラメーター


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
<td align="left"><p>ソース ファイルと行番号情報を指定します。 上位 16 ビット ("0 x"の後に最初の 4 つの 16 進数字) は、その識別子番号によってソース ファイルを特定します。 下位 16 ビットは、バグ チェックが発生したファイル内のソース行を特定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>場合<strong>CdExceptionFilter</strong>はスタックで、このパラメーターは例外レコードのアドレスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>場合<strong>CdExceptionFilter</strong>はスタックで、このパラメーターはコンテキスト レコードのアドレスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックの 1 つの考えられる原因は、ディスクの破損です。 ファイル システムまたはディスク上の不良ブロック (セクター) 内の破損には、このエラーを誘発できます。 SCSI と IDE のドライバの破損は、システムの機能を読み取って、そのため、エラーの原因で、ディスクに書き込む悪影響を受けることができます。

もう 1 つの考えられる原因は、非ページ プール メモリの不足です。 非ページ プール メモリは完全になくなると、このエラーは、システムを停止できます。 ただし、インデックス作成のプロセス中に使用可能な非ページ プール メモリの量が非常に低い場合別のカーネル モード ドライバーを非ページ プール メモリを必要とすることができますもこのエラーをトリガーします。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)パラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

**ディスク破損の問題を解決するには。** SCSI と FASTFAT (システム ログ)、またはデバイスや、エラーの原因となっているドライバーの特定に役立つ可能性がある Autochk (アプリケーション ログ) からのエラー メッセージをイベント ビューアを確認します。 ウイルス スキャナー、バックアップ プログラム、またはシステムを継続的に監視するディスク デフラグ ツールを無効にしてください。 システム製造元から提供されたハードウェア診断を実行することもあります。 詳細については、これらの手順は、コンピューターの製造元のマニュアルを参照してください。 実行**Chkdsk/f/r**を検出し、ファイル システム構造的な破損を解決します。 システム パーティションにディスクのスキャンが開始する前に、システムを再起動する必要があります。

**非ページ プール メモリの枯渇問題を解決するには。** コンピューターに新しい物理メモリを追加します。 これにより、カーネルで使用できる非ページ プール メモリの量が増加します。

 

 




