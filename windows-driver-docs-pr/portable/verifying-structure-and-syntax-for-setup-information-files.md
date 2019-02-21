---
Description: Verifying Structure and Syntax for Setup Information Files
title: セットアップ情報ファイルの構造と構文を確認しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b90b8eab6a30fa8cfe43b42bb955a769410c44ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538560"
---
# <a name="verifying-structure-and-syntax-for-setup-information-files"></a>セットアップ情報ファイルの構造と構文を確認しています


Windows Driver Kit (WDK) には、一連の ChkINF ツールとして参照される Perl スクリプトが用意されています。 これらのスクリプトは、構造体とセットアップ情報 (.inf) ファイルの構文を確認します。 これらのスクリプトの詳細については、WDK ドキュメントのドライバーの開発ツール セクションを参照してください。

WPD のすべての .inf ファイルには、UMDF 共同インストーラーを呼び出す必要があります。 つまりたびに CoInstallers セクションが宣言を\[CopyFiles\]ディレクティブが存在する必要があります。 ドライバーは、その他の共同インストーラーのバイナリは必要ありません (および CopyFiles ディレクティブが必要ない) 場合、空の CopyFiles セクションを宣言してから CoInstallers セクション内で参照する、要件を満たすことができます。

 

 




