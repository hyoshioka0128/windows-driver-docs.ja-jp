---
title: プラグ アンド プレイ デバイス
description: ESRT 構成テーブルの存在は、ファームウェア リソースごとに個別の PnP デバイス インスタンスを列挙するために Windows にリダイレクトされます。
ms.assetid: 85EE32E7-1871-490D-9FF6-07E0891C78E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beb3b3ebb01f4e364af2ec95be235fa9ce294de6
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161360"
---
# <a name="plug-and-play-device"></a>プラグ アンド プレイ デバイス


ESRT 構成テーブルの存在は、ファームウェア リソースごとに個別の PnP デバイス インスタンスを列挙するために Windows にリダイレクトされます。 照合目的でドライバーの場合は、ファームウェア リソース デバイスは、ハードウェア Id では、ファームウェアの ID の GUID を埋め込むによって一意に識別します。 ESRT 例を参照する[ESRT テーブル定義](esrt-table-definition.md)デバイスの対応するインスタンスを列挙します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイス インスタンス ID</th>
<th>Hardware ID (ハードウェア ID)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UEFI\RES_ {SYSTEM_FIRMWARE} \0</td>
<td><p>UEFI\RES_ {SYSTEM_FIRMWARE} &AMP; REV_1</p>
<p>UEFI\RES_ {SYSTEM_FIRMWARE}</p></td>
</tr>
<tr class="even">
<td>UEFI\RES_{DEVICE_FIRMWARE}\0</td>
<td><p>UEFI\RES_ {DEVICE_FIRMWARE} &AMP; REV_1</p>
<p>UEFI\RES_ {DEVICE_FIRMWARE}</p></td>
</tr>
</tbody>
</table>

 

2 つのハードウェア Id が、各ファームウェア リソース デバイスによって報告されることに注意してください。最初のハードウェア ID にはに 2 つ目はありません、現在のファームウェア リソースのバージョンが含まれます。 リソースのファームウェアのバージョンは、ファームウェア更新プログラムの適用の結果として変更される予定です、ことが重要にすべてのユーザーをすべてのファームウェア リソース バージョン間でのインストールには適用ができるように、2 つ目の解除でバージョン管理されたハードウェア ID の対象とドライバー現在インストールされているバージョンに関係なく、特定のシステムで提示します。

## <a name="related-topics"></a>関連トピック
[ESRT テーブルの定義](esrt-table-definition.md)  
[更新プログラムのドライバー パッケージの作成](authoring-an-update-driver-package.md)  
[更新プログラムの処理](processing-updates.md)  
[UEFI 環境からデバイス I/O](device-i-o-from-the-uefi-environment.md)  
[シームレスな危機防止と回復](seamless-crisis-prevention-and-recovery.md)  
[ファームウェアの更新状態](firmware-update-status.md)  



