---
title: Windows XP および Windows Me の WIA フィルム スキャナー互換性
description: Windows XP および Windows Me の WIA フィルム スキャナー互換性
ms.assetid: 9f96ef72-2482-435f-b512-b48c12dc1628
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 427f4e8d5a222bb24e9b536d245a0c7e5e6c3f26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360335"
---
# <a name="wia-film-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP および Windows Me の WIA フィルム スキャナー互換性





スキャンを実行するフィルム*いない*Microsoft Windows XP または Windows me. の存在 フィルム スキャナー (専用のフィルム スキャナーまたはフラット ベッド スキャナーのフィルム スキャナーを添付ファイル) は、Windows Vista で実行されている Windows XP の WIA アプリケーションにできなくなります。 [WIA 互換性レイヤー](wia-compatibility-layer.md)ですが、Windows Vista WIA サービス ハンドルだけベッドと基本的なフィーダー項目で (WIA\_カテゴリ\_ベッドと WIA\_カテゴリ\_フィーダー) の Windows XP アプリケーションを使用している場合、Windows Vista のデバイスフィルムとストレージの項目 (WIA\_カテゴリ\_フィルムおよび WIA\_カテゴリ\_FINISHED\_ファイル) は翻訳されません。

フィルムの項目の基本機能を模倣するためにフラット ベッドの項目を実装する場合は、Windows Vista を実行する Windows XP の WIA アプリケーションの基本的なサポートを行うことができます。 ユーザーに提示される既定のユーザー インターフェイスは、フラット ベッド スキャナーと同じため、アプリケーションは 1 つのフレームのみが表示なります。 また、このようなフラット ベッド項目を使用しても、Windows Vista ドライバーもうまくいきません Windows XP で Windows Vista で Windows XP のアプリケーションの一部のみがサポートを提供するため。

**注**   WIA フラット ベッド スキャナーの項目がスキャナーの項目のツリーで、最初の WIA 子項目にする必要があります、スキャナーでは、フラット ベッド スキャンもサポートする場合。

 

Windows XP および Windows Me の互換性の詳細については、次を参照してください。 [WIA フラット ベッド スキャナーの互換性の Windows と Windows XP](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)します。

 

 




