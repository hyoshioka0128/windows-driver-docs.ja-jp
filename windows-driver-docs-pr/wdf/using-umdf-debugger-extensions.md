---
title: Wudfext.dll でのデバッガー拡張機能の概要
description: このトピックでは、特定のユーザーモードドライバーフレームワーク (UMDF) ドライバーをデバッグするために使用できる、WudfExt dll のデバッガー拡張機能コマンドについて説明します。
ms.assetid: af84ed3a-33a1-4736-9080-c43e87052064
keywords:
- UMDF デバッガー拡張機能 WDK
- デバッガー拡張機能 WDK UMDF
- 拡張機能の WDK デバッガー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06a0092e1619c1e4e111c805ac6cfe832e09ab5d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210864"
---
# <a name="summary-of-debugger-extensions-in-wudfextdll"></a>Wudfext.dll でのデバッガー拡張機能の概要


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

Windows Driver Kit (WDK) には、 *Wudfext .dll*という名前のデバッガー拡張ライブラリが含まれています。これは、% DDKROOT%\\bin サブディレクトリにあります。 このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) バージョン1をデバッグするために使用できる、 *Wudfext dll*のデバッガー拡張コマンドについて説明します。*x*ドライバー。

Umdf バージョン2.0 以降の UMDF ドライバーをデバッグするには、代わりに、 *Wdfkd*デバッガー拡張機能ライブラリを使用する必要があります。 詳細については、「 [**Windows Driver Framework Extensions (Wdfkd .dll)**](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)」を参照してください。

*Wudfext dll*の各コマンドの詳細については、「[ユーザーモードドライバーフレームワーク拡張 (wudfext .dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-extensions--wudfext-dll-)」を参照してください。 使用可能なすべてのデバッガー拡張機能ライブラリの詳細については、 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)パッケージに付属のドキュメントを参照してください。

*Wudfext*デバッガー拡張機能ライブラリを読み込むには、デバッガーのコマンドプロンプトで次のコマンドを入力します。

**! WudfExt .dll を読み込みます。**

次の表は、WudfExt .dll 拡張ライブラリに用意されている拡張コマンドをまとめたものです。

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
<td align="left"><p>WudfExt がサポートするすべてのデバッガー拡張機能を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! umdevstacks</strong></p></td>
<td align="left"><p>ホストプロセス内のすべてのデバイススタックを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! umdevstack</strong></p></td>
<td align="left"><p>ホストプロセスのデバイススタックに関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! umirps</strong></p></td>
<td align="left"><p>ホストプロセス内の保留中の i/o 要求パケットの一覧を表示します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! umirp</strong></p></td>
<td align="left"><p>ユーザーモード i/o 要求パケットに関する情報を表示します</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfdriverinfo</strong></p></td>
<td align="left"><p>UMDF ドライバーに関する情報を表示します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfdevicequeues</strong></p></td>
<td align="left"><p>デバイスのすべての i/o キューを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfqueue</strong></p></td>
<td align="left"><p>I/o キューに関する情報を表示します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfrequest</strong></p></td>
<td align="left"><p>I/o 要求に関する情報を表示します</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfobject</strong></p></td>
<td align="left"><p>WDF オブジェクト、およびその親と子のリレーションシップに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfdevice</strong></p></td>
<td align="left"><p>デバイスのプラグアンドプレイ (PnP) と電源管理の状態システムを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfdumpobjects</strong></p></td>
<td align="left"><p>未処理の WDF オブジェクトの一覧を表示します。ドライバーのアンロード時にリークしたオブジェクトを特定するために使用されます</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! wudfiotarget</strong></p></td>
<td align="left"><p>I/o ターゲットに関する情報を表示します。これには、送信された要求の状態や一覧などが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudffile</strong></p></td>
<td align="left"><p>フレームワークファイルに関する情報を表示します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! umfile</strong></p></td>
<td align="left"><p>UMDF の<a href="creating-a-file-object-to-handle-i-o.md" data-raw-source="[intra-stack file](creating-a-file-object-to-handle-i-o.md)">スタック内のファイル</a>に関する情報を表示します</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudffilehandletarget</strong></p></td>
<td align="left"><p>ファイルハンドルベースの i/o ターゲットに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfusbtarget</strong></p></td>
<td align="left"><p>USB i/o ターゲットに関する情報を表示します</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfusbinterface</strong></p></td>
<td align="left"><p>USB インターフェイスオブジェクトに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfusbpipe</strong></p></td>
<td align="left"><p>USB パイプオブジェクトに関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! wudfrefhist</strong></p></td>
<td align="left"><p>フレームワークオブジェクトの参照カウントの履歴を表示します</p></td>
</tr>
</tbody>
</table>

 

 

 





