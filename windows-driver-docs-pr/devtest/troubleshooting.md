---
title: メタデータ作成ウィザードのトラブルシューティング
description: メタデータ作成ウィザードのトラブルシューティング
ms.assetid: EBAF4289-DA23-4FFE-8CC0-DD21021CBA86
keywords:
- メタデータ作成ウィザードのトラブルシューティング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c58d733fc51ca7e808ac5f558f0ffbacba9daa97
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769588"
---
# <a name="troubleshooting-the-metadata-authoring-wizards"></a>メタデータ作成ウィザードのトラブルシューティング


\[このトピックでは、Windows Driver Kit (WDK) 8 に用意されているデバイスメタデータ Authoring tool について説明します。 Windows 8.1 用のデバイスエクスペリエンスを開発している場合は、 [Microsoft Visual Studio 2013 および Windows Driver Kit (WDK) 8.1](https://www.microsoft.com/download/details.aspx?id=42273)で使用できるデバイスメタデータ作成ウィザードを使用します。 \]

次のいずれかのエラーメッセージが表示された場合は、表の解決列を参照して問題を解決してください。

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
<td align="left">メタデータ作成ウィザード</td>
<td align="left">ようこそ</td>
<td align="left">エラー: フォルダーの場所を指定してください</td>
<td align="left">フォルダーパスを入力してください。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">ようこそ</td>
<td align="left">エラー: FolderLocation. テキストフォルダーが存在しません</td>
<td align="left">ファイルパスを修正してください。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">ようこそ</td>
<td align="left">選択されたファイルは存在しません</td>
<td align="left">ファイルのパスまたは名前を修正してください。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">ようこそ</td>
<td align="left">XML ファイルエラー</td>
<td align="left"><p>XML エラーを修正します。</p>
<p>エラーの例:</p>
<ul>
<li>はの最初の子をにする必要がありました {0} {1} が、代わりにが見つかりました {2} 。</li>
<li>の後にを指定する必要がありました {0} {1} が、代わりにが見つかりました {2} 。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">[完了]</td>
<td align="left">パッケージの作成に失敗しました:</td>
<td align="left"><p>指示に基づいてパラメーターを変更します。</p>
<p>エラーの例:</p>
<ul>
<li>デバイスの ModelName を指定する必要があります (ロケール {0} )</li>
<li>このパッケージは、少なくとも1つの HardwareID または ModelID に関連付ける必要があります</li>
<li>このデバイスのプライマリカテゴリを指定する必要があります</li>
</ul>
<p>警告の例:</p>
<ul>
<li>ModelNumber ( {0} ) が指定されていません</li>
<li>DeviceDescription 2 ( {0} ) が指定されていません</li>
<li>汎用アイコンは、プライマリカテゴリの選択によって決定されます。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">関連付け</td>
<td align="left">無効な形式: "Value"-先頭と末尾に {} を追加しないでください。</td>
<td align="left">を削除し {} て、もう一度やり直してください。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">関連付け</td>
<td align="left">無効な GUID 形式: "Value"</td>
<td align="left">正しい GUID を入力して、もう一度やり直してください。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">アイコン</td>
<td align="left">アイコンファイルに問題がありました。 "エラーメッセージ" アイコンの検証エラー</td>
<td align="left">アイコンが見つからないか、コントロールパネルの [デバイスとプリンター] に表示される要件を満たしていません。 アイコンを見つけて修正し、もう一度やり直してください。
<p>エラーの例:</p>
<ul>
<li>エラー: Image 256x256 の透明度を設定する必要があります。</li>
<li>エラー: Image 48 x 48:32 ビット以上のアルファは存在しません。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">送信ウィザード</td>
<td align="left">メタデータパッケージの選択</td>
<td align="left">リストにその名前のパッケージが既に存在します</td>
<td align="left">デバイスメタデータパッケージの新しい GUID を作成します。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">メタデータパッケージの選択</td>
<td align="left">パッケージの読み込み中に問題が発生しました:</td>
<td align="left">指示に基づいてパラメーターを変更します。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">[完了]</td>
<td align="left">送信パッケージの作成で問題が発生しました:</td>
<td align="left">指示に基づいてパラメーターを変更します。</td>
</tr>
</tbody>
</table>

 

 

 





