---
title: Windows XP の WIA フラット ベッド スキャナーの互換性と Windows Me
description: Windows XP の WIA フラット ベッド スキャナーの互換性と Windows Me
ms.assetid: fc3424fa-3898-4f6a-a611-f81d97db8b1d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4665903ce1cc4e878167bfc801ce702b2ccbe8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532702"
---
# <a name="wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP の WIA フラット ベッド スキャナーの互換性と Windows Me





Windows Vista WIA 項目ツリーし、Windows XP および Windows me 向けに作成されたアプリケーションである互換性の問題を原因します。

Windows Vista WIA ドライバーとアプリケーションと古い WIA ドライバーとアプリケーション間の互換性の問題を簡略化するのには、Windows Vista は、内部互換性レイヤーが。 この互換レイヤーを使用して、Windows Vista のドライバーとアプリケーション、Windows XP (および Windows Me) ドライバーとアプリケーションをそれぞれ使用するができます。 Windows vista では、この変換処理では、ドライバーとアプリケーションの両方に対して透過的です。 この互換レイヤーの詳細については、次を参照してください。 [WIA 互換性レイヤー](wia-compatibility-layer.md)します。

ただし、Windows Vista のドライバーと Windows XP または Windows Me でアプリケーションの互換性は複雑です。 従来、オペレーティング システムに存在していた WIA のバージョン用に作成されたアプリケーションでは、異なる一連の規則と前提条件に従います。 Windows XP と Windows アイテム ツリー内の 1 つの項目の上にスキャナーの機能を組み合わせて Me WIA スキャナー項目ツリーです。 ルート項目は、その子項目の転送動作を制御します。 スキャナーは最初の子項目を使用して、プログラミング可能なデータ ソースと、ルート項目のプロパティとしてなど[ **WIA\_DPS\_ドキュメント\_処理\_選択**](https://msdn.microsoft.com/library/windows/hardware/ff551384) (WIA と呼ばれる\_IP\_ドキュメント\_処理\_Windows Vista で選択) スキャン ベッドとスキャン フィーダーを切り替えます。

このオーバー ロードの項目のアプローチでは、スキャナーの機能を分類するための重要な WIA 項目の必須の WIA プロパティを追跡するアプリケーションが必要です。 場合、WIA\_DPS\_ドキュメント\_処理\_スキャナーのルート項目選択のプロパティが存在する、アプリケーションでは、スキャナーがドキュメント フィーダーのスキャンをサポートしている前提としています。 このプロパティがフラット ベッドに設定されている場合、アプリケーションでは、スキャナーもサポートしているフラット ベッドからプラテン上スキャン前提としています。 その結果、古い WIA アプリケーションは新しい WIA スキャナー項目ツリーのルートに移動し、デバイスの機能を伝えている任意のプロパティは見つかりません。

**注**  フラット ベッド スキャナーの項目は、他のスキャン データ ソースが実装されている場合、WIA 項目ツリーの最初の子項目にする必要があります。 この場所により、基本的なフラット ベッド スキャナーの動作は、Windows XP および Windows Me のアプリケーションは、デバイスの機能をスキャン ベッドに自動的に検出されます。 一部のアプリケーションでは、唯一の子項目を使用して、最初の子項目に移動し、フラット ベッドまたはスキャナーのフィーダーであるとします。 最初の子項目としてフラット ベッド スキャナーの項目にスキャナーの項目のツリーを実装すると、多くの旧バージョンとの互換性に関する問題ができなくなります。

 

互換性の詳細については、次を参照してください。 [WIA 項目のプロパティと場所の変更](wia-item-property-and-location-changes.md)します。

 

 




