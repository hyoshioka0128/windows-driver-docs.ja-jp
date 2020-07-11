---
title: 拡張機能 INF ファイルテンプレートの使用
description: 拡張機能 INF テンプレートの使用方法について説明します。
ms.topic: article
ms.localizationpriority: medium
ms.date: 06/12/2020
ms.openlocfilehash: 7a15d1b449fc3c7a2238662b4ac094b2ebc700f7
ms.sourcegitcommit: 5148f4ff682a2d9cdf5eafdb76e13400331f5660
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2020
ms.locfileid: "86273191"
---
# <a name="using-an-extension-inf-file-template"></a>拡張機能 INF ファイルテンプレートの使用

このページでは、拡張機能の INF テンプレートを使用して、拡張性を向上させる方法について説明します。

拡張機能 INF テンプレートは、デバイス製造元 (IHV) が別のドライバーパッケージで公開するというコメントが付いた拡張 INF です。 通常、IHV は、基本 INF からオプション機能を分離し、拡張機能の INF テンプレートに格納します。 このテンプレートでは、IHV は、システムビルダー (OEM) がコメント解除および変更できるエントリを示すコメントと、コメントを解除できるが変更する必要のないエントリを提供します。  次に、OEM はこのテンプレートを開始点として使用して、拡張機能の INF を作成します。

テンプレートに基づいて拡張機能の INF を作成するには、「[拡張機能 inf を作成](using-an-extension-inf-file.md#creating-an-extension-inf)する」のガイダンスに従って、ページの下部にある例を参照してください。

テンプレートに基づく新しい拡張機能の INF を送信するには、 [Dua プロセス](https://docs.microsoft.com/windows-hardware/test/hlk/user/create-a-driver-only-update-package)を使用します。

> [!NOTE]
> OEM が DUA プロセスを使用して、IHV が提供する基本 INF を変更する場合、基本 INF の所有権は OEM に移ります。 代わりに、OEM は IHV に連絡し、適切な拡張機能が基本 INF に追加されることを要求するか、または IHV が拡張機能の INF テンプレートを提供する必要があります。

また、IHV は、拡張機能の INF テンプレートを使用して、既に公開されているドライバーパッケージにオプション機能を追加する場合もあります。 ベース INF を更新するのではなく、テンプレートを発行することによって、既存の拡張機能の Inf が引き続き動作するようにすることができます。 次のシーケンスは、これがどのように機能するかを示しています。

1. IHV は、新しい省略可能な値を拡張機能 INF テンプレートに追加しますが、ベース INF には追加しません。
2. IHV は、新しいレジストリ値が存在するかどうかを確認するために、基本ドライバーにコードを追加します。
    * 更新されたベースドライバで新しい値が見つかると、新しい機能が使用されます。
    * それ以外の場合は、以前の機能が使用されます。
3. OEM は、拡張機能 INF テンプレートを使用して、新しい値を設定する新しい拡張機能 INF を作成します。

代わりに、IHV がベース INF を更新することを決定した場合は、「[拡張機能 INF ファイルの使用](using-an-extension-inf-file.md#backward-compatibility)」で説明されているガイドラインに従ってください。

## <a name="related-topics"></a>関連トピック

* [拡張 INF ファイルの使用](using-an-extension-inf-file.md)
* [パートナー センターでの拡張 INF の使用](../dashboard/submit-dashboard-extension-inf-files.md)
