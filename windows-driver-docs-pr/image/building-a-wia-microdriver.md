---
title: WIA マイクロドライバーの作成
description: WIA マイクロドライバーの作成
ms.assetid: dcec3079-2844-4d87-b2e4-0c1850118192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fe2bdb19ccc7141c2a32cf72b7305339d2207ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373321"
---
# <a name="building-a-wia-microdriver"></a>WIA マイクロドライバーの作成





すべての WIA microdrivers では、次のヘッダー ファイルとライブラリ ファイルが必要です。

### <a name="header-files"></a>ヘッダー ファイル

WIA microdrivers のすべてでは、次の表に表示されるヘッダー ファイルを含める必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ヘッダー ファイル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>wiamicro.h</em></p></td>
<td><p>関数プロトタイプと WIA microdriver を必要とする構造体を定義します。</p></td>
</tr>
</tbody>
</table>

 

WIA microdrivers には、追加のヘッダー ファイルが必要です。 必要なヘッダーは、デバイスの種類および実装されている機能に依存します。 これらの要件については、リファレンス セクションで説明します。

### <a name="library-files"></a>ライブラリ ファイル

WIA には、次の表に示すようにライブラリ ファイルが使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ライブラリ ファイル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>wiaguid.lib</em></p></td>
<td><p>エクスポートはクラス id (Clsid) とインターフェイス識別子 (Iid) です。 すべての WIA microdrivers では、このライブラリが必要です。</p></td>
</tr>
</tbody>
</table>

 

WDK ビルド環境で*Include*と*Lib*ディレクトリは検索パス内の最初のディレクトリである必要があります。 これにより、ヘッダーとライブラリ ファイルの最新バージョンを使用していること。

**注**  のログ記録をオンにする microdriver を構築するときに、Visual C 6.0 でログを使用する場合は、 *Wiafbdrv.dll*を使用して、 *Wialogcfg.exe*に付属するプログラムWindows Me Driver Development Kit (DDK)。 また、microdriver 名が正しいことを確認する INF ファイルを確認します。 INF の確認、 **DeviceData** MicroDriver セクション ="自分のユーザー名。DLL"です。

 

 

 




