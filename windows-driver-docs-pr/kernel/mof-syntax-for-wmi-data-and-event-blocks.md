---
title: WMI データ ブロックとイベント ブロックの MOF 構文
description: WMI データ ブロックとイベント ブロックの MOF 構文
ms.assetid: 247037b7-d62e-4f74-8fa4-57e74f6c412f
keywords:
- WMI の WDK カーネルでは、イベント ブロック
- イベントは、WDK の WMI をブロックします。
- WDK の WMI のデータ ブロックします。
- WMI の WDK カーネルでは、データのブロック
- WDK の WMI をブロックします。
- MOF ファイルの WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9afa4b343242215a3d724f37e4bcec3e6221413
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380310"
---
# <a name="mof-syntax-for-wmi-data-and-event-blocks"></a>WMI データ ブロックとイベント ブロックの MOF 構文





ドライバーの WMI スキーマには、ドライバーを提供できる、WMI の要求に応答を実行できるメソッドの情報を定義、そのデータ ブロックについて説明します。 ドライバーのスキーマには、そのイベント ブロックは、ドライバーにより決定されたイベントが発生すると、WMI クライアントのユーザーが通知を要求するには、WMI、ドライバーを送信するデータ ブロックであるも説明します。

ドライバーのライターでは、管理オブジェクト フォーマット (MOF) でドライバーのスキーマを定義します。 MOF は、デスクトップ管理タスク フォース (DMTF) によって作成され、インターフェイス定義言語 (IDL) に基づくコンパイル済みの言語です。 ドライバーの MOF ファイルには、データのブロックと、ドライバーは、WMI に公開するイベント ブロックごとに MOF クラスの定義が含まれています。

WMI データ ブロックの MOF クラス定義は、この構文を次に示します。

**\[** <em>必須および省略可能なクラスの修飾子</em> **\]**

**クラス * * * ClassName* :*OptionalBaseClass*
 **{** 
 **\[キーに、読み取り\]** 
**文字列 InstanceName;** 
 **\[読み取り\]** 
**ブール アクティブ;** 
 ** \[ ** *必須および省略可能なプロパティ修飾子* ** \] ** 
 <em>datatype itemname1</em>* *;* *
 ** \[ ** *必須および省略可能なプロパティ修飾子* ** \] ** 
 <em>datatype itemnameN</em> **;** 
 **};** 次のトピックには、前に示した構文要素がについて説明します。

[WMI クラスの修飾子](wmi-class-qualifiers.md)

[WMI クラス名と基本クラス](wmi-class-names-and-base-classes.md)

[WMI のクラスで必要な項目](required-items-in-wmi-classes.md)

[WMI プロパティ修飾子](wmi-property-qualifiers.md)

[ドライバーの定義の WMI データ項目](driver-defined-wmi-data-items.md)

[WMI クラスの例](wmi-class-examples.md)

MOF 構文の概要については、WMI クライアントおよびその他のアプリケーションに関連している Microsoft Windows SDK 参照してください。

 

 




