---
title: WDF ドライバーのトレースと診断能力
description: このホワイトペーパーでは、windows Driver Foundation (WDF) ドライバーで Windows ソフトウェアトレースプリプロセッサ (WPP) を使用してイベントトレースを実装する方法について説明します。
ms.assetid: C89A218F-3E73-4D3E-8F53-5D52E97711EF
ms.date: 07/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa261ba4cdef22bcd966f5fef5e8bb157b97a04d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208902"
---
# <a name="tracing-and-diagnosability-for-wdf-drivers"></a>WDF ドライバーのトレースと診断能力


**最終更新日時:**

-   2008年10月19日

**適用対象:**

-   Windows Server 2008
-   Windows Vista
-   Windows Server 2003
-   Windows XP
-   Windows 2000

このホワイトペーパーでは、windows Driver Foundation (WDF) ドライバーで Windows ソフトウェアトレースプリプロセッサ (WPP) を使用してイベントトレースを実装する方法について説明します。

ファイル名: WPP\_の概要 .docx

169 KB

Microsoft Word ファイル

[Office ファイルビューアーを取得する](https://www.microsoft.com/download/office.aspx)

[![ダウンロードするにはここをクリック](./images/download.png)](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WPP_intro.docx)

ドライバーのソフトウェアトレースは、通常、カーネルモードとユーザーモードの両方のプロセスのトレースメッセージを記録するカーネルレベルのファシリティである Windows イベントトレーシング (ETW) に基づいています。 ETW は使用するには少し複雑になる可能性があるため、ほとんどのドライバー開発者は、Windows ソフトウェアトレースプリプロセッサ (WPP) を使用します。これにより、ETW トレース用のドライバーをインストルメント化するプロセスが簡素化され、強化されます。

## <a name="in-this-white-paper"></a>このホワイトペーパーは次のとおりです。

-   WPP ソフトウェアのトレースの基礎
-   トレースメッセージの関数とマクロ
-   ドライバーでのソフトウェアトレースのサポート
-   ソフトウェアのトレース用ツール
-   ソフトウェアトレースセッションを実行する方法

 

 





