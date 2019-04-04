---
title: メタデータ作成ウィザードのトラブルシューティング
description: メタデータ作成ウィザードのトラブルシューティング
ms.assetid: EBAF4289-DA23-4FFE-8CC0-DD21021CBA86
keywords:
- メタデータの編集ウィザードのトラブルシューティング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0121ffa85d2c0886a7195a95dc930cd6f32f223
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464332"
---
# <a name="troubleshooting-the-metadata-authoring-wizards"></a>メタデータ作成ウィザードのトラブルシューティング


\[このトピックでは、デバイス メタデータの Authoring tool で、Windows Driver Kit (WDK) 8 の提供について説明します。 Windows 8.1 のデバイス エクスペリエンスを開発する場合は、デバイス メタデータの作成ウィザードで使用可能なを使用して[Microsoft Visual Studio 2013 と Windows Driver Kit (WDK) 8.1](https://go.microsoft.com/fwlink/p/?LinkId=226411)します。 詳細については、[Windows 8.1 のデバイス エクスペリエンス](https://go.microsoft.com/fwlink/p/?linkid=325561)を参照してください。 \]

次のエラー メッセージを受信する場合は、テーブル内の問題を解決する解像度の列を参照します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">ツール</td>
<td align="left">画面</td>
<td align="left">エラー メッセージ</td>
<td align="left">解決方法</td>
</tr>
<tr class="even">
<td align="left">メタデータの作成ウィザード</td>
<td align="left">Welcome</td>
<td align="left">エラー:フォルダーの場所を指定する必要があります。</td>
<td align="left">フォルダーのパスを入力します。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Welcome</td>
<td align="left">エラー:FolderLocation.Text folder does not exist</td>
<td align="left">ファイルのパスを修正します。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Welcome</td>
<td align="left">選択したファイルが存在しません。</td>
<td align="left">ファイル パスまたは名前を修正します。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Welcome</td>
<td align="left">XML ファイルのエラー</td>
<td align="left"><p>XML エラーを修正します。</p>
<p>エラーの例:</p>
<ul>
<li>最初の子を予期していた{0}する{1}、されましたが、見つかった{2}代わりにします。</li>
<li>予期していた{0}が後に続く{1}、されましたが、見つかった{2}代わりにします。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">完了</td>
<td align="left">パッケージの作成に失敗しました。</td>
<td align="left"><p>指示に基づくパラメーターを変更します。</p>
<p>エラーの例:</p>
<ul>
<li>デバイスの ModelName が指定する必要があります (ロケール{0})</li>
<li>このパッケージを少なくとも 1 つの HardwareID または ModelID で関連付ける必要があります。</li>
<li>このデバイスの主なカテゴリを指定する必要があります。</li>
</ul>
<p>警告の例:</p>
<ul>
<li>"モデル番号"({0}) が指定されていません。</li>
<li>デバイス詳細 2 ({0}) が指定されていません。</li>
<li>汎用アイコンは、プライマリ カテゴリの選択によって決定されます。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">関連付け</td>
<td align="left">形式が無効です。「値」-、{} が、先頭と末尾に追加しないでください。</td>
<td align="left">削除、{}もう一度やり直してください。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">関連付け</td>
<td align="left">GUID の形式が無効です。"Value"</td>
<td align="left">正しい GUID を入力し、もう一度やり直してください。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Icon</td>
<td align="left">アイコン ファイルがある問題が発生しました。「エラー メッセージ」アイコンの検証エラー</td>
<td align="left">アイコンが見つからないか、デバイスとプリンターのコントロール パネルに表示される要件を満たしていません。 検索するか、アイコンを修正してもう一度やり直してください。
<p>エラーの例:</p>
<ul>
<li>エラー:256 x 256 の画像の透明度を設定する必要があります。</li>
<li>エラー:イメージの 48 48:32 ビット + アルファは存在しません。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">送信ウィザード</td>
<td align="left">メタデータ パッケージを選択します。</td>
<td align="left">一覧でその名前を持つパッケージが既にあります。</td>
<td align="left">デバイス メタデータ パッケージの新しい GUID を作成します。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">メタデータ パッケージを選択します。</td>
<td align="left">パッケージを読み込み中に問題が発生しました。</td>
<td align="left">指示に基づくパラメーターを変更します。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">完了</td>
<td align="left">提出パッケージの作成で問題が発生しました。</td>
<td align="left">指示に基づくパラメーターを変更します。</td>
</tr>
</tbody>
</table>

 

 

 





