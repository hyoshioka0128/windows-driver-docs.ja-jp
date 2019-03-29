---
title: 印刷 Web ページの ActiveX オブジェクト
description: 印刷 Web ページの ActiveX オブジェクト
ms.assetid: 85c37895-542f-4399-bf87-517eaab99a09
keywords:
- Web ページ、WDK ActiveX オブジェクトを印刷します。
- Web ページの WDK プリンター、ActiveX オブジェクト
- カスタマイズされた Web ページ WDK、ActiveX オブジェクトの印刷
- ActiveX オブジェクト WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a624e6915d133ca9bae9dcbd91ec7a3971ea766
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581047"
---
# <a name="activex-objects-for-print-web-pages"></a>印刷 Web ページの ActiveX オブジェクト





次の 3 つの ActiveX オブジェクト[Iasphelp](https://msdn.microsoft.com/library/windows/hardware/ff550742)、 [IOleCvt](https://msdn.microsoft.com/library/windows/hardware/ff551819)、および[ISNMP](https://msdn.microsoft.com/library/windows/hardware/ff554396)、Web ページの印刷は提供されています。 ASP ファイルは VBScript などのスクリプト言語を使用して、オートメーション インターフェイスでは、各オブジェクトにアクセスできます。 オブジェクトとインターフェイスは、Oleprn.dll で実装されます。

次の一覧には、各インターフェイスの簡単な説明が含まれています。

-   [Iasphelp オートメーション インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff550742)指定したプリンターに関連付けられているプロパティを取得することができます。

    このインターフェイスは、ページが呼び出されたもの以外のプリンターに関する情報を取得する ASP ページ、ASP セッション変数からご利用いただけませんで情報へのアクセスを提供します。

-   [IOleCvt オートメーション インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff551819)文字列を ANSI から Unicode に変換することができ、その逆の場合、文字列を UTF8 の形式に変換して、Unicode に変換する文字列を異なるコード ページを使用します。

-   [ISNMP オートメーション インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554396)設定し、プリンターの RFC 1759 がサポートされている場合は、SNMP の Oid に関連付けられている値を取得することができます。

    [ISNMP](https://msdn.microsoft.com/library/windows/hardware/ff554396)インターフェイスは、Microsoft の著しく IP/ポート モニターを使用するプリンターでのみ使用できます。 このインターフェイスは、SNMP 管理 API 関数の OLE オートメーション ラッパー基本的にです。 これらの関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

    オブジェクトの数値の文字列を使用して Id (Oid) を指定することができ、テキストを含めることでは、RFC 1759 で指定された名前の文字列の管理情報ベース (MIB)。 追加の MIB 名できます定義、コンパイル、および、カスタマイズされた (mib) をインストールする場合、Windows SDK ドキュメントの説明に従って。

ActiveX と自動化については、Windows SDK のドキュメントを参照してください。

 

 




