---
title: CVS の使用
description: CVS の使用
ms.assetid: 4ad1202e-0be5-4adc-af8b-6b8d7cb34b04
keywords:
- 同時実行バージョンのシステム (CVS)
- ソース サーバー、CVS
- SrcSrv、CVS
- 同時実行バージョン システム (CVS), 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3a916e4bfc75dd7e68edc42c42fc0a4f2b555e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371583"
---
# <a name="using-cvs"></a>CVS の使用


移行元サーバーの CVS モジュールは、同時実行バージョン システム (CVS) 1.11.17 (クライアント) を使用して開発されました。 CVS の他のバージョンでテストされていません。 さらに、モジュールの現在のバージョンは、ベータ版です。

### <a name="span-idcvsrootspanspan-idcvsrootspancvsroot"></a><span id="cvsroot"></span><span id="CVSROOT"></span>CVSROOT

インデックス ビルドのソースをコンピューター CVSROOT はパスワードとユーザーの情報を含めることはできません。 Cvs.exe を使用して、資格情報を設定します。

準備する、 [Srcsrv.ini](the-srcsrv-ini-file.md)ファイルのインデックスを作成する CVS が一意に、ネットワーク内の他と区別する、リポジトリのエイリアスを入力する必要があります。 このリポジトリは、環境内で CVSROOT の値に一致する必要があります。 ソースのインデックス付きの .pdb ファイルにエイリアスが定義されているため、デバッガーのクライアントを使用して維持する Srcsrv.ini のコピーでこの値を設定する必要はありません。

### <a name="span-idclientcomputerspanspan-idclientcomputerspanclient-computer"></a><span id="client_computer"></span><span id="CLIENT_COMPUTER"></span>クライアント コンピューター

CVS サンド ボックスまたは CVSROOT セットは、デバッグ中にファイルを抽出するクライアント コンピューターは必要はありません。 CVS バイナリ パスが、これは必要し、リポジトリがロックされている場合、ユーザー名と Cvs.exe でパスワードを設定する必要があります。

### <a name="span-idrevisiontagsspanspan-idrevisiontagsspanrevision-tags"></a><span id="revision_tags"></span><span id="REVISION_TAGS"></span>リビジョンのタグ

CVS はそのバージョン番号でのファイルを抽出できません。 代わりに、実行する必要がありますを使用する何と呼ばれますが、*タグ*します。 CVS ベースのシステムをインデックス作成時に、すべての変更がリポジトリにチェックインされ、「cvs タグ」コマンドを使用してタグを適用し、ことを確認する必要があります。 次に、ファイルをインデックス作成時に確実に"label"コマンド ライン パラメーターを使用してインデックスを作成するビルドに関連付けるタグを指定します。 CVS を設定して同じ結果を得ることができます\_環境内のラベル。 その他の値は、環境またはコマンドラインから設定できます。 使用して、 **-[概要] タブ** コマンド ライン オプション SSIndex で選択内容を調べ、すべてが正しく構成されたことを確認します。

```console
ssindex.cmd -system=cvs -??
```

 

 





