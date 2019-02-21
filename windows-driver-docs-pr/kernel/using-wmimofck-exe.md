---
title: Wmimofck.exe を使用します。
description: Wmimofck.exe を使用します。
ms.assetid: cbf735c4-1c0d-4ff3-8a5c-b9d1de84bca4
keywords:
- WMI の WDK カーネル、Wmimofck.exe ユーティリティ
- Wmimofck.exe ユーティリティ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1733c154eb9cd68e167d352bd414149c73315412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558407"
---
# <a name="using-wmimofckexe"></a>Wmimofck.exe を使用します。





Wmimofck.exe ユーティリティは、Windows Driver Kit (WDK) に含まれています。 このアプリケーションは、入力によって生成された MOF ファイル (.bmf ファイル) のバイナリ、 [MOF コンパイラ](compiling-a-driver-s-mof-file.md)(mofcomp.exe)。 クラス、プロパティ、メソッドおよび .bmf ファイルで指定されたイベントが WMI を使用するために有効である Wmimofck.exe が確認されます。 Wmimofck.exe は、次のファイルを生成できるもです。

-   C 言語ヘッダー ファイル (.h ファイル) ヘッダー ファイルの MOF の定義との同期を維持するために使用されます。

-   C の言語のソースのドライバーの WMI コード スタブを含むファイル。

-   16 進数のバージョンの実行時に動的な MOF データを提供するためのドライバー ソースに含まれる .bmf データ。

-   VBScript または HTML でのアプリケーション テンプレートをテストします。

実行する、 **wmimofck**ユーティリティでは、次の構文を使用します。

**wmimofck** \[  **-h * * * filename* \[ **-m** \] \[ **-u** \] \] \[* *-c * * * filename* \] \[ **-x * **filename* \] \[** -t***filename *\] \[* *-w***ディレクトリ*\] \[* - yfilename*\] \[*- zfilename *\]

場合、 **-h**パラメーターを指定すると、Guid、データ構造、および MOF ファイルに指定されたメソッドのインデックスを定義する C 言語のヘッダー ファイルを作成します。 呼び出し元が指定されている場合、 **-m**フラグを同様に、ヘッダー ファイルが入力と各 WMI メソッドの出力の構造体の定義が含まれます。 既定では、 *wmimofck*可変長のプロパティが含まれている WMI クラスのメンバーの定義を生成しません。 呼び出し元が指定されている場合 **-u**、し*wmimofck*を指定する文字列プロパティを含む、固定サイズを持つすべてのプロパティのメンバーの定義が生成されます、 **MaxLen**修飾子。 場合、 **-t**パラメーターを指定すると、VBScript プログラムが作成されたすべてのデータ ブロックと MOF ファイルで指定したプロパティがクエリを実行します。

場合、 **-x** MOF のバイナリ データのテキスト表現を含むテキスト ファイルが作成されたパラメーターを指定します。 ドライバーがドライバーのイメージ ファイル上のリソースではなく、WMI クエリを使用してバイナリ MOF をレポート作成をサポートしている場合、ドライバーのソースに含めることができます。

場合、 **-c**パラメーターが指定されて、デバイス ドライバーの WMI コードを実装するためのテンプレートが含まれる C 言語のソース ファイルが生成されます。

場合、 **-w**パラメーターを指定すると、HTML ファイルのセットが生成される WMI データ ブロックへのアクセスに使用できる基本的な UI を作成します。

**-Y**と **-z**フラグを組み合わせて使用するだけです。 **と y**言語に依存しない WMI クラスの宣言を含むファイルを指定し、 **~ z**特定の言語のクラスの修正を指定します。 コマンドは、 *wmimofck localizedfile* **と y * * * mof* **~ z * * * mfl*マージ、 *mof*と*mfl* MOF ファイルの完全なローカライズされたバージョンを形成するファイル。 参照してください[構築およびローカライズされた MOF ファイルを展開する](building-and-deploying-the-localized-mof-file.md)詳細についてはします。

 

 




