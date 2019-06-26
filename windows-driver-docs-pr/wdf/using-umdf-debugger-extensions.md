---
title: Wudfext.dll でのデバッガー拡張機能の概要
description: このトピックでは、WudfExt.dll で、特定のユーザー モード ドライバー フレームワーク (UMDF) ドライバーをデバッグに使用できるデバッガー拡張機能のコマンドについて説明します。
ms.assetid: af84ed3a-33a1-4736-9080-c43e87052064
keywords:
- WDK UMDF のデバッガー拡張機能
- WDK UMDF のデバッガー拡張機能
- 拡張機能の WDK デバッガー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99bf2a50ccc369298d5427a73c0b51e3d859ff08
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372170"
---
# <a name="summary-of-debugger-extensions-in-wudfextdll"></a>Wudfext.dll でのデバッガー拡張機能の概要


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Windows Driver Kit (WDK) には、という名前のデバッガー拡張機能ライブラリが含まれています。 *WudfExt.dll*、DDKROOT % である\\bin サブディレクトリ。 このトピックでは、デバッガー拡張機能のコマンドを説明します*WudfExt.dll*、ユーザー モード ドライバー フレームワーク (UMDF) バージョン 1 のデバッグに使用することができます。 *。x*ドライバー。

UMDF バージョン 2.0 以降 UMDF ドライバーをデバッグする必要があります代わりに使用する、 *Wdfkd.dll*デバッガー拡張機能ライブラリ。 詳細については、次を参照してください。 [ **Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)します。

内の各コマンドの詳細については*WudfExt.dll*を参照してください[ユーザー モード ドライバー フレームワークの拡張機能 (Wudfext.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-extensions--wudfext-dll-)します。 すべての利用可能なデバッガー拡張機能ライブラリの詳細についてで提供されるドキュメントを参照して、 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)パッケージ。

読み込み、 *WudfExt.dll*デバッガーの拡張機能ライブラリに、デバッガーのコマンド プロンプトで次のコマンドを入力します。

**! WudfExt.dll を読み込む**

WudfExt.dll の拡張機能ライブラリを提供する拡張機能のコマンドを次の表に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">拡張</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>! ヘルプ</strong></p></td>
<td align="left"><p>WudfExt.dll をサポートしているすべてのデバッガー拡張機能を示しています</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! umdevstacks</strong></p></td>
<td align="left"><p>ホスト プロセスですべてのデバイス スタックを示しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! umdevstack</strong></p></td>
<td align="left"><p>ホスト プロセスでデバイス スタックに関する情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! umirps</strong></p></td>
<td align="left"><p>ホスト プロセスで保留中の I/O 要求パケットの一覧を示しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! umirp</strong></p></td>
<td align="left"><p>ユーザー モードの I/O 要求パケットに関する情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfdriverinfo</strong></p></td>
<td align="left"><p>UMDF ドライバーに関する情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfdevicequeues</strong></p></td>
<td align="left"><p>デバイスのすべての I/O キューを示しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfqueue</strong></p></td>
<td align="left"><p>I/O キューに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfrequest</strong></p></td>
<td align="left"><p>I/O 要求に関する情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfobject</strong></p></td>
<td align="left"><p>WDF オブジェクトとその親と子のリレーションシップに関する情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfdevice</strong></p></td>
<td align="left"><p>プラグおよびプレイ (PnP) デバイスの電源管理の状態のシステムを示しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfdumpobjects</strong></p></td>
<td align="left"><p>WDF の未処理のオブジェクトの一覧を示しています。ドライバーをアンロードするときに、リークしているオブジェクトを決定するために使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfiotarget</strong></p></td>
<td align="left"><p>状態と送信した要求の一覧を含む、I/O ターゲットに関する情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudffile</strong></p></td>
<td align="left"><p>Framework ファイルに関する情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! umfile</strong></p></td>
<td align="left"><p>UMDF についての情報を表示<a href="creating-a-file-object-to-handle-i-o.md" data-raw-source="[intra-stack file](creating-a-file-object-to-handle-i-o.md)">スタック内のファイル</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudffilehandletarget</strong></p></td>
<td align="left"><p>ファイル ハンドル ベースの I/O ターゲットに関する情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfusbtarget</strong></p></td>
<td align="left"><p>USB I/O ターゲットに関する情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfusbinterface</strong></p></td>
<td align="left"><p>USB インターフェイス オブジェクトに関する情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfusbpipe</strong></p></td>
<td align="left"><p>USB パイプ オブジェクトに関する情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfrefhist</strong></p></td>
<td align="left"><p>Framework のオブジェクトの数の履歴を参照して示しています</p></td>
</tr>
</tbody>
</table>

 

 

 





