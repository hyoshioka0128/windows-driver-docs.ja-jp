---
title: ストレージ カーネル デバッガー拡張機能
description: 記憶域のカーネル デバッガーの拡張機能 (storagekd) は、Windows 8 以降のオペレーティング システム (OS) のターゲットの記憶装置ドライバーをデバッグするために使用されます。
ms.assetid: 8EF83BC8-6ABB-496C-98A6-EF0298D78F76
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fe9018af0a2906d22c742a78b249d5a4ba8a0ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335517"
---
# <a name="storage-kernel-debugger-extensions"></a>ストレージ カーネル デバッガー拡張機能


記憶域のカーネル デバッガーの拡張機能 (storagekd) は、Windows 8 以降のオペレーティング システム (OS) のターゲットの記憶装置ドライバーをデバッグするために使用されます。

マネージ classpnp ストレージ クラス ドライバーを使用して、記憶装置ドライバーと管理 Storport 記憶域ミニポート ドライバーでは、デバッグするために役立つ拡張機能のコマンドが記載**Storagekd.dll**します。

参照してください[SCSI ミニポート拡張 (Scsikd.dll および Minipkd.dll)](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md) Windows 7 と以前のバージョンの OS のターゲットのニーズをデバッグします。

**重要な**  特殊記号この拡張機能を使用する必要があります。 詳細については、「 [Windows 用デバッグ ツールのダウンロードとインストール](index.md)」を参照してください。

 

## <a name="span-idstoragekerneldebuggerextensioncommandsspanspan-idstoragekerneldebuggerextensioncommandsspanspan-idstoragekerneldebuggerextensioncommandsspanstorage-kernel-debugger-extension-commands"></a><span id="Storage_kernel_debugger_extension_commands"></span><span id="storage_kernel_debugger_extension_commands"></span><span id="STORAGE_KERNEL_DEBUGGER_EXTENSION_COMMANDS"></span>記憶域カーネル デバッガー拡張コマンド


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storhelp"></span><span id="_STORAGEKD.STORHELP"></span><strong><a href="-storagekd-storhelp.md" data-raw-source="[!storagekd.storhelp](-storagekd-storhelp.md)">!storagekd.storhelp</a></strong></p></td>
<td align="left"><p>ヘルプのテキストを表示します<strong>Storagekd.dll</strong>拡張コマンド。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storclass"></span><span id="_STORAGEKD.STORCLASS"></span><strong><a href="-storagekd-storclass.md" data-raw-source="[!storagekd.storclass](-storagekd-storclass.md)">!storagekd.storclass</a></strong></p></td>
<td align="left"><p>指定した情報が表示されます<em>classpnp</em>デバイス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storadapter"></span><span id="_STORAGEKD.STORADAPTER"></span><strong><a href="-storagekd-storadapter.md" data-raw-source="[!storagekd.storadapter](-storagekd-storadapter.md)">!storagekd.storadapter</a></strong></p></td>
<td align="left"><p>指定した情報が表示されます<em>Storport</em>アダプター。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storunit"></span><span id="_STORAGEKD.STORUNIT"></span><strong><a href="-storagekd-storunit.md" data-raw-source="[!storagekd.storunit](-storagekd-storunit.md)">!storagekd.storunit</a></strong></p></td>
<td align="left"><p>指定した情報が表示されます<em>Storport</em>論理ユニットです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storloglist"></span><span id="_STORAGEKD.STORLOGLIST"></span><strong><a href="-storagekd-storloglist.md" data-raw-source="[!storagekd.storloglist](-storagekd-storloglist.md)">!storagekd.storloglist</a></strong></p></td>
<td align="left"><p>表示、 <em>Storport</em>アダプターの内部のログ エントリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storlogirp"></span><span id="_STORAGEKD.STORLOGIRP"></span><strong><a href="-storagekd-storlogirp.md" data-raw-source="[!storagekd.storlogirp](-storagekd-storlogirp.md)">!storagekd.storlogirp</a></strong></p></td>
<td align="left"><p>表示、 <em>Storport の</em>IRP が提供されているアダプターの内部のログ エントリをフィルターします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storlogsrb"></span><span id="_STORAGEKD.STORLOGSRB"></span><strong><a href="-storagekd-storlogsrb.md" data-raw-source="[!storagekd.storlogsrb](-storagekd-storlogsrb.md)">!storagekd.storlogsrb</a></strong></p></td>
<td align="left"><p>表示されます、 <em>Storport の</em>アダプターの内部のログ エントリがストレージ (または SCSI) のフィルター処理された要求ブロック (SRB) 提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storsrb"></span><span id="_STORAGEKD.STORSRB"></span><strong><a href="-storagekd-storsrb.md" data-raw-source="[!storagekd.storsrb](-storagekd-storsrb.md)">!storagekd.storsrb</a></strong></p></td>
<td align="left"><p>指定されたストレージ (または SCSI) に関する情報を表示します。 ブロックの要求 (SRB)。</p></td>
</tr>
</tbody>
</table>

 

 

 





