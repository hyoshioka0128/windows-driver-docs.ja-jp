---
title: Windows XP および Windows Me の WIA フィーダー スキャナー互換性
description: Windows XP および Windows Me の WIA フィーダー スキャナー互換性
ms.assetid: 7877943e-ee61-455d-b489-db223e1ddbe1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd54ce7772b237476bbb60450dbfea5f4aad6435
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571210"
---
# <a name="wia-feeder-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP および Windows Me の WIA フィーダー スキャナー互換性





このトピックでは、Windows Vista、Windows XP、および Windows me. フィーダー スキャナーに関連するいくつかの互換性の問題を説明します

### <a name="changes-from-windows-xp-to-windows-vista"></a>Windows XP から Windows Vista への変更

さまざまな Windows XP と Windows Vista のスキャンを処理する方法の変更が発生しました。 たとえば、Windows Vista では、機能ユニットごとは別のカテゴリに属しています。 これらのカテゴリの表現、 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)プロパティとして WIA\_カテゴリ\_を送り、フィーダーと WIA\_カテゴリ\_ベッドのフラット ベッドします。 これらの項目の両方がある場合、スキャナーで Windows Vista では、どちらも項目のツリーで表されます。 Windows xp の場合、すべてのスキャナーの機能単位を表す項目のツリーで、項目を単一のスキャンが発生しました。

次の図では、Windows XP では、スキャナーの項目のツリーが表示されます。

![windows xp では、スキャナー項目のツリーを示す図](images/wia-feeder-tree-xp.png)

転送のすべては、この項目を無効になり、(フィーダーとフラット ベッドの両方) のすべてのスキャン設定を使用します。

これに対し、次の図は、Windows Vista では、フラット ベッドとフィーダーの付いたスキャナーのスキャナーの項目のツリーを表示します。

![フラット ベッドと windows vista では、フィーダーの付いたスキャナーのスキャナーの項目のツリーを示す図](images/wia-feeder-tree4.png)

この項目のツリーは、項目のツリー、フラット ベッドとフィーダーに別の項目として関数単位を表します。 スキャナーのこの種類の詳細については、次を参照してください。[非二重モード対応のドキュメント フィーダー](non-duplex-capable-document-feeder.md)します。

スキャナーが (つまり、ドキュメントの両方の側をスキャン) の二重化できる場合は、Windows Vista の項目のツリーは次の図のようになります。

![両面印刷で windows vista スキャナーの項目のツリーを示す図](images/wia-feeder-tree3.png)

上記の図は、フラット ベッドとフィーダーの付いたスキャナーを表す項目ツリーを示しています。

なし、Windows Vista でのフラット ベッド スキャナーの項目のツリーは、次の図のようになります。

![windows vista フィーダー スキャナー項目のツリーを示す図](images/wia-feeder-tree1.png)

両面印刷をスキャナーの項目のツリーおよびフィーダー スキャナーの項目のツリーは、データ転送は、常にフィーダー項目から発生します。 スキャン設定フィーダーと (前面と背面の両方) の子項目の両方に格納されます。

同じ設定にフロント エンドとバックエンドの項目が設定される場所のスキャンが呼び出されます、*双方向の基本的な*をスキャンします。 フロント エンドとバックエンドの項目は互いに独立して設定されている場合、スキャンが呼び出されます、*双方向の高度な*をスキャンします。 これらの種類のスキャンの詳細については、次を参照してください。[単純な二重モード対応のドキュメント フィーダー](simple-duplex-capable-document-feeder.md)と[二重モード対応ドキュメント フィーダー付きの高度な](advanced-duplex-capable-document-feeder.md)します。

### <a name="compatibility-support-in-windows-vista"></a>Windows Vista での互換性をサポート

Windows XP 用の Windows Vista のドライバーやアプリケーションの互換性は、Windows Vista 内にある、WIA サービスで互換レイヤーによって処理されます。 このレイヤーは、Windows XP で使用されていた、同じ方法で Windows Vista で使用する、以前のアプリケーションおよびドライバーです。 ただし、古いアプリケーションと Windows Vista のアプリケーションと比較してドライバーおよびドライバーの機能の一部が失われるがあります。

### <a name="compatibility-support-in-windows-xp"></a>Windows XP での互換性をサポート

Windows Vista のドライバーを使用して、Windows XP コンピューター上の非常に制限付きサポートがあります。 フィーダー スキャナーでは、フラット ベッド スキャンもサポートしています、WIA フラット ベッド スキャナーの項目は、ルート項目の後に、スキャナーの項目のツリーの最初の WIA 子項目をある必要があります。 この項目のツリー ダイアグラムに示されています、[非二重モード対応のドキュメント フィーダー](non-duplex-capable-document-feeder.md)トピック。 Windows XP でのスキャン設定をすべてをツリー内で最初の項目を検索する必要がありますので、この構成は Windows Vista のドライバーと Windows XP のいくつかの互換性を許可します。

互換レイヤーと Windows XP および Windows Me の互換性の詳細については、次を参照してください。 [WIA フラット ベッド スキャナーの互換性の Windows と Windows XP](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)します。

 

 




