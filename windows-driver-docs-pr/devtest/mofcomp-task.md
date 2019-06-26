---
title: Mofcomp タスク
description: Windows Driver Kit (WDK) には、MSBuld を使用してドライバーをビルドするときに、Mofcomp.exe ツールを実行できるようにの Mofcomp にタスクが用意されています。
ms.assetid: 94B70223-393F-49C9-B2C9-34FF64D26454
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bda7c120efa3c9850d5edc880461605c6066185
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363820"
---
# <a name="mofcomp-task"></a>Mofcomp タスク


Windows Driver Kit (WDK) には、MSBuld を使用してドライバーをビルドするときに、Mofcomp.exe ツールを実行できるようにの Mofcomp にタスクが用意されています。 ツールの詳細については、次を参照してください。 [ **mofcomp**](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)します。

MSBuild では、Mofcomp 項目を使用して、Mofcomp.exe を Mofcomp タスクのパラメーターを送信します。 Mofcomp の項目メタデータは、プロジェクト ファイルの Mofcomp を使用してアクセスします。

次の例では、.vcxproj ファイル内のメタデータを編集する方法を示します。

```XML
<ItemGroup>
    <Mofcomp Include="b.mof">
      <WMISyntaxCheck>true</WMISyntaxCheck>
    </Mofcomp>
</ItemGroup>
```

次の例は、コマンド ラインの呼び出しを示しています。

```
mofcomp.exe -WMI b.mof
```

