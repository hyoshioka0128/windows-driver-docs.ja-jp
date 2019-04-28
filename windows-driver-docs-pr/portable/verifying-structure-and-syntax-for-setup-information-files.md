---
Description: セットアップ情報ファイルの構造と構文の確認
title: セットアップ情報ファイルの構造と構文の確認
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b90b8eab6a30fa8cfe43b42bb955a769410c44ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370440"
---
# <a name="verifying-structure-and-syntax-for-setup-information-files"></a>セットアップ情報ファイルの構造と構文の確認


Windows Driver Kit (WDK) には、一連の ChkINF ツールとして参照される Perl スクリプトが用意されています。 これらのスクリプトは、構造体とセットアップ情報 (.inf) ファイルの構文を確認します。 これらのスクリプトの詳細については、WDK ドキュメントのドライバーの開発ツール セクションを参照してください。

WPD のすべての .inf ファイルには、UMDF 共同インストーラーを呼び出す必要があります。 つまりたびに CoInstallers セクションが宣言を\[CopyFiles\]ディレクティブが存在する必要があります。 ドライバーは、その他の共同インストーラーのバイナリは必要ありません (および CopyFiles ディレクティブが必要ない) 場合、空の CopyFiles セクションを宣言してから CoInstallers セクション内で参照する、要件を満たすことができます。

 

 




