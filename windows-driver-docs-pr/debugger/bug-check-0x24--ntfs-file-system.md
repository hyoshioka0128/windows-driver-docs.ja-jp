---
title: バグ チェック 0x24 NTFS_FILE_SYSTEM
description: NTFS_FILE_SYSTEM のバグ チェックでは、0x00000024 の値を持ちます。 Ntfs.sys、NTFS ドライブを読み書きするシステムをできるようにするドライバー ファイルに問題が発生しました。 これを示します。
ms.assetid: 9d2dd8a8-b550-4392-b663-6902a015ef7b
keywords:
- バグ チェック 0x24 NTFS_FILE_SYSTEM
- NTFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NTFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3486a074cf4487334ce20db9dcb9fb2b50e55b63
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464324"
---
# <a name="bug-check-0x24-ntfsfilesystem"></a>バグ チェック 0x24:NTFS\_ファイル\_システム


NTFS\_ファイル\_システムのバグ チェックが 0x00000024 の値を持ちます。 Ntfs.sys、NTFS ドライブを読み書きするシステムをできるようにするドライバー ファイルに問題が発生しました。 これを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="ntfsfilesystem-parameters"></a>NTFS\_ファイル\_システム パラメーター


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
<td align="left"><p>場合<strong>NtfsExceptionFilter</strong>はスタックで、このパラメーターは例外レコードのアドレスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>場合<strong>NtfsExceptionFilter</strong>はスタックで、このパラメーターはコンテキスト レコードのアドレスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックの 1 つの考えられる原因は、ディスクの破損です。 NTFS ファイル システムまたはハード ディスク上の不良ブロック (セクター) 内の破損は、このエラーを誘発できます。 破損したハード ドライブ (SATA/IDE) のドライバーも悪影響を与えるシステムに影響を与えるため、ディスクに読み書きする機能のエラーの原因です。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)パラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

**ディスク破損の問題を解決するには。**

-   デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性があるシステム ログに表示されているハード ドライブに関連するエラー メッセージのイベント ビューアを確認します。

-   ウイルス スキャナー、バックアップ プログラム、またはシステムを継続的に監視するディスク デフラグ ツールを無効にしてください。

-   記憶域サブシステムに関連するシステムの製造元から提供されたハードウェア診断を実行することもあります。

-   ないファイル システムのエラーを確認するのにには、スキャンのディスク ユーティリティを使用します。 スキャンを選択するドライブを右クリックして**プロパティ**します。 をクリックして**ツール**します。 をクリックして、**今すぐチェック**ボタンをクリックします。
-   ハード ドライブに十分な空き領域があることを確認します。 オペレーティング システムと一部のアプリケーションは、スワップ ファイルを作成する十分な空き領域を必要とし、他の機能です。 システム構成に基づきと、正確な要件は異なりますが、通常は 10 ~ 15% 空き領域があることをお勧めします。

-   システム ファイル チェッカー ツールを使用して、欠落または破損システム ファイルを修復します。 システム ファイル チェッカーは、ユーティリティは Windows ユーザーを Windows システム ファイルで破損をスキャンし、復元できるようにするには、ファイルが破損しています。 システム ファイル チェッカー (SFC.exe) ツールを実行するのにには、次のコマンドを使用します。

    ```console
    SFC /scannow
    ```

    詳細については、次を参照してください。[システム ファイル チェッカー ツールを使用してシステム ファイルの欠落または破損の修復](https://support.microsoft.com/kb/929833)します。

-   **ドライバーの検証ツール**

    Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 ドライバー コードの実行でエラーが参照してください、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifer*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、次を参照してください。 [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)します。

以前は、この停止コードのもう 1 つの考えられる原因は非ページ プール メモリの不足です。 非ページ プール メモリは完全になくなると、このエラーは、システムを停止できます。 ただし、インデックス作成のプロセス中に使用可能な非ページ プール メモリの量が非常に低い場合別のカーネル モード ドライバーを非ページ プール メモリを必要とすることができますもこのエラーをトリガーします。

 

 




