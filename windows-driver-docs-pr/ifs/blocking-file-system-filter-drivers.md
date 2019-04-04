---
title: 従来のファイル システム フィルター ドライバーをブロック
description: 以降で Windows 10 version 1607 では、管理者およびドライバー開発者が使用できますレジストリ設定従来のファイル システム フィルター ドライバーをブロックします。
ms.assetid: 90A562FB-D616-4D38-8D4F-7EFCDF9E617F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9069f8556b9bb888400ec47d4e048c0e3d1e2ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553494"
---
# <a name="blocking-legacy-file-system-filter-drivers"></a>従来のファイル システム フィルター ドライバーをブロック

以降で Windows 10 version 1607 では、管理者およびドライバー開発者が使用できますレジストリ設定従来のファイル システム フィルター ドライバーをブロックします。 *従来のファイル システム フィルター ドライバー*はファイル システムに接続されているドライバー スタックを直接とフィルター マネージャーを使用しないでください。 このトピックでは、ブロックとブロック解除のレガシ ファイル システム フィルター ドライバーのレジストリ設定について説明します。 従来のファイル システム フィルターがブロックされたときに、システム イベント ログに入力されたイベントと従来のファイル システム ドライバーが実行されている OS を確認する方法についても説明します。

<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>を参照してください。 ミニフィルター ドライバーは従来、ドライバーを移植するには、<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>を参照してください。
</div>
 

## <a name="span-idhowtoblocklegacydriversspanspan-idhowtoblocklegacydriversspanspan-idhowtoblocklegacydriversspanhow-to-block-legacy-drivers"></a><span id="How_to_block_legacy_drivers"></span><span id="how_to_block_legacy_drivers"></span><span id="HOW_TO_BLOCK_LEGACY_DRIVERS"></span>従来のドライバーをブロックする方法


使用して、 **IoBlockLegacyFsFilters**レジストリ キーをシステムが従来のファイル システム フィルター ドライバーをブロックするかどうかを指定します。 ブロックされると、すべてのレガシ ファイル システム フィルター ドライバーの読み込みがブロックされます。 レジストリ変更を有効にするには、システムの再起動を実行します。

次のレジストリ パス、レジストリ キーを作成する必要があります。

``` syntax
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\I/O System
```

有効な DWORD の値を**IoBlockLegacyFsFilters**キーは、次のとおり。

| **IoBlockLegacyFsFilters**値 | 説明                                                                                       |
|----------------------------------|---------------------------------------------------------------------------------------------------|
| **1**                            | 従来のファイル システム フィルター ドライバーは、読み込みまたは記憶域ボリュームへのアタッチからブロックされます。       |
| **0**                            | 従来のファイル システム フィルター ドライバーはブロックされません。 このリリースでは、既定の動作です。 |

 

これは、キーがどのようにレジストリ エディターで。

![ioblocklegacyfsfilters レジストリ キーを編集します。](images/ioblockregkey.png)

## <a name="span-idexamplewhenalegacydriverisblockedfromloadingspanspan-idexamplewhenalegacydriverisblockedfromloadingspanspan-idexamplewhenalegacydriverisblockedfromloadingspanexample-when-a-legacy-driver-is-blocked-from-loading"></a><span id="Example__when__a_legacy_driver_is_blocked_from_loading"></span><span id="example__when__a_legacy_driver_is_blocked_from_loading"></span><span id="EXAMPLE__WHEN__A_LEGACY_DRIVER_IS_BLOCKED_FROM_LOADING"></span>例: 従来のドライバーがブロックされた場合の読み込み


**エラー**イベントは、システム イベント ログに記録から読み込み、従来のファイル システム フィルター ドライバーがブロックされたときに次のようにします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント プロパティ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ログの名前</td>
<td align="left">System</td>
</tr>
<tr class="even">
<td align="left">Source</td>
<td align="left">Microsoft-Windows-Kernel-IO</td>
</tr>
<tr class="odd">
<td align="left">日付</td>
<td align="left">2015 年 12 月 29 日午後 2時 55分: 05</td>
</tr>
<tr class="even">
<td align="left">イベント ID</td>
<td align="left">1205</td>
</tr>
<tr class="odd">
<td align="left">タスク カテゴリ</td>
<td align="left">なし</td>
</tr>
<tr class="even">
<td align="left">レベル</td>
<td align="left">エラー</td>
</tr>
<tr class="odd">
<td align="left">キーワード</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ユーザー</td>
<td align="left">CONTOSO\user</td>
</tr>
<tr class="odd">
<td align="left">コンピューター</td>
<td align="left">user.domain.corp.contoso.com</td>
</tr>
<tr class="even">
<td align="left">説明</td>
<td align="left">従来のファイル システム フィルターをブロックするには、Windows が構成されます。 フィルター名: \Driver\sfilter</td>
</tr>
</tbody>
</table>

 

## <a name="span-idhowtocheckiflegacydriversarerunningspanspan-idhowtocheckiflegacydriversarerunningspanspan-idhowtocheckiflegacydriversarerunningspanhow-to-check-if-legacy-drivers-are-running"></a><span id="How_to_check_if_legacy_drivers_are_running"></span><span id="how_to_check_if_legacy_drivers_are_running"></span><span id="HOW_TO_CHECK_IF_LEGACY_DRIVERS_ARE_RUNNING"></span>従来のドライバーが実行されているかどうかを確認する方法


フィルターのレガシ ファイル システム フィルター ドライバーをまたは実行していないことを確認する不明な場合は、次を実行できます。

**従来のファイル システム フィルター ドライバーを実行しているかどうかを確認するには**

1.  右クリックし、管理者特権でコマンド プロンプトを開き、 **cmd.exe**アイコンをクリックすると**管理者として実行**します。
2.  種類: `fltmc filters`
3.  従来のドライバーを探して、これらは、あるものを**フレーム**の値**&lt;レガシ&gt;** します。

この例で AVLegacy EncryptionLegacy、という、従来のファイル システム フィルター ドライバーが付いて、 **&lt;レガシ&gt;** フレームの値。 AVMiniFilter という名前のファイル システム ドライバーがない、 **&lt;レガシ&gt;** ミニフィルター ドライバー (は直接接続、ファイル システム スタックにないと、フィルター マネージャーを使用) であるフレームの値。

``` syntax
C:\Windows\system32>fltmc filters
 
Filter Name                     Num Instances    Altitude    Frame
------------------------------  -------------  ------------  -----
AVLegacy                                        389998.99   <Legacy>
EncryptionLegacy                                149998.99   <Legacy>
AVMiniFilter                           3        328000         0
```

従来のファイル システム フィルター ドライバーをブロックした後に引き続きレガシ ドライバーが実行されている場合は、設定した後、システムを再起動するように、 **IoBlockLegacyFsFilters**レジストリ キー。 設定には、再起動後はなりません。

システムのレガシ ファイル システム フィルター ドライバーの場合、ファイル システム ドライバーのミニフィルターのバージョンを取得するそれぞれの Isv を使用します。 フィルター マネージャー モデルを使用するミニフィルター ドライバーへのレガシ ファイル システム フィルター ドライバーの移植方法の詳細については、[レガシ フィルター ドライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)を参照してください。

 

 




