---
title: テキスト ログのイベント カテゴリを有効にします。
description: テキスト ログのイベント カテゴリを有効にします。
ms.assetid: 555f698b-69e2-469b-b958-185cb35eeb5a
keywords:
- イベント カテゴリの WDK SetupAPI ログ
- テキスト ログの WDK SetupAPI、イベント カテゴリ
- ログマスク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f5229398b921b6a2ff122096444b2349a60af1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536531"
---
# <a name="enabling-event-categories-for-a-text-log"></a>テキスト ログのイベント カテゴリを有効にします。


SetupAPI ログ エントリを書き込む場合のみテキスト ログでイベントのカテゴリ テキスト ログのログ エントリが有効になっていると、[イベント レベル](setting-the-event-level-for-a-text-log.md)ログがイベント ログ エントリのイベント レベル以上のテキスト。

次の表は、SetupAPI をサポートするイベント カテゴリ、イベントのカテゴリと、マニフェスト定数の値を表すマニフェスト定数を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント カテゴリの操作</th>
<th align="left">イベント カテゴリのマニフェスト定数</th>
<th align="left">イベント カテゴリの値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>デバイスのインストール</p></td>
<td align="left"><p>TXTLOG_DEVINST</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
<tr class="even">
<td align="left"><p>INF ファイルを管理します。</p></td>
<td align="left"><p>TXTLOG_INF</p></td>
<td align="left"><p>0x00000002</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ファイルのキューを管理します。</p></td>
<td align="left"><p>TXTLOG_FILEQ</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>ファイルのコピー</p></td>
<td align="left"><p>TXTLOG_COPYFILES</p></td>
<td align="left"><p>0x00000008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>レジストリ設定を管理します。</p></td>
<td align="left"><p>TXTLOG_REGISTRY</p></td>
<td align="left"><p>0x00000010</p></td>
</tr>
<tr class="even">
<td align="left"><p>デジタル署名を確認します。</p></td>
<td align="left"><p>TXTLOG_SIGVERIF</p></td>
<td align="left"><p>0x00000020</p></td>
</tr>
<tr class="odd">
<td align="left"><p>デバイスとドライバーのプロパティを管理します。</p></td>
<td align="left"><p>TXTLOG_PROPERTIES</p></td>
<td align="left"><p>0x00000040</p></td>
</tr>
<tr class="even">
<td align="left"><p>バックアップ データ</p></td>
<td align="left"><p>TXTLOG_BACKUP</p></td>
<td align="left"><p>0x00000080</p></td>
</tr>
<tr class="odd">
<td align="left"><p>管理ユーザー インターフェイス ダイアログ ボックス</p></td>
<td align="left"><p>TXTLOG_UI</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="even">
<td align="left"><p>新しいデバイス マネージャー</p></td>
<td align="left"><p>TXTLOG_NEWDEV</p></td>
<td align="left"><p>0x01000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ユーザー モードの PnP マネージャー</p></td>
<td align="left"><p>TXTLOG_UMPNPMGR</p></td>
<td align="left"><p>0x02000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバー ストアを管理します。</p></td>
<td align="left"><p>TXTLOG_DRIVER_STORE</p></td>
<td align="left"><p>0x04000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クラスのインストーラーや共同インストーラーの操作</p></td>
<td align="left"><p>TXTLOG_INSTALLER</p></td>
<td align="left"><p>0x40000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>ベンダーから提供された操作</p></td>
<td align="left"><p>TXTLOG_VENDOR</p></td>
<td align="left"><p>0x80000000</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="to-enable-event-categories-for-the-setupapi-logs--create--or-modify--the-following-reg-dword-registry-value-"></a>SetupAPI ログのイベント カテゴリを有効にする、作成 (または変更) に、次[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)レジストリ値。  
**HKEY_LOCAL_MACHINE\\ソフトウェア\\Microsoft\\Windows\\CurrentVersion\\セットアップ\\ログマスク**

**ログマスク**デバイス インストールのテキスト ログとアプリケーション インストールのテキスト ログにレジストリ値が適用されます。

場合、**ログマスク**レジストリ値が存在しないか、SetupAPI がテキスト ログのすべてのイベント カテゴリを使用します。 場合、**ログマスク**レジストリ値が 0 で、SetupAPI テキスト ログのすべてのイベント カテゴリを無効にします。

**ログマスク**レジストリ値は 0 X として書式設定*VVVVVVVV、場所 VVVVVVVV*は 32 ビット フィールド。 すべてのカテゴリを有効にするには設定**ログマスク**を 0 XFFFFFFFF にします。 特定のカテゴリのみを有効にするには、対応するイベント カテゴリの定数のビットごとの OR を実行します。 次に、例を示します。

-   デバイス インストールの操作によって書き込まれるログ エントリのみを有効にするには設定**ログマスク**TXTLOG_DEVINST (0X00000001) の値を

-   デバイス インストールの操作、およびドライバー ストアの操作によって書き込まれるログ エントリのみを有効にするには設定**ログマスク**に (TTXTLOG_DRIVER_STORE |TEXTLOG_DEVINST) (0X04000001)。

-   カスタム インストールの操作によって書き込まれるログ エントリのみを有効にするには設定**ログマスク**TXTLOG_VENDOR (0x80000000) にします。

 

 





