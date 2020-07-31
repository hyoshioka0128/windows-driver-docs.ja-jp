---
title: WMI データ ブロックとイベント ブロックの MOF 構文
description: WMI データ ブロックとイベント ブロックの MOF 構文
ms.assetid: 247037b7-d62e-4f74-8fa4-57e74f6c412f
keywords:
- WMI WDK カーネル、イベントブロック
- イベントブロック WDK WMI
- データブロック WDK WMI
- WMI WDK カーネル、データブロック
- WDK WMI をブロックする
- MOF ファイル WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: db1dae96f39cc52881beb4fe55e0f4a4d832d2e4
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425728"
---
# <a name="mof-syntax-for-wmi-data-and-event-blocks"></a>WMI データ ブロックとイベント ブロックの MOF 構文





ドライバーの WMI スキーマでは、ドライバーが提供できる情報と、WMI 要求に応答して実行できるメソッドを定義するデータブロックが記述されています。 また、ドライバーのスキーマでは、イベントブロックも記述されています。これは、ドライバーによって特定されたイベントが発生したときに、ドライバーが WMI に送信するデータブロックです。これは、WMI クライアントユーザーが通知を要求した場合に発生します。

ドライバーライターは、管理オブジェクトフォーマット (MOF) でドライバーのスキーマを定義します。 MOF は、デスクトップ管理タスクフォース (DMTF) によって作成され、インターフェイス定義言語 (IDL) に基づいて作成されたコンパイル言語です。 ドライバーの MOF ファイルには、ドライバーが WMI に公開する各データブロックとイベントブロックの MOF クラス定義が含まれています。

WMI データブロックの MOF クラス定義は、次の構文に従います。

```mof
[Required and optional class qualifiers]

classClassName : OptionalBaseClass 
{ 
[key, read] 
string InstanceName; 
[read] 
boolean Active; 
[ Required and optional property qualifiers ] 
datatype itemname1; 
[ Required and optional property qualifiers ] 
datatype itemnameN; 
}; 
```

次のトピックでは、上に示した構文要素について説明します。

[WMI クラス修飾子](wmi-class-qualifiers.md)

[WMI クラス名と基本クラス](wmi-class-names-and-base-classes.md)

[WMI のクラスの必須項目](required-items-in-wmi-classes.md)

[WMI プロパティ修飾子](wmi-property-qualifiers.md)

[ドライバーによって定義される WMI データ項目](driver-defined-wmi-data-items.md)

[WMI クラスの例](wmi-class-examples.md)

WMI クライアントおよびその他の種類のアプリケーションに関連する MOF 構文の一般的な説明については、Microsoft Windows SDK を参照してください。

 

 




