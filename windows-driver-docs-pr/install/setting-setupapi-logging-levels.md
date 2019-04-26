---
title: SetupAPI のログ レベルの設定
description: SetupAPI のログ レベルの設定
ms.assetid: e6fa4c9c-e210-42c7-8bc7-d36463073c28
keywords:
- ログ記録レベル WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10bfa0dec357cf349f4f1a4ccefb1e319664e722
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348684"
---
# <a name="setting-setupapi-logging-levels"></a>SetupAPI のログ レベルの設定





SetupAPI ログは、すべてのいずれかに書き込まれる情報の量を制御する*デバイス インストール アプリケーション*または個々 のデバイスのインストール アプリケーション。

すべてのデバイスのインストール アプリケーション SetupAPI ログに書き込まれる情報のレベルを変更するには、次のレジストリ値を作成 (または変更)。

```cpp
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

(次の表に記載した値を使用して) この値を設定してログに記録されるエラーのレベルを選択して、ログ記録の詳細度を変更または記録を無効にすることができます。 ログ ファイルについてもデバッガーに情報を記録することもできます。

個々 のデバイスのインストール アプリケーションのログ記録レベルを指定するには、次のキーの下のレジストリ エントリを作成します。

```cpp
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\AppLogLevels
```

このキーの下には、アプリケーションの実行可能ファイルの名前を表す値の名前を作成し、名前 (次の表に記載した値を使用) などに必要なログ記録レベルを割り当てる**service.exe=** <em>LoggingLevel</em>します。

ログ記録レベルは、DWORD 値です。 この値が指定されていないか、ゼロの場合、SetupAPI は、次の表に記載されている既定の動作を使用します。

3 つの部分、0 x として書式設定の DWORD 値から成る*SSSSDDGG*します。 下位の 8 ビット マスク 0x000000FF、によって表されるは、全般的なデバイスのインストール操作のログ記録レベルを設定します。 次の上位の 8 ビット マスク 0x0000FF00、によって表されるデバイス インストールの操作のログ記録レベルを設定します。 最上位ビットは、特別なフラグです。

次の表には、一般的なログ記録レベル、デバイスのインストールのログ記録レベル、および Windows 2000 以降の特別なログ記録フラグが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">一般的なログ記録レベル</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>既定の設定 (現在 0x20) を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>オフ (デバイスのインストール ログ記録されません)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000010</p></td>
<td align="left"><p>エラー ログに記録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000020</p></td>
<td align="left"><p>ログのエラーと警告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000030</p></td>
<td align="left"><p>エラー、警告、およびその他の情報を記録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000040</p></td>
<td align="left"><p>詳細モードでは、エラー、警告、およびその他の情報をログインします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000050</p></td>
<td align="left"><p>詳細出力モード、およびタイムスタンプ付きのエントリには、エラー、警告、およびその他の情報をログインします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000060</p></td>
<td align="left"><p>詳細出力モード、および時間のエントリには、エラー、警告、およびその他の情報をログインします。 さらに、すべてのエントリでは、タイムスタンプです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000070</p></td>
<td align="left"><p>詳細出力モード、およびメッセージには、エラー、警告、およびその他の情報をログインします。 すべてのエントリが、タイムスタンプです。 キャッシュ ヒット数など、システムの速度が低下する追加のメッセージが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x000000FF</p></td>
<td align="left"><p>使用可能な最も詳細なログ記録を指定します。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイスのログ記録レベル</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>既定の設定 (現在 0x3000) を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000100</p></td>
<td align="left"><p>オフ (デバイスのインストール ログ記録されません)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00001000</p></td>
<td align="left"><p>エラー ログに記録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00002000</p></td>
<td align="left"><p>ログのエラーと警告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00003000</p></td>
<td align="left"><p>エラー、警告、およびその他の情報を記録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00004000</p></td>
<td align="left"><p>詳細モードでは、エラー、警告、およびその他の情報をログインします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00005000</p></td>
<td align="left"><p>詳細出力モード、およびタイムスタンプ付きのエントリには、エラー、警告、およびその他の情報をログインします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00006000</p></td>
<td align="left"><p>詳細出力モード、および時間のエントリには、エラー、警告、およびその他の情報をログインします。 さらに、すべてのエントリでは、タイムスタンプです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00007000</p></td>
<td align="left"><p>詳細出力モード、およびメッセージには、エラー、警告、およびその他の情報をログインします。 すべてのエントリが、タイムスタンプです。 キャッシュ ヒット数など、システムの速度が低下する追加のメッセージが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0000FF00</p></td>
<td align="left"><p>使用可能な最も詳細なログ記録を指定します。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特殊なフラグ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x08000000</p></td>
<td align="left"><p>(<em>Windows XP 以降</em>) すべてのログ エントリにタイムスタンプを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>(<em>Windows XP 以降</em>) の各エントリが書き込まれた後に、ディスクにログ情報をフラッシュしません。 (ログ記録時間は短くなりますが、システムがクラッシュした場合、情報が失われる可能性があります)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>エントリをグループ化ではなく時間順のログ エントリを記述します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>出力をログ ファイルについてもデバッガーに送信します。</p></td>
</tr>
</tbody>
</table>

 

たとえば、SetupAPI がいくつかのサンプルを解釈*LoggingFlags*値は次のように。

-   0x00000000 では、既定のログ記録を意味します。

-   0x0000FFFF では、詳細ログ記録を意味します。

-   0x8000FF00 手段、インストールの詳細なデバイス情報をログ ファイルと、デバッガーの両方にログインします。

クリーン インストール中に、既定の SetupAPI ログ記録レベルを変更するには、セットアップのテキスト モードとフル インストール モードのセットアップの期間中に、レジストリを編集します。 次の手順では、手順を説明します。 これらの手順をインストールすることを想定しています*d:\\Winnt*いて、別のパーティション上の Windows の同じバージョンのビルドをします。 次の手順、SetupAPI ログ記録レベルを変更します。

1.  テストするクリーン ビルドのインストールを開始します。

2.  テキスト モードのセットアップ後の最初の起動時にセットアップ プロセスを停止 (つまり、フル インストール モードに設定)。

3.  ブート メニューから選択して、ビルドを起動し、管理者としてログオンします。

4.  レジストリ ハイブ (ファイル) を記載*d:\\Winnt\\System32\\config*します。ここでのレジストリ ハイブを変更する必要があります*Software.sav*します。

5.  Windows 2000 では、実行*Regedt32*「ローカル コンピューターの HKEY_LOCAL_MACHINE」ウィンドウの選択および HKEY_LOCAL_MACHINE キーを選択します。 をクリックし、**レジストリ**メニュー選択し、**ハイブの読み込み**します。

    Windows xp 以降を実行*RegEdit*します。 HKEY_LOCAL_MACHINE を強調表示をクリックして、**ファイル**メニュー選択し、**ハイブの読み込み**します。

6.  ファイルを参照して選択*d:\\Winnt\\System32\\config\\software.sav*します。 キー名が表示されたら、"_sw.sav"を入力します。

7.  Hkey_local_machine _sw.sav キーを開き、次のキーを強調表示します。

    ```cpp
    HKEY_LOCAL_MACHINE_sw.sav\Microsoft\Windows\CurrentVersion\Setup
    ```

    Windows 2000 では、をクリックして、**セキュリティ**メニューの **権限**管理者にフル コントロールを付与します。

    Windows xp 以降、**編集**メニューの **アクセス許可**、し、管理者にフル コントロールを付与します。

8.  Windows 2000 でのクリックを使用してこのキーの下で必要なレジストリ値を追加**編集**選択**値の追加**します。

    Windows xp 以降、**編集**選択**新しい DWORD 値**します。

    値を入力します。 たとえば、"0 xffff"を追加する完全な詳細なログ記録を有効にします。

9.  HKEY_LOCAL_MACHINE を選択します。\\_sw.sav、および、ハイブのアンロード (を使用して、**レジストリ**Windows 2000 では、[] メニューまたは**ファイル**] メニューの [Windows XP 以降) _sw.sav キーは表示されなくなります。

10. コピー *d:\\Winnt\\System32\\config\\software.sav*に*d:\\Winnt\\System32\\config\\ソフトウェア*します。

11. 再起動し、セットアップを続行します。

12. この変更を確認するには、フル インストール モードのセットアップでは、shift キーを押しながら F10 キーを押して、実行*regedit.exe*とログ記録レベルを確認します。

 

 





