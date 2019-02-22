---
title: ソース管理システムを作成します。
description: ソース管理システムを作成します。
ms.assetid: 86492545-fc94-40ee-b22d-26fa2b0fbcc8
keywords:
- ソース サーバー、HTTP サイト
- ソース サーバー、UNC 共有
- SrcSrv、HTTP サイト
- SrcSrv、UNC 共有
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09c645663bc3fb568d10aa11932974d95817b144
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559861"
---
# <a name="creating-your-own-source-control-system"></a>ソース管理システムを作成します。


このセクションでは、SrcSrv をビルドまたはバージョン管理システムに統合できるように、インストルメンテーションのスクリプトを準備する方法を理解することができます。 実装は SrcSrv に付属する言語仕様のバージョンによって異なります。

さまざまなシンボル ハンドラーのコードで Srcsrv.dll の呼び出し方法の詳細に説明します。 ただし、この情報は、静的でない、将来のためになりません。 Srcsrv.dll を直接呼び出すコードを記述しようといない必要があります。 これは、DbgHelp または Visual Studio 製品の予約されています。 このような機能を自社製品に統合する必要があるサード パーティ ベンダーを使用する必要があります、 **SymGetSourceFile**関数。 DbgHelp API でその他のこの関数は、Windows のツールをデバッグ インストール ディレクトリの sdk のヘルプ/サブディレクトリにある DbgHelp ドキュメントでは、について説明します。

このセクションの内容:

[言語仕様 1](language-specification-1.md)

[言語仕様 2](language-specification-2.md)

 

 