この例では、WMI のスイッチを使用してファイル b.mof で mofcomp.exe を呼び出します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Mofcomp タスク パラメーター</th>
<th align="left">項目メタデータ</th>
<th align="left">ツールへの切り替え</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Sources</td>
<td align="left">@(Mofcomp)</td>
<td align="left"></td>
<td align="left">ITaskItem の必須パラメーターです。 ソース ファイルの一覧を指定します。</td>
</tr>
<tr class="even">
<td align="left">契約</td>
<td align="left">%(Mofcomp.Amendment)</td>
<td align="left"><strong>-修正:</strong><em>&lt;ロケール&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 MOF ファイルを、言語に依存しないバージョンと言語固有のバージョンに分割します。</td>
</tr>
<tr class="odd">
<td align="left">機関</td>
<td align="left">%(Mofcomp.Authority)</td>
<td align="left"><strong>A:</strong><em>&lt;機関&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 WMI へのログオン時に使う機関 (ドメイン名) として <Authority> を指定します。</td>
</tr>
<tr class="even">
<td align="left">自動バックアップ</td>
<td align="left">%(Mofcomp.AutoRecover)</td>
<td align="left"><strong>-autorecover</strong></td>
<td align="left">省略可能なブール型パラメーター。 指定した MOF ファイルを、リポジトリ回復時にコンパイルされるファイルの一覧に追加します。</td>
</tr>
<tr class="odd">
<td align="left">CreateBinaryMOFFile</td>
<td align="left">%(Mofcomp.CreateBinaryMOFFile)</td>
<td align="left"><strong>B:</strong><em>&lt;ファイル名&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 コンパイラが、WMI リポジトリに変更を加えずに名前のファイル名の MOF ファイルのバイナリ バージョンを作成を要求します。</td>
</tr>
<tr class="even">
<td align="left">LanguageNeutralOutput</td>
<td align="left">%(Mofcomp.LanguageNeutralOutput)</td>
<td align="left"><strong>-MOF:</strong><em>&lt;パス&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 言語に依存しない出力の名前です。</td>
</tr>
<tr class="odd">
<td align="left">LanguageSpecificOutput</td>
<td align="left">%(Mofcomp.LanguageSpecificOutput)</td>
<td align="left"><strong>-MFL:</strong><em>&lt;パス&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 言語固有の出力の名前です。</td>
</tr>
<tr class="even">
<td align="left">MinimalRebuildFromTracking</td>
<td align="left">%(Mofcomp.MinimalRebuildFromTracking)</td>
<td align="left"></td>
<td align="left">省略可能なブール型パラメーター。 True の場合、追跡対象のインクリメンタル ビルドが実行されます。それ以外の場合、再構築が実行されます。</td>
</tr>
<tr class="odd">
<td align="left">MOFClass</td>
<td align="left">% (Mofcomp.MOFClass)</td>
<td align="left"><ul>
<li><strong>-クラス:</strong><em>createonly</em></li>
<li><strong>-クラス:</strong><em>forceupdate</em></li>
<li><strong>-クラス:</strong><em>safeupdate</em></li>
<li><strong>-クラス:</strong><em>updateonly</em></li>
</ul></td>
<td align="left">省略可能な文字列パラメーター。 許可または禁止、作成または更新 MOF ファイル内のクラス。 ドキュメントを参照してクラス ファミリの詳細については、スイッチでします。</td>
</tr>
<tr class="even">
<td align="left">MOFInstance</td>
<td align="left">% (Mofcomp.MOFInstance)</td>
<td align="left"><ul>
<li><strong>インスタンス:</strong><em>createonly</em></li>
<li><strong>インスタンス:</strong><em>updateonly</em></li>
</ul></td>
<td align="left">省略可能な文字列パラメーター。 MOF ファイルのインスタンスの更新または作成できます。 ドキュメントを参照してください。 詳細については、スイッチのインスタンス ファミリでします。</td>
</tr>
<tr class="odd">
<td align="left">NamespacePath</td>
<td align="left">%(Mofcomp.NamespacePath)</td>
<td align="left"><strong>-N</strong><em>&lt;namespacepath&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 コンパイラが namespacepath として指定された名前空間に、MOF ファイルを読み込むことを要求します。</td>
</tr>
<tr class="even">
<td align="left">パスワード</td>
<td align="left">%(Mofcomp.Password)</td>
<td align="left"><strong>-P:</strong><em>&lt;パスワード&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 コンピューターのユーザー ログオン時に入力するパスワードとパスワードを指定します。</td>
</tr>
<tr class="odd">
<td align="left">ResourceLocale</td>
<td align="left">%(Mofcomp.ResourceLocale)</td>
<td align="left"><strong>-L</strong><em>&lt;ResourceLocale&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 -ER スイッチと組み合わせて使うと、MOF についてのローカライズされた説明テキストをバイナリ MOF から抽出します。</td>
</tr>
<tr class="even">
<td align="left">ResourceName</td>
<td align="left">%(Mofcomp.ResourceName)</td>
<td align="left"><strong>-ER:</strong><em>&lt;ResourceName&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 指定したリソースからバイナリ MOF を抽出します。</td>
</tr>
<tr class="odd">
<td align="left">SyntaxCheck</td>
<td align="left">%(Mofcomp.SyntaxCheck)</td>
<td align="left"><strong>-確認</strong></td>
<td align="left">省略可能なブール型パラメーター。 コンパイラが構文チェックだけを実行して適切なエラー メッセージを出力することを要求します。 このスイッチを使用して他のスイッチを使用しないできます。</td>
</tr>
<tr class="even">
<td align="left">ToolPath</td>
<td align="left">$(MofcompToolPath)</td>
<td align="left"></td>
<td align="left">省略可能な文字列パラメーター。 ツールがあるフォルダーへの完全パスを指定することができます。</td>
</tr>
<tr class="odd">
<td align="left">TrackerLogDirectory</td>
<td align="left">%(Mofcomp.TrackerLogDirectory)</td>
<td align="left"></td>
<td align="left">省略可能な文字列パラメーター。 書き込む tlog の追跡ツールのログ ディレクトリを指定します。</td>
</tr>
<tr class="even">
<td align="left">TrackFileAccess</td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
<td align="left">省略可能なブール型パラメーター。 True の場合は、このタスクのファイル アクセスのパターンを追跡します。</td>
</tr>
<tr class="odd">
<td align="left">UserName</td>
<td align="left">%(Mofcomp.UserName)</td>
<td align="left"><strong>-U:</strong><em>&lt;ユーザー名&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 ログオンしたユーザーの名前として、ユーザー名を指定します。</td>
</tr>
<tr class="even">
<td align="left">WMISyntaxCheck</td>
<td align="left">%(Mofcomp.WMISyntaxCheck)</td>
<td align="left"><strong>-WMI</strong></td>
<td align="left">省略可能なブール型パラメーター。 コンパイラが WMI 構文チェックを実行するように要求します。 -B: スイッチは、このスイッチを使用する必要があります。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**mofcomp**](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)

 

 






