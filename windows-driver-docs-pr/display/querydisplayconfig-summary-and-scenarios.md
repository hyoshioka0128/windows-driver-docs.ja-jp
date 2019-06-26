---
title: QueryDisplayConfig の概要とシナリオ
description: QueryDisplayConfig の概要とシナリオ
ms.assetid: a556b3d7-3cac-49b1-99db-7ce8a844a8a8
keywords:
- Windows 7 の WDK の表示、CCD Api、QueryDisplayConfig 接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD Api、QueryDisplayConfig 接続が表示されます。
- Windows 7 の WDK の表示、CCD Api、QueryDisplayConfig 構成が表示されます。
- 構成するには、WDK Windows Server 2008 R2 の表示、CCD Api、QueryDisplayConfig が表示されます。
- CCD WDK Windows 7 の概念の表示、QueryDisplayConfig
- CCD 概念 WDK Windows Server 2008 R2 の表示、QueryDisplayConfig
- QueryDisplayConfig WDK Windows 7 の表示
- QueryDisplayConfig WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8277fbb50d5ea0177fa7b8e93bc7a175280dbbf2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385049"
---
# <a name="querydisplayconfig-summary-and-scenarios"></a>QueryDisplayConfig の概要とシナリオ


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次のセクションでは、呼び出し元が使用する方法をまとめると、 [ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) CCD 関数を使用するためのシナリオを提供**QueryDisplayConfig**します。

### <a name="span-idquerydisplayconfigsummaryspanspan-idquerydisplayconfigsummaryspanquerydisplayconfig-summary"></a><span id="querydisplayconfig_summary"></span><span id="QUERYDISPLAYCONFIG_SUMMARY"></span>QueryDisplayConfig の概要

呼び出し元が使用できる[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)の次の情報を列挙します。

-   すべての現在の一連の可能な個々 のパスには、モニターが接続されています。 呼び出し元では、可能なトポロジを構築するパスを組み合わせることができます、します。

-   すべての現在アクティブなパス。

-   アクティブなパスと接続されるディスプレイの設定の永続性データベースで現在定義されています。

-   ソースとターゲットのパスごとに、向き、スケーリング、レイアウト、およびコネクタの種類と共にモードです。

-   現在のトポロジをマップするホット キー オプション。

### <a name="span-idquerydisplayconfigscenariosspanspan-idquerydisplayconfigscenariosspanquerydisplayconfig-scenarios"></a><span id="querydisplayconfig_scenarios"></span><span id="QUERYDISPLAYCONFIG_SCENARIOS"></span>QueryDisplayConfig シナリオ

[**QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)は、次のシナリオで呼び出されます。

-   表示のコントロール パネル アプレット呼び出し[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)を初回起動時に、コントロール パネルに現在適用されているトポロジを使用した、コントロール パネルのユーザー インターフェイスを設定します。 現在適用されているトポロジには、強制の投影を有効にするこれらの表示が含まれています。

-   表示のコントロール パネル アプレット呼び出し[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)のすべての設定可能なパスを列挙するために、 **multimon** ボックスの一覧。

-   表示がホット キーの呼び出しで、コントロール パネルのユーザー インターフェイスが開始する前に[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)現在設定されている (つまりは、複製、内部、外部、または拡張) の表示オプションを取得します。

-   サード パーティ製アプリケーションが呼び出す可能性があります[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)接続されるディスプレイ一連のデータベースに格納されている現在の設定をクエリします。

 

 





