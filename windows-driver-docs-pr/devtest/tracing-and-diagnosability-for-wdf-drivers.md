---
title: トレースと診断の WDF ドライバー
description: このホワイト ペーパーでは、Windows Driver Foundation (WDF) ドライバーでは、Windows ソフトウェア トレース プリプロセッサ (WPP) を使用してイベントのトレースを実装する方法について説明します。
ms.assetid: C89A218F-3E73-4D3E-8F53-5D52E97711EF
ms.date: 07/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ccf50f665a9025c01bfbc5f9cb3657a578c0110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548650"
---
# <a name="tracing-and-diagnosability-for-wdf-drivers"></a>トレースと診断の WDF ドライバー


**最終更新日。**

-   2008 年 10 月 19 日

**適用対象します。**

-   Windows Server 2008
-   Windows Vista
-   Windows Server 2003
-   Windows XP
-   Windows 2000

このホワイト ペーパーでは、Windows Driver Foundation (WDF) ドライバーでは、Windows ソフトウェア トレース プリプロセッサ (WPP) を使用してイベントのトレースを実装する方法について説明します。

ファイル名:WPP\_intro.docx

169 KB

Microsoft Word ファイル

[Office ファイル ビューアーを入手します。](http://www.microsoft.com/download/office.aspx)

[![ここをクリックしてダウンロードするには](./images/download.png)](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WPP_intro.docx)

ドライバー ソフトウェア トレースで Event Tracing for Windows (ETW)、カーネル モードとユーザー モードの両方のプロセスのトレース メッセージを記録するカーネル レベルの機能は、通常基づきます。 ETW なを使用するという複雑なので、ほとんどのドライバー開発者は、簡素化し、ETW トレース用のドライバーをインストルメント化のプロセスを強化する Windows ソフトウェア トレース プリプロセッサ (WPP) を使用します。

## <a name="in-this-white-paper"></a>このホワイト ペーパー。

-   WPP ソフトウェア トレースの基礎
-   トレース メッセージの関数とマクロ
-   ドライバーでのソフトウェア トレースのサポート
-   ソフトウェア トレースするためのツール
-   ソフトウェア トレース セッションを実行する方法

 

 





