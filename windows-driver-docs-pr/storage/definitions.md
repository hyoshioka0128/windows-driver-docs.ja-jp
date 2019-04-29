---
title: 定義
description: 定義
ms.assetid: 904b7dd3-472d-4286-81c1-2af1109e2139
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07c043d0f4f095dccf25c714c34f17e553cc5a70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392751"
---
# <a name="definitions"></a>定義


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IEEE 1667</p></td>
<td align="left"><p>標準プロトコルのセキュリティで保護された認証とセキュリティで保護されたホストと、直接接続されている一時的な記憶域デバイス (TSD)、USB フラッシュ ドライブ、ポータブル ハード ドライブ、または携帯電話などの間の信頼の作成。"</p>
<p>詳細については、次を参照してください。<a href="https://standards.ieee.org/standard/1667-2018.html">検出、認証、およびホストの添付ファイルの記憶域デバイスでの承認の IEEE 1667 2018-IEEE 標準</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1667 認証サイロ</p></td>
<td align="left"><p>1667 サイロ関数を持つデバイス、デバイスからホスト、またはその両方のホストのいずれかの認証を提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1667 標準認証サイロ</p></td>
<td align="left"><p>標準証明書またはパスワード認証サイロを Microsoft が配布ドライバー基本 1667 仕様で定義されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1667 USB フラッシュ デバイス (UFD)</p></td>
<td align="left"><p>USB デバイスの設定、IEEE 1667 仕様に従った 1667 コマンドの実装をフラッシュします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>サード パーティの認証サイロ</p></td>
<td align="left"><p>サイロの認証機能を実装する指定の標準的な認証サイロを 1667 の基本セットで定義されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>サード パーティ製のサイロ</p></td>
<td align="left"><p>1667 のセットに含まれていないサイロはサイロの標準を指定します。 関数は、専用および IEEE 1667 基本標準に記載されていません。 「不明」のサイロと呼ばれるにあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>アドレス指定可能なコマンド ターゲット (ACT)</p></td>
<td align="left"><p>1667 コマンドを受け取り、必要に応じて (論理ユニットを参照してください)、ユーザー データへのアクセスを提供するアクセスの独立した単位。 1667 仕様に従って、ACT はユーザーのデータ アクセス機能を提供する必要はありません。 1667 デバイスは、1 つまたは複数の機能を実装することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>認証</p></td>
<td align="left"><p>いずれかが要求した id の信憑性を検証する機能が、ホストを使用する (とそれに関連する IEEE 1667) またはデバイス。 パスワード認証の場合、デバイスのユーザーが確立されているシークレットのパスワードは資格情報をこの目的を果たします。 証明書認証の場合、ペアの公開キーで暗号化されたバイトの乱数ストリームに正常に暗号化を解除して、秘密キーを所有しているを実証する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Authorization</p></td>
<td align="left"><p>後、デバイス管理のリソースへの concomitant のアクセスが承認されたか、ホスト id が認証されていることを示す値。 ホストからデバイスへの認証はデバイスからホストへの認証が成功した認証、デバイスとホスト間で接続されているデータ チャネルは、関連付けられている、ACT のユーザー データ部分への承認アクセスを制御します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>証明書サイロ (証明書サイロ)</p></td>
<td align="left"><p>認証の基礎として証明書と関連付けられている公開/秘密キー ペアを使用する認証サイロです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>大容量記憶装置レガシ (またはレガシ UFD)</p></td>
<td align="left"><p>1667 コマンドを実装しない、USB 大容量記憶装置 (または USB フラッシュ デバイス) を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>論理ユニット (LUN)</p></td>
<td align="left"><p>ホスト システム上の 1 つのディスクとして公開されているデバイスに含まれるユーザー データのアクセス許可の独立した単位。 LUN は、承認された状態で現在データ方位 1667 ACT と同義です。</p>
<p>いくつか Ufd は複数の LUN に対応します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>パスワードのサイロ (PW サイロ)</p></td>
<td align="left"><p>パス フレーズの認証の基本として一致を使用して認証サイロです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>リムーバブル メディア ビット (RMB)</p></td>
<td align="left"><p>少し SCSI 問い合わせコマンドに対するデバイスの応答に含まれているメディアが取り外し可能かどうかを示すを (0x12) (RMB = 1) または固定 (RMB = 0)。 PDO がホット プラグ可能なデバイスを表すかどうかを示すために使用 DEVICE_CAPABILITIES のリムーバブル フィールドと混同しないように RMB はデバイス自体ではなく、メディアのプロパティを表します。 どの RMB のメディア = 1 の扱いは、システムによって RMB でメディアを表示するよりも 0 を = です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>サイロ</p></td>
<td align="left"><p>1667 コマンドに応答する独立した機能単位。 各機能を 1 つまたは複数のサイロをアタッチすることがあります。 1667 サイロのコマンドは、ACT の特定のインデックスとインデックスのサイロにアドレス指定することがあります。</p></td>
</tr>
</tbody>
</table>

 

 

 




