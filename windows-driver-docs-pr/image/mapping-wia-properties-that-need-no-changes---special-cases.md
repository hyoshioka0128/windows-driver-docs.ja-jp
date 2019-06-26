---
title: 変更する必要のない WIA プロパティのマッピング - 特殊なケース
description: 変更する必要のない WIA プロパティのマッピング - 特殊なケース
ms.assetid: 4ed02c01-efe8-4728-a54a-26fe27aa403c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9261968858e110a09f1ef491b68458cb349e9ff7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376588"
---
# <a name="mapping-wia-properties-that-need-no-changes---special-cases"></a>変更する必要のない WIA プロパティのマッピング - 特殊なケース


互換レイヤーが失敗する場合は次のとおりです。

-   不足している破損している Windows XP プロパティが必要な Windows Vista のプロパティに関連する互換性レイヤーを使用できないレンダリング可能性があります。 このような場合は、現在のセッションは失敗です。項目の構造とプロパティ (このような場合で、アプリケーションの COM プロキシに機能しない) Windows XP および Windows Vista のドライバーとアプリケーション間の違いにより続行のオプションは使用できません。 [ **WIA\_DPS\_ドキュメント\_処理\_選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)と[ **WIA\_DPS\_ドキュメント\_処理\_機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)プロパティは、特殊なケースは theWindows Vista のフラット ベッド項目のみが変換されます、Windows XP ドライバーによってサポートされていない場合アプリケーション

-   しない限り、その特定のコンテキストを設定すると、またはこれらのプロパティがコンテキストごとに異なる有効であり、現在の値がある可能性がありますに (フラット ベッドを送り、またはプロパティ コンテキスト) は、特定のコンテキストに依存する特定の Windows XP ルート プロパティを使用できない可能性があります。 WIA\_DPS\_ドキュメント\_処理\_正しいフィーダー/ベッド コンテキストを設定する選択が使用されます。、フィーダー (および必要な場合に双方向) に設定されますまたは Windows XP ドライバーのルート項目のフラット ベッドします。 その他のすべてのケースでコンテキスト設定してください、適切なプロパティ。 これは、場合も、Windows XP のデバイスは、フィーダーと、フラット ベッドの両方をサポートし、すべてのルートのプロパティは、Windows Vista のフラット ベッドとフィーダーの両方の項目に変換可能性があります。

-   重複する Windows Vista プロパティは、Windows XP の一意のプロパティを変換、WIA サービスについては、同じプロパティを別の Windows Vista 項目から別の値に設定されているケースを処理する方法を決定する必要があります。 ソリューションでは、コンテキストが変更されるたびに、すべての Windows XP A-AIT アイテムのプロパティを再初期化します。 このように別々 のプロパティのセットは、Windows Vista のドライバーのフィーダーとフラット ベッドの項目を Windows XP のアプリケーションからネゴシエートでした。

-   Windows Vista ドライバー フィーダーまたはベッドの項目を実装していないかどうか (たとえば、ドライバー実装フィルム/TPA(transparency adapter) や記憶域アイテムだけです)、互換性レイヤーは使用できません。 汎用の Windows XP の子項目は Windows Vista のフィルム/TPA やストレージの項目を常に作成できますと仮定する安全ではありません。 さらに、Windows Vista ドライバーがフィルム/TPA とストレージの両方のアイテムを実装している場合、さらに多くの問題が発生する可能性が。 そのため、少なくとも、ベッドまたはフィーダー項目を実装していない Windows Vista のドライバーの互換性レイヤが機能しません。

-   ドライバーは、部分的には、新しい Windows Vista 項目構造のサポートを実装が、Windows Vista のイメージの完全なサポートを提供する失敗する場合、Windows XP ドライバーが例については、正しい Windows XP 項目構造 (ルートと子項目をスキャン) を実装しない場合転送では、プロパティまたは項目の互換性レイヤが無効にして、現在のセッションは失敗します。

 

 




