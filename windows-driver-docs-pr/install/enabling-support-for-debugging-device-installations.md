---
title: デバイスのインストールのデバッグのサポートの有効化
description: デバイスのインストールのデバッグのサポートの有効化
ms.assetid: cc47b4c9-fd1d-47c2-9af9-0b7f4a7a918a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d52e1c40e423ef11048e05427e44de9fcb735c2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357835"
---
# <a name="enabling-support-for-debugging-device-installations"></a>デバイスのインストールのデバッグのサポートの有効化


以降、Windows Vista では、プラグ アンド プレイ (PnP) マネージャー、システムで新しいデバイスを検出した場合、オペレーティング システムの起動時、デバイスのインストールのホスト プロセス (*DrvInst.exe*) を検索し、デバイスのドライバーをインストールします。

オペレーティング システムが提供するデバイスのインストールのホスト プロセスのデバッグのサポートの種類を設定するには、作成 (または変更)、次[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)デバッグするターゲット システム上のレジストリ値。

**HKEY_LOCAL_MACHINE\\ソフトウェア\\Microsoft\\Windows\\CurrentVersion\\デバイス インストーラー\\DebugInstall**

次の表に、デバッグのサポートを使用して指定されている型、 **DebugInstall**レジストリ値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DebugInstall 値</th>
<th align="left">デバッグのサポート</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>デバイスのインストール プロセスは、ユーザー モード デバッガーを使用してデバッグされます。 詳細については、次を参照してください。<a href="debugging-device-installations-with-a-user-mode-debugger.md" data-raw-source="[Debugging Device Installations with a User-mode Debugger](debugging-device-installations-with-a-user-mode-debugger.md)">ユーザー モード デバッガーでのデバイス インストールのデバッグ</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>デバイスのインストール プロセスは、カーネル デバッガー (KD) を使用してデバッグされます。 詳細については、次を参照してください。 <a href="debugging-device-installations-with-the-kernel-debugger--kd-.md" data-raw-source="[Debugging Device Installations with the Kernel Debugger (KD)](debugging-device-installations-with-the-kernel-debugger--kd-.md)">Kernel Debugger (KD) でのデバイス インストールのデバッグ</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>デバイスのインストール プロセスのデバッグ。 これは、場合の既定のサポート<strong>DebugInstall</strong>がレジストリに存在しません。</p></td>
</tr>
</tbody>
</table>

 

後に、 **DebugInstall**レジストリ値の設定をデバッグするターゲット システムを再起動する必要はありません。 ただし、 **DebugInstall**値が 0 に設定されるまで、次のデバイスのインストールとそれ以降のデバイスのインストールごとに有効なままの開始前にレジストリ値を設定する必要があります。

**注**  をリセットすることを確認する、 **DebugInstall**レジストリ値を 0 (または値を削除します)、ターゲット システムでデバイスのインストールをデバッグする必要が不要になったとすぐにします。

 

 

 





