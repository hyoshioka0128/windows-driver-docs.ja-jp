---
title: AFM ファイルを NTF ファイルに変換する
description: AFM ファイルを NTF ファイルに変換する
ms.assetid: 5c6c8843-c1b8-4cbd-81db-8a54cc377020
keywords:
- ミニドライバー WDK Pscript、して変換します。
- NTF ファイル
- .ntf ファイル
- .afm ファイル
- して
- NTF ファイルに変換します。
- Adobe フォント メトリック WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85f56bc39fdb6c712edb85abd0a97a54c0dbe48d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574200"
---
# <a name="converting-afm-files-to-ntf-files"></a>AFM ファイルを NTF ファイルに変換する





Windows 2000 以降、Adobe フォント メトリックを (*AFM*) .ntf ファイルにファイルを変換する必要があります。 Makentf.exe、という名前をこの変換を実行するためのコマンド ライン ツールには、Windows ドライバー開発キット (DDK) とが指定されています。

1 つまたは複数の .afm ファイルを変換するには、次のコマンド構文を使用します。

**makentf** {**-win32**|**-win64**} **** \[**-v**\] **** \[**-o**\] **** <em>NTF\_FileName</em>**.ntf** *AFM\_FileNames*

場所*NTF\_ファイル名*、生成される .ntf ファイルの名前を指定し、 *AFM\_ファイル名*変換する 1 つ以上の AFM ファイルのセットです。

次のコマンド ライン オプションがサポートされています。

<a href="" id="-win32"></a>**-win32**  
Win32 のドライバーに対して NTF ファイルを作成します。 このコマンド ライン オプションが指定されている場合 **-win64**は指定できません。

<a href="" id="-win64"></a>**-win64**  
Win64 ドライバー NTF ファイルを作成します。 このコマンド ライン オプションが指定されている場合 **-win32**は指定できません。

<a href="" id="-v"></a>**-v**  
詳細。 このオプションは、生成される NTF ファイルの構造体のテキスト形式で表示を格納しているコマンドの出力ストリームを作成します。

<a href="" id="-o"></a>**-o**  
西ヨーロッパ言語の標準グリフ セットを省略します。 既定では、Makentf.exe には、.ntf ファイルを生成するときに、西ヨーロッパ言語の標準グリフ セットが含まれます。 .Ntf の複数のファイルを作成する場合、すべてのファイルが一緒に使用する限り、ファイルのいずれかで、西ヨーロッパ言語のグリフを含めるだけでかまいませんを設定します。 たとえば、Roman フォント メトリックを含む 1 つ .ntf ファイルおよび日本語フォント メトリックを含む別に作成するいるとします。 次のコマンドを使用する場合があります。

```cpp
makentf -win32 roman.ntf roman1.afm roman2.afm roman3.afm
makentf -win32 -o jpn.ntf jpn1.afm jpn2.afm jpn3.afm
```

これらのファイルをまとめて使用する場合西グリフ セットの情報は常に得られる roman.ntf からは必要ありません jpn.ntf 内の情報を複製し、余分な領域を消費するため。 その一方で jpn.ntf を単独で、使用する場合に **-o**指定されていない必要があります。

2 番目のコマンド構文もサポートされて、次のように。

**makentf** *filename*

場所*filename*出力テキストを受け取るファイルの名前を指定します。 この構文では、PostScript グリフの名前と Makentf.exe に既知のコード ページごとに Unicode 値の一覧を含むファイルを作成する Makentf.exe が原因です。

PSFamily.dat、追加のファイルは、WDK で提供され、Makentf.exe を含む同じディレクトリに存在する必要があります。 これは、表示、各フォント ファミリ名と Makentf.exe を提供するテキスト ファイルです。

標準 .afm ファイルを変換することができます、前に、次のような行を追加する必要があります。

```cpp
Comment UniqueID IDnumber
```

場所*id 番号:* フォント ベンダーによって発行されたフォントの一意の識別子を表します。

Makentf.txt には、いくつかの追加の .map とするのと同じディレクトリ内に存在する必要があります .ps ファイルが必要です東アジア フォントの .afm ファイルを処理しているときに **-o** PSFamily.dat とします。 追加の .map と (PSFamily.dat) と WDK で提供される、.ps ファイルは、フォントの Unicode コードから CID へのマッピング テーブルを作成するために必要なは。 詳細については、[東アジア言語 AFM ファイルの変換を NTF ファイル](converting-east-asian-afm-files-to-ntf-files.md)を参照してください。

.Ntf ファイルに変換される .afm ファイルに含めることができます、 **FontBBox2**キーワード。 このキーワードの引数がの場合と同様**FontBBox** (を参照してください、 *Adobe フォント メトリック ファイル形式の仕様*、Adobe Systems, Inc. から) ことを除いて、 **FontBBox2**引数を指定する設定 (約) などの特定の文字で使用されるグリフの境界ボックス中**FontBBox**引数が .afm ファイルで説明されているすべての文字の和集合の境界ボックスについて説明します。 場合**FontBBox2**が検出されなければ、指定された値**FontBBox**境界ボックスのために使用します。

 

 




