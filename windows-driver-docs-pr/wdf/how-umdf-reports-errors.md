---
title: UMDF がエラーを報告する方法
description: このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) がエラーを報告する方法について説明します。 両方の UMDF バージョン 1 と 2 に適用されます。
ms.assetid: 44e4e5df-d968-4973-8a36-e93c75320ff6
keywords:
- ユーザー モード ドライバー フレームワーク WDK のエラー
- UMDF WDK、エラー
- ユーザー モード ドライバー WDK UMDF、エラー
- エラー WDK UMDF
- Windows エラー報告の WDK UMDF
- WER WDK UMDF
- エラー報告の WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ca2c3fd39ea7ebe57309f5bfc3721b7acb02b77
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538396"
---
# <a name="how-umdf-reports-errors"></a>UMDF がエラーを報告する方法


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) がエラーを報告する方法について説明します。 両方の UMDF バージョン 1 と 2 に適用されます。

UMDF ドライバーがクラッシュしたときに、フレームワークは、Windows エラー報告 (WER) レポートを作成します。

UMDF には、次の種類のエラーが報告されます。

-   [UMDF Verifier](using-umdf-verifier.md)エラー。

-   ホスト プロセスで未処理の例外。

-   ホスト プロセスが予期せず終了します。

-   エラーまたは重要な操作のタイムアウト。 タイムアウトの詳細については、[UMDF でホスト プロセスのタイムアウト](how-umdf-enforces-time-outs.md)を参照してください。

UMDF エラー レポートには、次の情報を含めることができます。 レポートの内容は、検出された問題に依存します。

-   ホスト プロセスのメモリ ダンプ

-   UMDF のトレース ログのコピー

-   構成については、デバイスは、デバイス名、製造元、インストールされているドライバーを含めることができます、およびドライバーのバイナリ バージョン

-   問題、ドライバー、フレームワークへの最後の呼び出しの (またはその逆) のアドレスを含めることができる問題のあるコード、例外情報の分析

 

 





