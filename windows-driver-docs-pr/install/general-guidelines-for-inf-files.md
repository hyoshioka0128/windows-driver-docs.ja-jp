---
title: INF ファイルの一般的なガイドライン
description: INF ファイルの一般的なガイドライン
ms.assetid: a0394708-46ed-47f8-a629-0c7d3088df3b
keywords:
- INF ファイル WDK デバイス インストールでは、一般的なガイドライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 788d55c9f1a0c810da0d0952cdf56d9f6fe40f51
ms.sourcegitcommit: a5cbd86f3019a54ba6425999b651d6ef8bd29937
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2019
ms.locfileid: "57693059"
---
# <a name="general-guidelines-for-inf-files"></a>INF ファイルの一般的なガイドライン




INF ファイルには多くの共通部分があり、次の構文規則の 1 つのセットです。 ただし、さまざまな Microsoft Windows でサポートされているデバイスとは異なるはも。 INF ファイルを作成するときに、次の情報源を参照してください。

-   このセクションで、 [INF ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)資料を参照します。

-   デバイスのクラスのドキュメントです。

    たとえば、デバイスがプリンターの場合は、表示[のインストールと構成のプリンター ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff551648)します。

-   INF ファイル用のツールを WDK です。

    詳細については、[INF ファイル用のツール](https://msdn.microsoft.com/library/windows/hardware/ff552956)を参照してください。 これらのツールに含まれる、 \\WDK の Tools サブディレクトリ。

-   サンプルの INF ファイルと類似したデバイスの INF ファイル。

    WDK には、そのサンプル ドライバーの INF ファイルが含まれています。 デバイスのようなデバイスの INF ファイルがあるかどうかを確認するサンプル ドライバーを探します。

作成したり、改行の挿入を制御できます任意のテキスト エディターを使用して、INF ファイルを変更することができます。 INF に非 ASCII 文字が含まれている場合は、Unicode ファイルとしてファイルを保存します。

INF ファイルを Windows 7 に付属し、以前のオペレーティング システムのファイル名をいる必要があります<em>xxxxxxxx</em>**.inf**ここで、"*xxxxxxxx*"が 8 文字を超えていません。 オペレーティング システムから個別に付属する INF ファイルの名前は 8 文字に制限されています。

Windows 8 以降、INF ファイル名は 8 文字に制限されていますかに関係なく場合、オペレーティング システムを出荷します。

任意に変更しないで、INF ファイルのタイムスタンプ、バージョン管理メカニズムとして。 指定された日、バージョン番号に基づいて INF ファイルのバージョン管理する必要があります、 [ **INF バージョン セクション**](inf-version-section.md)します。

## <a name="best-practices-for-naming-and-versioning-your-inf-file"></a>名前付けのベスト プラクティスとバージョン管理、INF ファイル

- INF 名は、他のベンダーから Inf との競合が発生する可能性を削減する方法で名前必要があります。  たとえば、INF 名前が考えられますが、プレフィックスまたはサフィックスとして会社名の省略形。
- 文字列や設定などのブランド化などの側面で異なる同じドライバー パッケージの 2 つの異なるバリエーションがある場合は、これらの 2 つのドライバー パッケージは一意の名前が必要です。
- INF を更新するたびに、または、INF ファイルの参照を日時、INF でバージョンを更新する必要があります。
 





